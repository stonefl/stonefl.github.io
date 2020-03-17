---
layout: post
published: true
title: Setup Kubeflow Cluster in Shared VPC on Google Cloud Platform
date: '2020-03-21'
categories:
  - Google Cloud Platform
tags:
  - Kubeflow
---
[Kubeflow](https://www.kubeflow.org/) is an open-source project which aims to make running ML workloads on Kubernetes simple, portable and scalable. However, setting up a Kubeflow cluster in a shared VPC on Google Cloud Platform can not be done through the web console yet. This post tries to describe the steps you need to follow to set up a Kubeflow using a Shared VPC through command line. 
<!--more-->

## Prepare the Environment
1. Install [Google SDK](https://cloud.google.com/sdk/), if you use Cloud Shell, enable the [boost mode](https://cloud.google.com/shell/docs/features#boost_mode). The following steps are tested in Cloud Shell. 
2. Run this command in the service project to check if subnet and secondary ranges are usable
```
gcloud container subnets list-usable \                 
--project <service project ID> \  
--network-project <Host Project ID>
```
3. Follow this guide to [set up OAuth for Cloud IAP](https://www.kubeflow.org/docs/gke/deploy/oauth-setup/).
4. Download and install `kfctl` from [kfctl releases page](https://github.com/kubeflow/kfctl/releases/tag/v1.0):

```
# make a bin folder to contain the kfctl
mkdir ~/bin
# download kfctl from the releases page
wget -P /tmp https://github.com/GoogleCloudPlatform/training-data-analyst/raw/master/courses/data-engineering/kubeflow-resources/kfctl_v1.0-0-g94c35cf_linux.tar.gz 
# unzip to the bin folder
tar -xvf /tmp/kfctl_v1.0-0-g94c35cf_linux.tar.gz -C ~/bin
# add the kfctl binary to the PATH
export PATH=$PATH:~/bin
```
5. Configure gcloud default values for zone and project:
```
# Set your GCP project ID and the zone where you want to create 
# the Kubeflow deployment:
export PROJECT=<your GCP project ID>
export ZONE=<your GCP zone>

gcloud config set project ${PROJECT}    
gcloud config set compute/zone ${ZONE}
```
6. Select the KFDef spec to use as the basis for your deployment
```
export CONFIG_URI="https://raw.githubusercontent.com/kubeflow/manifests/v1.0-branch/kfdef/kfctl_gcp_iap.v1.0.0.yaml"
```
7. Create environment variables containing the OAuth client ID and secret that you created earlier
```
export CLIENT_ID=<CLIENT_ID from OAuth page>
export CLIENT_SECRET=<CLIENT_SECRET from OAuth page>
```
The CLIENT_ID and CLIENT_SECRET can be obtained from the Cloud Console by selecting** APIs & Services** -> **Credentials**

8. Pick a name KF_NAME for your Kubeflow deployment and directory for your configuration.
```
export KF_NAME=<your choice of name for the Kubeflow deployment>
export BASE_DIR=<path to a base directory>
export KF_DIR=${BASE_DIR}/${KF_NAME}
```
*  For example, your kubeflow deployment name might be ‘my-kubeflow’ or ‘kf-test’.
* Set base directory where you want to store one or more Kubeflow deployments. For example, ${HOME}/kf_deployments.

## Deploy Kubeflow with Customization

1. Download the KFDef file to your local directory to allow modifications
```
export CONFIG_FILE="kfdef.yaml"
mkdir -p ${KF_DIR}
cd ${KF_DIR}
curl -L -o ${CONFIG_FILE} https://raw.githubusercontent.com/kubeflow/manifests/v1.0-branch/kfdef/kfctl_gcp_iap.v1.0.0.yaml
```
**CONFIG_FILE** should be the name you would like to use for your local config file; e.g. “kfdef.yaml”

2. Edit the KFDef spec in the yaml file. The following snippet shows you how to set values in the configuration file using yq:

```
yq w -i ${CONFIG_FILE} 'spec.plugins[0].spec.project' ${PROJECT}
yq w -i ${CONFIG_FILE} 'spec.plugins[0].spec.zone' ${ZONE}
yq w -i ${CONFIG_FILE} 'metadata.name' ${KF_NAME}
```
3. Run the kfctl build command to generate kustomize and GCP Deployment manager configuration files for your deployment:
```
cd ${KF_DIR}
kfctl build -V -f ${CONFIG_FILE}
```
4. Then update the `${KF_DIR}/gcp_config/cluster.jinja` file created from step 3 to specify the network and subnetwork:
```
cluster:
  name: {{ CLUSTER_NAME }}
  network: projects/<host project ID>/global/networks/<network name>
  subnetwork: projects/<host project ID>/regions/<region>/subnetworks/<subnet name>
  initialClusterVersion: "{{ properties['cluster-version'] }}"
```
5. In `${KF_DIR}/gcp_config/cluster.jinja`, disable subnetwork creation and specify secondary IP ranges by name (ipAllocationPolicy section may have to be moved out of the IF block if you aren't setting private cluster = true)
```
{% if properties['securityConfig']['privatecluster'] %}
ipAllocationPolicy:
  createSubnetwork: false
  useIpAliases: true
  clusterSecondaryRangeName: <name of secondary ip range for pods>
  servicesSecondaryRangeName: <name of secondary ip range for services>
```
6. Enable private clusters by editing `${KF_DIR}/gcp_config/cluster-kubeflow.yaml` and updating the following two parameters:
```
privatecluster: true
gkeApiVersion: v1beta1
```
7. After above changes, run the kfctl apply command to deploy Kubeflow:

```
cd ${KF_DIR}
kfctl apply -V -f ${CONFIG_FILE}
```
Cluster creation will take 3 to 5 minutes to complete. Do not proceed until the command prompt is returned in the console.

Note: You may notice warnings in the console related to ... **Encountered error applying application cert-manager** ... and ... **Default user namespace pending creation** ... these are advisory and will not affect completion of the cluster.

While it is running, you can view instantiation of the following objects in the GCP Console:

In **Deployment Manager**, two deployment objects will appear:
* {KF_NAME}-storage
* {KF_NAME}kubeflow-qwiklab
In **Kubernetes Engine**, a cluster named as {KF_NAME} will appear:
* In the Workloads section, a number of Kubeflow components
* In the Services section, a number of Kubeflow services

When the deployment finishes, check the resources installed in the namespace kubeflow in your new cluster. To do this from the command line, first set your kubectl credentials to point to the new cluster:
```
gcloud container clusters get-credentials ${KF_NAME} --zone ${ZONE} --project ${PROJECT}
```
Then see what’s installed in the `kubeflow` namespace of your GKE cluster:
```
kubectl -n kubeflow get all
```

## Delete Kubeflow Deployment
Once you done your job, you use the following commands to delete the deployment:
```
# If you want to delete all the resources, including storage:
kfctl delete -f ${CONFIG_FILE} --delete_storage

# If you want to preserve storage, which contains metadata and information
# from Kubeflow Pipelines:
kfctl delete -f ${CONFIG_FILE}
```


## References

https://googlecoursera.qwiklabs.com/focuses/46792

https://github.com/kubeflow/kubeflow/issues/3082

https://www.kubeflow.org/docs/gke/deploy/deploy-cli/

https://www.kubeflow.org/docs/gke/private-clusters/


