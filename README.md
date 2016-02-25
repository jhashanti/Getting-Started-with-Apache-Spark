# Getting-Started-with-Apache-Spark
##Steps for running Spark on Windows:

Required files:
  1. jdk-8u73-windows-x64.exe from http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html
  2. scala.msi from http://www.scala-lang.org/download/2.10.6.html
  3. sbt-0.13.9.zip from http://get.jenv.mvnsearch.org/download/sbt/sbt-0.13.9.zip
  4. hadoop-2.6.0.zip from http://hadoop.apache.org/releases.html#Download
  5. spark-1.6.0-bin-hadoop2.6.zip http://spark.apache.org/downloads.html
  
Steps:  
  1. Install JDK 1.8.73 
  2. Install scala-2.10.6.msi  into D:\scala-2.10.6
  3. Install sbt 0.13.9 into D:\sbt-0.13.9 
  4. Extract hadoop-2.6.0.zip to D:\
  5. Extract spark-1.6.0-bin-hadoop2.6.zip to D:\
  6. Create new system environment variables for HADOOP_HOME, JAVA_HOME, SBT_HOME, SCALA_HOME, and SPARK_HOME
  
            HADOOP_HOME D:\hadoop-2.6.0
            JAVA_HOME C:\Program Files\Java\jdk1.8.0_73
            SBT_HOME D:\sbt-0.13.9
            SCALA_HOME D:\scala-2.10.6
            SPARK_HOME D:\spark-1.6.0-bin-hadoop2.6
  7. create the below directories
  
            D:\tmp\hive
  8. Open a command prompt and navigate to D:\ and run the below command
  
            D:\hadoop-2.6.0\bin\winutils.exe chmod 777 /tmp/hive
  9. Navigate to spark-shell as mentioned below
  
            cd D:\spark-1.6.0-bin-hadoop2.6\bin\spark-shell
  10. scala prompt can be seen, which means spark is running
  
##Steps for Hadoop2.6.0 installation on Ubuntu(Single Node Cluster)
  http://www.bogotobogo.com/Hadoop/BigData_hadoop_Install_on_ubuntu_single_node_cluster.php
  
##Steps for Apache Spark installation on Ubuntu 
  http://blog.prabeeshk.com/blog/2014/10/31/install-apache-spark-on-ubuntu-14-dot-04/
  

