# HDFS + YARN + Spark 1.3.x cluster + Apache Zeppelin
Apache Spark™ is a fast and general purpose engine for large-scale data processing.
Key features:
Apache Zeppelin (v 0.5.0 incubating) A web-based notebook that enables interactive
data analytics. You can make beautiful data-driven, interactive and collaborative 
documents with SQL, Scala and more.
**Speed:**
Run programs up to 100x faster than Hadoop MapReduce in memory, or 10x faster on disk.
Spark has an advanced DAG execution engine that supports cyclic data flow and in-memory computing.
**Ease of Use:**
Write applications quickly in Java, Scala or Python.
Spark offers over 80 high-level operators that make it easy to build parallel apps.
And you can use it interactively from the Scala and Python shells.
**General Purpose Engine:**
Combine SQL, streaming, and complex analytics.
Spark powers a stack of high-level tools including Shark for SQL, MLlib for 
machine learning, GraphX, and Spark Streaming. You can combine these frameworks 
seamlessly in the same application.
**Integrated with Cluster Managers: YARN**
Spark can run on Hadoop 2's YARN cluster manager, and can read any existing Hadoop data.

 
For more details <http://spark.apache.org/>
## Usage 
    from bundle's home directory:
    juju quickstart bundles.yaml

## Scale Out Usage

In order to increase the amount of spark slaves, you just add units, to add one 
unit to hadoop compute-slave nodes (current bundle has 3 compute-slave):
    juju add-unit -n4 compue-slave
    
## Smoke tests after deployment 
    # Spark admins use ssh to access spark console from master node
    1) juju ssh spark/0  <<= ssh to spark master
    2) Use spark-submit to run your application:
    spark-submit --class org.apache.spark.examples.SparkPi --deploy-mode cluster \
    --master yarn-client /usr/lib/spark/lib/spark-examples*.jar  10
    you should get pi = 3.14
    or execute demo.sh from /home/ubuntu
    
    3) Spark’s shell provides a simple way to learn the API, as well as a powerful 
    tool to analyze data interactively. It is available in either Scala or Python. 
    Start it by running the following in the Spark directory:
    $spark-shell <== for interaction using scala 
    $pyspark     <== for interaction using python
## Access Apache Zeppelin Web site
    from any web browser, load : http://{spark-node-ip}:8080
    note: use "juju status" command to discover spark node IP address
    
