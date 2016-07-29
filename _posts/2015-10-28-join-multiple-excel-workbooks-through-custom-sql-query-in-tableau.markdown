---
author: stonefl
comments: true
date: 2015-10-28 20:09:31+00:00
layout: post
link: https://leifengtechblog.wordpress.com/2015/10/28/join-multiple-excel-workbooks-through-custom-sql-query-in-tableau/
slug: join-multiple-excel-workbooks-through-custom-sql-query-in-tableau
title: Join Multiple Excel Workbooks through Custom SQL Query in Tableau
wordpress_id: 150
categories:
- Tips and Tricks
tags:
- SQL
- Tableau
---

Recently I came across the need of joining multiple excel files in Tableau. I did a hard research on how to do it. However, most of the instructions I found were about how to join two tabs in the same excel workbook. In this post, I will describe how to join multiple worksheets from different workbooks, which spent me about one hour to figure out. Please note the instructions here work for Tableau Desktop 9.0 or later.


## Scenario


Suppose we have one Excel workbook that contains one worksheet that would be joined with another worksheet in another workbook. For example, there is a 'Connections' worksheet in workbook 'testjoin01.xlsx', recording the origin, destination, and travel times.

[caption id="attachment_153" align="alignnone" width="232"][![Connections in 'testjoin01.xlsx'](https://leifengtechblog.files.wordpress.com/2015/10/01.png)](https://leifengtechblog.files.wordpress.com/2015/10/01.png) Connections in 'testjoin01.xlsx'[/caption]

We want to join it with the 'Nodes' worksheet in workbook 'testjoin02.xlsx'. The sheet stores latitude and longitude of associated nodes.

[caption id="attachment_154" align="alignnone" width="215"][![Nodes in 'testjoin02.xlsx'](https://leifengtechblog.files.wordpress.com/2015/10/02.png)](https://leifengtechblog.files.wordpress.com/2015/10/02.png) Nodes in 'testjoin02.xlsx'[/caption]


## Use Custom SQL to Create the Join




## Step 1


Open a new Tableau workbook, select **Excel** in the Connect To a file section. Find the 'testjoin01.xlsx' workbook, and click the drop-down arrow next to **Open**, and select **Open with Legacy Connection.**


## Step 2


Drag the** New Custom SQL** table from the left pane to the join area.


## Step 3


In the custom SQL query field, copy and paste the LEFT JOIN query similar to the one shown below, change and update to your use case.

[code language="SQL" collapse="false" title="Custom SQL"]
SELECT 
a.*,
b.[LAT] AS [OR_LAT], b.[LONG] AS [OR_LONG],
c.[LAT] AS [DE_LAT], c.[LONG] AS [DE_LONG]
FROM(([Connections$] AS a
  LEFT JOIN
   [C:\Users\lf\Desktop\testjoin02.xlsx].[Nodes$] AS b 
      ON a.[Orig] = b.[ICLOC])
  LEFT JOIN
   [C:\Users\lf\Desktop\testjoin02.xlsx].[Nodes$] AS c 
      ON a.[Dest] = c.[ICLOC])
[/code]

In the SQL query above, nested left joins are used to join the Nodes sheet in the second workbook twice, one for the origin, the other for the destination. Please note, the full path of the second workbook has to be specified in the left joins.
