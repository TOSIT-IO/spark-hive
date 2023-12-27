# TDP Spark Hive Notes

The version 1.2.1.spark2-1.0 of Apache Hive is based on the `release-1.2.1-spark2` branch of the [repository](https://github.com/JoshRosen/hive/tree/release-1.2.1-spark2).

**Note**: This is a repository that is only needed for the Spark Dependency. Apache Spark 2.x depends on version `org.spark-project.hive:1.2.1.spark2` which was a fork hosted on the Github of one of Spark's maintainers.

Hortonworks had their own version of Hive 1.x as a dependency to Spark: https://github.com/hortonworks/spark_hive2-release/tree/HDP-3.1.5.0-152-tag (link is now dead).

The only addition to Apache Hive 1.2 is the support of Hadoop 3 which removes the `Unrecognized Hadoop major version number`. See branch 2.X of TDP Spark repository for details.

## Building

```
mvn clean install -Phadoop-2 -Dgpg.skip -DskipTests
```

- -Phadoop-2: compile with Hadoop
- -Dgpg.skip: skip GPG signature to avoid setup GPG for compiling this project

## Test execution notes

Should we care about testing this Hive version ?

## Build notes

- HIVE-16081 : allow 0.23 shim creation for Hadoop 3 (Sergey Shelukhin, reviewed by Gunther Hagleitner)

Add a case to handle Hadoop 3 version which removes the `Unrecognized Hadoop major version number` for TDP Spark 2.

- fix(ql/pom.xml): exclude pentaho-aggdesigner-algorithm from the calcite dependency

pentaho-aggdesigner-algorithm is downloaded to compile because it is a calcite dependency and conjars repo is no longer available so it can't be downloaded (See HIVE-25173).
Moreover it is not packaged inside "hive-exec.jar" so we exclude it.
