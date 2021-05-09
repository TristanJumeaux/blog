---
author: "Tristan Jumeaux"
title: "Apache Hive : My understanding, walkthrough a request"
date: "2021-03-18"
description: "An article that explain why Hive exists and how it is working."
weight: 1
tags: ["Data","Big Data", "Warehouse"]
ShowToc: true
TocOpen: true
---

It’s been two months now that I’ve started my first job as a Data Engineer. 
My daily work involves interactions with Hadoop’s HDFS, Hbase and Hive.
I’ve got to say that it is an exciting period ! I’m learning tons of new stuff.
Anyway, let’s dive in Hive !


## What's Hive ?

Used on top of file systems (HDFS, S3,..) Hive allows you to do data warehousing. You can create databases and tables that you can request as in other databases.
Initially developed by Facebook in the early 2010s, it became very popular among companies handling important volumes of data.

## Why ? 

Everything comes from trying to analyze important volumes of data. 
To do so, back in the 2010s, we had to think and work with MapReduce. 
However, it’s not easy nor fast to create MapReduce jobs. 
Moreover, the majority of analysts were/are used to thinking the SQL way. 
It would have been hard for them to switch to the MapReduce paradigm.

These observations led to the creation of [Hive](https://hive.apache.org/), a data warehouse for large datasets ! 
How did they fill these needs ?

## Architecture

![s3bucket](/images/archi_hive.png)

### Requesting 

To begin with, Hive can receive requests from several sources.

There are two main ways of accessing Hive datas.

Firstly, you can query Hive using JDBC/ODBC clients.
These options will transits through HiveServer2. 
To summarize, HiveServer2 is an interface that receives remote requests, transmits them to Hive and retrieves results.

Also, Hive provides a CLI called Beeline. It bypasses the HiveServer2 and communicates directly with the Driver.

### Processing

Let’s assume that we have a request that has been transmitted to Hive.

It will now come by what’s called the Hive Driver.
The driver plays a crucial role, he's the main component of Hive.
As a basketball fan, I often like to compare it to a point guard. He is directing what happens.
A more global comparison would be to see it as the process in the driver seat of the Hive car.

The first thing that the driver is going to do is to call the compiler. 
The goal of this step is to make sure that the request is correct. If so, begin the translation to a job.

To begin with, the compiler will parse the request and call the metastore.

_What is the metastore?_ It is a database referencing every table and its metadatas. It contains the location of data for each table and its schema. <br/>
Hence, the compiler will ask for the metastore informations about the tables that are referenced by the request.

After gathering everything he needs, the compiler can start its work. 

Here are 4 bullet points summing up compiler's actions :
* Type checking and semantic analysis to ensure that the request respects database and tables.
* Creation of a logical plan: translate the request to a tree of operators. Operators can be joins, filters, groupby,..
* Call the [Optimizer](https://cwiki.apache.org/confluence/display/Hive/Design#Design-Optimizer) to improve performances on operations like Joins or groupby. 
* Analyze the operator tree and convert it to a sequence (a DAG) of jobs (Map/Reduce jobs or metastore changes or file system changes,..) called a Query Plan.

Here, we realize what’s great about Apache Hive. Remember what we talked about during the introduction ? Now we have a product that creates Map/Reduce jobs from SQL requests. This is great. But the job isn’t finished !

### Retrieving

As Mike Goldberg said powerfully, __Here we go__ ! It’s time to execute our request!
In order to do so, we need to find an execution engine that allows us to process MapReduce on HDFS.

MapReduce, Spark or Tez are the 3 frameworks that we can choose.
Tez has been promoted as the default one by Hive. It is an upgraded version of MapReduce. As a quick recap, MapReduce splits his work in many stages and consequently spends too much time writing results to disk. On the other hand, Tez does as many operations as possible in memory and minimizes the writes.

Any of these 3 frameworks, will get our DAG and execute the different steps.
To do so, they will deal with YARN to get containers and resources necessary.

At the end, the execution engine will send back the results to the Driver which will, itself, send it back to the client.

This is how Hive processes SQL requests on high volumes of data.

## What’s my usage of Hive ?

During my daily work, Hive has several use cases.

The main one is for Analysts. Using a JDBC/ODBC connector and a client, they study the results of processes that have run.

The second one, a similar one, is for technical teams.
When there is a problem detected by the Analysts, having Hive tables allows us to understand where the various errors came from.
Similarly, when developing and running a new feature, having Hive tables at some key steps helps us to monitor progress.

## Business value

The main value lies when a company is dealing with important volumes of data in a Hadoop cluster. Hive is a product that can leverage a significant ROI. It gives you visibility about your datas.

Moreover, the possibility to request in an SQL like syntax is cost and time saving. Your data analysts will not need a lot of time to adapt, they will be operational instantaneously.

To end with, Cloudera now offers support around Apache Hive. They can help you with your implementation and usage. It can be a nice help for companies entering the Data world.

## Conclusion 

This blog post is about to end ! 
We’ve seen Hive architecture and how it processes a request.
In these explanations, everything has been about on-premise architecture. 
However, for a couple of years, public clouds arrived and changed the data landscape.
What’s the role of Apache Hive in these new environments ? It might be a great topic for a next blog post, reach out if you’re interested ! 

### References

https://cwiki.apache.org/confluence/display/Hive/Home#Home-UserDocumentation
https://cwiki.apache.org/confluence/display/Hive/Design#Design-Compiler
