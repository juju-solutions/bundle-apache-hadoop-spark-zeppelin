# Apache Hadoop with Spark and Zeppelin

This bundle is a 6 node cluster designed to scale out. Built around Apache
Hadoop components, it contains the following units:

  * 1 NameNode (HDFS)
  * 1 ResourceManager (YARN)
  * 3 Slaves (DataNode and NodeManager)
  * 1 Spark
    - 1 Plugin (colocated on the Spark unit)
    - 1 Zeppelin (colocated on the Spark unit)


## Usage

Deploy this bundle using juju-quickstart:

    juju quickstart apache-hadoop-spark-zeppelin

See `juju quickstart --help` for deployment options, including machine
constraints and how to deploy a locally modified version of `bundle.yaml`.


### Verify the deployment

The services provide extended status reporting to indicate when they are ready:

    juju status --format=tabular

This is particularly useful when combined with `watch` to track the on-going
progress of the deployment:

    watch -n 0.5 juju status --format=tabular

The charm for each core component (namenode, resourcemanager, spark, zeppelin)
also each provide a `smoke-test` action that can be used to verify that each
component is functioning as expected.  You can run them all and then watch the
action status list:

    juju action do namenode/0 smoke-test
    juju action do resourcemanager/0 smoke-test
    juju action do spark/0 smoke-test
    juju action do zeppelin/0 smoke-test
    watch -n 0.5 juju action status

Eventually, all of the actions should settle to `status: completed`.  If
any go instead to `status: failed` then it means that component is not working
as expected.  You can get more information about that component's smoke test:

    juju action fetch <action-id>


### Access the Zeppelin web interface

To access the Apache Zeppelin web interface, first expose the Zeppelin service:

    juju expose zeppelin

The web interface is available at the following location (find
*spark_unit_ip_address* with `juju status spark/0 | grep public-address`):

    http://{spark_unit_ip_address}:9090


### Scale out

This bundle was designed to scale out. To increase the amount of
slaves, you can add units to the slave service. To add one unit:

    juju add-unit slave

Or you can add multiple units at once:

    juju add-unit -n4 slave


## Contact Information

- <bigdata@lists.ubuntu.com>


## Help

- [Juju mailing list](https://lists.ubuntu.com/mailman/listinfo/juju)
- [Juju community](https://jujucharms.com/community)
