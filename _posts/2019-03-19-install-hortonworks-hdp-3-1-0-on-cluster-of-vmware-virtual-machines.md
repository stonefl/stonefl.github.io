---
layout: post
published: true
title: Install Hortonworks HDP 3.1.0 on Cluster of VMWare Virtual Machines
subtitle: Hortonworks Tutorials
date: '2019-03-19'
bigimg: /img/post/hortonworks.png
categories:
  - Tutorial
tags:
  - Hadoop
  - Big Data
---
This post describes the process that I followed to install Hortontworks HDP 3.1.0 on a cluster with three VMWare virtual Hosts. This process followes three major steps: 1) set up the cluster environemnt; 2) set up a local repository for both Ambari and HDP stacks; 3) install HDP stacks through Ambari server. You can follow this process to install other versions, you can check product versions through Hortonworks support matrix: https://supportmatrix.hortonworks.com/



<!--more-->

# Table of Content

{:.no_toc}

* TOC
{:toc}

# Virtual Nodes Info

First thing I did is set up three virtual hosts in VMWare with following info:


|   Host Name   |   Host IP      | Configuration|
| ------------- | -------------  |------------- |
| hadoop-master | 146.xxx.xxx.75 | 4 x cpu, 16 GB Ram, 100 GB disk|
| hadoop-node-1 | 146.xxx.xxx.76 |4 x cpu, 16 GB Ram, 100 GB disk |
|hadoop-node-2  | 146.xxx.xxx.77 |4 x cpu, 16 GB Ram, 100 GB disk |

for each host, `yum` has been setup.

# Prepare the Cluster Environment

## 0. Setting Proxy

If you're behind proxy, then many repositories, including `yum` repository, are accessed through proxy servers. For each host, you can set up proxy server info through adding

```
export https_proxy=https://<your.https-proxy.address>:<port#>
export http_proxy=http://<your.http-proxy.address>:<port#>
```

to the `/root/.bashrc`. And run `source .bashrc` to refresh.

## 1. Make sure the run level is multi-user text mode. 

Run following command to check the run level:

```bash
systemctl get-default
```

It is expected to see the response of `multi-user.target`. If not, run following command to change:

```bash
systemctl set-default multi-user.target
```

## 2. Check and set hostnames.

- For each host in the cluster, confirm that the hostname is set to a `FQDN` name by running following command:

```bash
hostname -f
```

This should return a a fully qualified domain name ([FQDN](https://en.wikipedia.org/wiki/Fully_qualified_domain_name)), which has a format like `fully.qualified.doman.name` 
You can use `hostname` command to set the hostname on each host in the cluster. For example:

```bash
hostname hadoop-master.qualified.doman.name
```

- Edit Network Configuration File. For each host in the cluster, open the network configuration file through 

```bash
vi /etc/sysconfig/network
```

Modify the HOSTNAME property to FQDN:

```
NETWORK=yes
HOSTNAME=fully.qualified.doman.name
```

- Edit the hosts file. Open the hosts file on each host in the cluster through `vi /etc/hosts` add a line to each file. For example:

```
146.xxx.xxx.75 hadoop-master.qualified.doman.name hadoop-master
146.xxx.xxx.76 hadoop-master.qualified.doman.name hadoop-node-1
146.xxx.xxx.77 hadoop-master.qualified.doman.name hadoop-node-2
```

After made these changes. It needs reboot through running `reboot`.

## 3. Set up password-less SSH:

- Login to the `hadoop-master` host with `root` user and generate SSH keys using `ssh-keygen -t rsa`. Press enter for all prompts and accept all default values.	
- Run following command to copy ssh identification for localhost. Enter password when prompted for the password:

```
ssh-copy-id localhost
```

Then run command `ssh hadoop-master` to make sure no password needed.

**For each of other hosts in the cluster:**

- Copy the SSH file from `hadoop-master` to every other hosts in the cluster, for example:

```
scp -pr /root/.ssh root@hadoop-node-1.qualified.doman.name:/root/
```

- Upload the generated `id_rsa.pub` to the `root`'s **.ssh** directory as a file with name **authorized_keys**, for example:

```
 cat .ssh/id_rsa.pub | ssh root@hadoop-node-1.qualified.doman.name 'cat >> .ssh/authorized_keys'
```

- Set permissions for **.ssh** directory and **authorized_keys** file:

```
ssh root@hadoop-node-1.qualified.doman.name; chmod 700 .ssh; chmod 640 .ssh/authorized_keys
```

From the `hadoop-master` host, run following commands in sequence, to make sure inter-node connection using SSH without password:

```
ssh hadoop-node-1
ssh hadoop-node-2
ssh hadoop-master
ssh hadoop-node-2
ssh hadoop-node-1
ssh hadoop-master
```

## 4. Enable NTP

Run following commands on each host to install and enable NTP service:

```
yum install -y ntp
systemctl enable ntpd
systemctl start ntpd
```

After that run `timedatectl status` and look for following lines to verfiy that NTP is running

```
NTP enabled: yes
NTP synchronized: yes
```

To synchronze:

- stop ntp serivce: `systemctl stop ntpd`
- add `server your.ntp.server.address` to the `/etc/ntp.conf` 's servers part.
- Force time synchronize: `ntpdate your.ntp.server.address`
- Restart ntp: `systemctl start ntpd`
- Run `systemctl enable ntpdate` to make sure running the `ntpdate` at boot time.

## 5. Configuring Firewall

Run following commands to disable firewall on each host in the cluster:

```
systemctl disable firewalld
service firewalld stop
```

Run `systemctl status firewalld` to make sure firewall is disabled.

## 6. Disable SElinux

For each host in the cluster, change SELINUX value from **enhancing** to **disabled** in `/etc/selinux/config`

## 7. Install `wget` 

Install `wget` on all nodes:

```
yum install -y wget
```

# Set up a Local Repository for Ambari and HDP Stack

## 1.  Create and start an HTTP sever on the master host: 

```
yum install -y httpd
service httpd restart
chkconfig httpd on
```

Make sure there is the repository `/var/www/html`has been created on the host.

## 2. Set up the local repository

- Download the tarball files for Ambari and HDP stacks through following commands:

```
wget http://public-repo-1.hortonworks.com/ambari/centos7/2.x/updates/2.7.3.0/ambari-2.7.3.0-centos7.tar.gz

wget http://public-repo-1.hortonworks.com/HDP/centos7/3.x/updates/3.1.0.0/HDP-3.1.0.0-centos7-rpm.tar.gz

wget http://public-repo-1.hortonworks.com/HDP-UTILS-1.1.0.22/repos/centos7/HDP-UTILS-1.1.0.22-centos7.tar.gz

wget http://public-repo-1.hortonworks.com/HDP-GPL/centos7/3.x/updates/3.1.0.0/HDP-GPL-3.1.0.0-centos7-gpl.tar.gz

```

The URL's can be obtained from [Ambari Repositories](https://docs.hortonworks.com/HDPDocuments/Ambari-2.7.3.0/bk_ambari-installation/content/ambari_repositories.html) and [HDP 3.1.0 Repositories](https://docs.hortonworks.com/HDPDocuments/Ambari-2.7.3.0/bk_ambari-installation/content/hdp_31_repositories.html)

- Untar and copy the files to `/var/www/html/`. For example, 
  `tar zxvf ambari-2.7.3.0-centos7.tar.gz -C /var/www/html/`
  Then record the base URL's which are needed for installing the cluster:

```
Ambari: http://146.xxx.xxx.75/ambari/centos7/2.7.3.0-139/
HDP: http://146.xxx.xxx.75/HDP/centos7/3.1.0.0-78/
HDP-GPL: http://146.xxx.xxx.75/HDP-GPL/centos7/3.1.0.0-78/
HDP-UTILS: http://146.xxx.xxx.75/HDP-UTILS/centos7/1.1.0.22/
```

**Tips**:

1. make sure you can browser in the web browser;
2. The path where you can see the `repodata` directory.

# Installing Ambari Server and Agent

## 1. Download Ambari Repository

- Login to the `hadoop-master` host as `root`
- Check the repository URL from [Ambari Repository Links](https://docs.hortonworks.com/HDPDocuments/Ambari-2.7.3.0/bk_ambari-installation/content/ambari_repositories.html)
- Download Ambari repository file to the directory`/etc/yum.repos.d/`, through following command:

```
wget -nv http://public-repo-1.hortonworks.com/ambari/centos7/2.x/updates/2.7.3.0/ambari.repo -O /etc/yum.repos.d/ambari.repo
```

- Edit the `ambari.repo` file and change the `baseurl` and `gpgkey` to the local repository obtained above.
- Run `yum repolist` to confirm that the repository has been configured successfully. You should see `ambari-2.7.3.0-xxx` on the list.
  See [Download Ambari Repository](https://docs.hortonworks.com/HDPDocuments/Ambari-2.7.3.0/bk_ambari-installation/content/download_the_ambari_repo_lnx7.html) for more information.

## 2. Install Ambari Server

Install the Ambari server on the master node through command:

```
yum install -y ambari-server
```

See [Install Ambari Server](https://docs.hortonworks.com/HDPDocuments/Ambari-2.7.3.0/bk_ambari-installation/content/install-ambari-server-rhel7.html) for more information.

## 3. Set up Ambari Server

Set 
`-Dhttp.proxyHost=<yourProxyHost> -Dhttp.proxyPort=<yourProxyPort> -Dhttps.proxyHost=<yourProxyHost> -Dhttps.proxyPort=<yourProxyPort>`
in the file `/var/lib/ambari-server/ambari-env.sh`
Run following command on the Ambari server host to start the setup process:

```
ambari-server setup
```

See [Set Up Ambari Server](https://docs.hortonworks.com/HDPDocuments/Ambari-2.7.3.0/bk_ambari-installation/content/set_up_the_ambari_server.html) for more information.

# Install, Configure and Deploy the Cluster

## 1. Start the Ambari Server

```
ambari-server start
```

After the server starts successfully, you can login to the server with default user/name `admin/admin` at:
`http://146.xxx.xxx.75:8080/`

## 2. Installing HDP through Installation Wizard

Follow the steps of the Wizard intall HDP:

- Step 0 Get Started: give a name to your cluster, for example, `InfoSecHadoop`

- Step 1 Select Version: Select `HDP-3.1`, `Use Local Repository`. Delete all other OS, leave readhat7 only. Copy the Base URL to the places.

- Step 2 Install Options:

  ![step2.png](../img/post/Step2.JPG)

- Step 3 Confirm Hosts: it will automatically do the regiestration with the setting in Step 2.

- Step 4 Choose Services: choose basic ones, you can add more later.

- Step 5 Assign Masters: keep default

- Step 6: Select all for the `Client` option.

**Error 1:** emtpty HDP Url: https://community.hortonworks.com/articles/231020/ambari-273-ambari-writes-empty-baseurl-values-writ.html

**Error 2:** Requires: libtirpc-devel: https://community.hortonworks.com/idea/107386/libtirpc-devel-required.html
Run following commands on all hosts:

```
subscription-manager repos --enable=rhel-7-server-optional-rpms
yum install -y libtirpc-devel
```

**Error 3** Hive install failed because of mysql-connector-java.jar due to HTTP error: HTTP Error 404: Not Found
https://community.hortonworks.com/articles/170133/hive-start-failed-because-of-ambari-error-mysql-co.html
Run following commands on Ambari server:

```
yum install -y mysql-connector-java
ls -al /usr/share/java/mysql-connector-java.jar
cd /var/lib/ambari-server/resources/
ln -s /usr/share/java/mysql-connector-java.jar mysql-connector-java.jar

```

**Error 4** Empty Baseurl for Public Repository (No solution, might be proxy issue):
https://community.hortonworks.com/questions/45147/ambari-setup-select-stack-404-error.html
https://community.hortonworks.com/questions/35820/hdp-stack-repositories-not-found.html

**Error 5** Ambari Files View - Service hdfs check failed:
Solved: In order to fix it you should try creating a new "File View" instance by clicking on the "Create Instance" button on the File View. You can choose the default options to create the view instance (if it is not kerberized)
https://community.hortonworks.com/questions/128758/service-hdfs-check-failed-from-ambari.html?page=1&pageSize=10&sort=votes

https://community.hortonworks.com/questions/176438/ambari-files-view-service-hdfs-check-failed.html

https://community.hortonworks.com/questions/88350/service-hdfs-check-failed-1.html

https://community.hortonworks.com/questions/131550/ambari-views-fail-after-kerberos-enabled.html

# References

Official HDP 3.10 installation documentation: <https://docs.hortonworks.com/HDPDocuments/HDP3/HDP-3.1.0/index.html>

Apache Ambari Installation Document:
https://docs.hortonworks.com/HDPDocuments/Ambari-2.7.3.0/bk_ambari-installation/content/ch_Getting_Ready.html

Check Hortonworks Support Matrix to make sure product versions:
<https://supportmatrix.hortonworks.com/>

Using yum with a Proxy server
https://docs.fedoraproject.org/en-US/Fedora_Core/3/html/Software_Management_Guide/sn-yum-proxy-server.html
