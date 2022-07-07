# Introduction to CERN Analytix

### Table of content

2. [Requests and access](#requests-and-access)
3. [EOS](#eos)
4. [SWAN](#swan)
5. [PySpark on SWAN](#pyspark-on-swan)
6. [HDFS Starter](#hdfs-starter)
7. [LXPLUS](#lxplus)

### Requests and access

1. Hadoop Cluster Access
    * To do data analysis and be connected to the Hadoop cluster, you need to gain the Hadoop cluster access fisrt via the [CERN Service Portal.](https://cern.service-now.com/service-portal?id=service_element&name=Hadoop-Service)
    * [Getting started with Hadoop](https://hadoop-user-guide.web.cern.ch/gettingstarted_md.html)
    * [Using SPARK on Hadoop](https://hadoop-user-guide.web.cern.ch/spark/Using_Spark_on_Hadoop.html)
2. CERNBox
    * CERNBox is a place you can share your work projects. It is also required that you have your own CERNBox before using SWAN as it will be your SWAN home directory.
    * Access to CERNBox [here.](https://cernbox.web.cern.ch/cernbox/) 

### SWAN

SWAN (Service for Web based ANalysis) is a platform to perform interactive data analysis in the cloud. It uses your CERNBox as the home directory and you can access CERN experiments' and user data in CERN Cloud (EOS) there. [Read more about SWAN.](https://swan.web.cern.ch/swan/) 

Examples of how to use SWAN to do data analysis and visualization [here.](https://swan-gallery.web.cern.ch/basic/)

### PySpark on SWAN

PySpark is an interface for Apache Spark in Python. It not only allows you to write Spark applications using Python APIs, but also provides the PySpark shell for interactively analyzing your data in a distributed environment. PySpark supports most of Spark’s features such as Spark SQL, DataFrame, Streaming, MLlib (Machine Learning) and Spark Core. [Read more.](https://spark.apache.org/docs/latest/api/python/)

How-to:
1. Log in to SWAN directly from the [SWAN page](https://swan-k8s.cern.ch) or log in to your CERNBox then open SWAN Notebook from there.
2. Create a new project and a new file.
3. On the top panel, look for a *Star* button. It will appear there only if you already have the Hadoop cluster access. Configure needed library then click *connect*.


Note:
- The following variables are automatically initiated when connect to the Spark cluster:
    * sc = [SparkContext](https://spark.apache.org/docs/3.2.0/api/java/org/apache/spark/SparkContext.html#:~:text=A%20SparkContext%20represents%20the%20connection,before%20creating%20a%20new%20one.)
    * spark = [SparkSession](https://spark.apache.org/docs/3.2.0/api/java/org/apache/spark/sql/SparkSession.html)

### HDFS Starter

Learn more about CERN HDFS [here.](https://clouddocs.web.cern.ch/containers/tutorials/hdfs.html)

#### Connect via command line

1. Connect to [LXPLUS](#LXPLUS) using SSH. 
    * Machines running CentOS7 Linux 64 bit mode: @lxplus7.cern.ch 
    * Machines running CentOS8: @lxplus8.cern.ch 


```python
ssh [username]@lxplus7.cern.ch
```

2. configure as indicated in [here](https://hadoop-user-guide.web.cern.ch/getstart/client_cvmfs.html)


```python
#first time setup
source /cvmfs/sft.cern.ch/lcg/views/LCG_99/x86_64-centos7-gcc8-opt/setup.sh
#if use spark
source /cvmfs/sft.cern.ch/lcg/etc/hadoop-confext/hadoop-swan-setconf.sh analytix 3.2 spark3
```


```python
kinit
```

3. Explore the HDFS by looking up the path. [More path from CMS MONIT docs](https://cmsmonit-docs.web.cern.ch/MONIT/sources/)


```python
hdfs dfs -ls /
```

#### Connect via SWAN

After connecting to the cluster, you can explore HDFS directly from SWAN


```python
!hdfs dfs -ls /
```

#### Create your own directory

You can have your own directory in the HDFS. The example shows the directory in case pf working under CMS.


```python
!hdfs dfs -mkdir hdfs://analytix/cms/users/[username]
```

#### More commands

Read the HDFS commands full document [here.](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HDFSCommands.html)

1. Check size of the folder


```python
!hdfs dfs -du -s -h hdfs://[path]
```

2. Copy a file/ folder from HDFS to your EOS storage


```python
!hdfs dfs -cp  hdfs://[path] file:${PWD}/[path]
```

Note that the PWD specifies your current directory in the [EOS](#EOS) space. You can check it by running the command on SWAN.


```python
!$PWD
```

or


```python
import os
os.getcwd()
```
