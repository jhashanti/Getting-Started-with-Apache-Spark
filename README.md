
## Table of Contents

* [Installing & Setting Up Spark locally](#running-spark)
* [Scala Basics with examples](#scala-basics)
* [Apache Spark Introduction](#spark-intro)
  * [Resilient Distributed Datasets](#spark-rdd)
    * [Creating RDD](#spark-creating-rdd)
  * [Transformations](#spark-transformation)
    * [Worked out examples using Transformations](#spark-transformation-example)
  * [Actions](#spark-action)
    * [Worked out examples using Actions](#spark-action-example)
  * [Word Count example](#spark-word-count)
  * [Shared Variables](#spark-shared-variables)
    * [Broadcast Variables](#spark-shared-variables-broadcast)
    * [Accumulators](#spark-shared-variables-accumulators)
  * [Spark Streaming](#spark-streaming)
  * [SparkSQL](#spark-sql)
  * [MLlib](#spark-mllib)
  * [GraphX](#spark-graphx)
* [Published Papers](#spark-papers)
* [Blogs](#spark-blogs)
* [Books](#spark-books)
* [Videos](#spark-videos)
* [Use Cases](#spark-use-case)
* [Quora Resources](#spark-quora-resource)
* [Courses & Certifications](#spark-courses-certification)
* [Groups](#spark-groups)

###<a name="running-spark"></a>Installing & setting up spark locally

* [Windows](#running-spark-windows)
* [Ubuntu](#running-spark-ubuntu)

####<a name="running-spark-windows"></a>Steps for running Spark on Windows

* Required files:
    1. jdk-8u73-windows-x64.exe from http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html
    2. scala.msi from http://www.scala-lang.org/download/2.10.6.html
    3. sbt-0.13.9.zip from http://get.jenv.mvnsearch.org/download/sbt/sbt-0.13.9.zip
    4. hadoop-2.6.0.zip from http://hadoop.apache.org/releases.html#Download
    5. spark-1.6.0-bin-hadoop2.6.zip http://spark.apache.org/downloads.html
  
* Steps:  
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
  
####<a name="running-spark-ubuntu"></a>Steps for running Spark on Ubuntu

  * [Hadoop2.6.0 installation on Ubuntu(Single Node Cluster)](http://www.bogotobogo.com/Hadoop/BigData_hadoop_Install_on_ubuntu_single_node_cluster.php)
  * [Apache Spark installation on Ubuntu](http://blog.prabeeshk.com/blog/2014/10/31/install-apache-spark-on-ubuntu-14-dot-04/)
  

###<a name="scala-basics"></a>Scala Basics

  * [Simple Hello world example](#scala-hello-world)
  * [Class](#scala-classes)
  * [Object](#scala-objects)
  * [If Else](#scala-if-else)
  * [Loops](#scala-loops)
  * [Anonymous Function](#scala-anonymous-function)
  * [Recursive Function](#scala-recursive-function)
  * [Tail Recursion](#scala-tail-recursion)
  * [Nested Function](#scala-nested-function)
  * [Case Class](#scala-case-class)
  * [Pattern Matching](#scala-pattern-matching)
  * [Collections](#scala-collections)
  * [Higher Order Function](#scala-high-order-function)
  
<a name="scala-hello-world"></a>Simple hello world example:

            object Test{
            	def main(args: Array[String]): Unit = {
            	println("hello, world !")
            	}
            }
            Test.main(Array())
            
            hello, world !
            
 <a name="scala-if-else"></a>If and else:
  
            object Test{
            	def main(args: Array[String]): Unit = {
            	var x = 30
            	if(x > 20)
            	println("Greater than 20")
            	else
            	println("Less than 20")
            	}
            }
            Test.main(Array())
            
            Greater than 20
  <a name="scala-loops"></a>Loops:
  
            object Test{
            	def main(args: Array[String]): Unit = {
            	var x = 30;
            		for( a<- 1 to 5 by 2)
            		{
            			println(a)
            		}
            	}
            }
            Test.main(Array())
            
            1
            3
            5
            
 <a name="scala-anonymous-function"></a>Anonymous function:
  
            var add = (a:Int,b:Int) => a+b
            println(add(1,2))
            
            3
            
  Calling functions from other function:
  
            object Test{
              def main(args: Array[String]): Unit = {
              println(sumOfCube(2,3))
              }
              def cube(x:Int):Int = (x*x*x)
              def sumOfCube(a:Int,b:Int):Int ={
              cube(a) + cube(b)
              }
            }
            Test.main(Array())
            
            35
 
  <a name="scala-recursive-function"></a>Recursive function: 
  
            def factorial(number:Int) : Int = {
              if (number == 1)
                 return 1
              number * factorial (number - 1)
            }
            println(factorial(5))
            
            120
  
  <a name="scala-tail-recursion"></a>Tail recursion:
  
            def factorial(accumulator: Int, number: Int) : Int = {
              if(number == 1)
                return accumulator
              factorial(number * accumulator, number - 1)
            }
            println(factorial(1,5))
            
            120
            
  <a name="scala-nested-function"></a>Nested function:
  
            def factorial(i : Int): Int = {
              def fact(i : Int, accumulator:Int):Int = {
              if(i<=1)
                accumulator
              else
                fact(i -1, i*accumulator)
              }
              fact(i,1)
            }
            println(factorial(5))
            
            120
  
  <a name="scala-classes"></a>Classes:
  
            class Point(xc:Int,yc:Int){
              var x:Int = xc
              var y:Int =yc
              def move(dx:Int,dy:Int){
                x = x+dx
                y = y+dy
                println(x)
                println(y)
              }
            }
            var a = new point(2,3)
            a.move(2,3) 
            
            4
            6
  
  <a name="scala-objects"></a>Objects:
  
            object Test{
              def main(args: Array[String]){
                val point = new Point(10,20)
                printPoint
                def printPoint{
                  println(point.x);
                  println(point.y);
                }
              }
            }
            Test.main(Array())
            
            10
            20
  
  <a name="scala-case-class"></a>Case class: 
  
            case class Employee(EmployeeName:String,EmployeeAge:Int)
            var e = Employee("XYZ",22)
            
 <a name="scala-pattern-matching"></a> Pattern Matching:
  
            object Test{
              def main(args: Array[String]){
                println(matchTest(3))
              }
              def matchTest(x:Int):String = x match{
                case 1 => "one"
                case 2 => "two"
                case _ => "many"
              }
            }
            Test.main(Array())
            
            many
  
  <a name="scala-collections"></a>Collections:
  
    Some commonly used collections
    List:
              sacla> var l = List(1,2,3)
              scala> l.map(_ + 1) //calling map function on each element of the List
              res0: List[Int] = List(2,3,4)
              
    Sequence:
              sacla> var s = seq(1,1,2)
              res0: Seq[Int] = List(1,1,2)
    Set: 
              sacla> var s = Set(1,1,2)
              res0: scala.collection.immutable.Set[Int] = Set(1,2)
    Map:
              sacla> var m = Map("x" -> 24, "y" -> 25, "z" -> 26)
              sacla> m.map(x => x._1) //calling map function on each element of the Map
              res0:  scala.collection.immutable.Iterable[String] =List(x,y,z)
              
    Array:
              scala> var a = Array(1,2,3)
              a: Array[Int] = Array(1,2,3)
    Range:
              1 to 3
              Range(1,2,3)
              
              1 to 10 by 2
              Range(1,3,5,7,9)
              
              1 until 3
              Range(1,2)
              
    Iterator:
              var it = Iterator("a","b","c")
              while(it.hasNext){
                println(it.next)
              }
              
              a
              b
              c
  
 <a name="scala-high-order-function"></a>Higher Order functions:
  
              class Decorator(left: String, right: String) {
                def layout[A] (x: A) = left + x.toString() + right
              }

              object Test{
                def main(args:Array[String]){
                  val decorator = new Decorator("[", "]")
                  println(apply(decorator.layout, 7))
                }
                def apply(f: Int => String, v: Int) = f(v)
              }
              Test.main(Array())
              
              [7]

###<a name="spark-intro"></a>Apache Spark Introduction

 * [Introduction](http://www.infoq.com/articles/apache-spark-introduction)
 * [Spark Summit: Deeper understanding of Spark Internals](https://spark-summit.org/2014/wp-content/uploads/2014/07/A-Deeper-Understanding-of-Spark-Internals-Aaron-Davidson.pdf)

####<a name="spark-rdd"></a>Resilient Distributed Datasets

#####<a name="spark-creating-rdd">creating RDD
    
               scala> var xtemp = sc.parallelize(Array(1,2,2,4))
               scala> var textFile = sc.textFile("../README.md")

####<a name="spark-transformation"></a>Transformations

#####<a name="spark-transformation-example"></a>Worked out examples using transformations
  
  * [map](#spark-transformation-map)
  * [filter](#spark-transformation-filter)
  * [flatMap](#spark-transformation-flatmap)
  * [groupByKey](#spark-transformation-groupbykey)
  * [reduceByKey](#spark-transformation-reducebykey)
  * [mapPartition & mapPartitionWithIndex](#spark-transformation-mappartion-mappartitionswithindex)
  * [union](#spark-transformation-union)
  * [intersection](#spark-transformation-intersection)
  * [join](#spark-transformation-join)
  * [cartesian](#spark-transformation-cartesian)
  * [cogroup](#spark-transformation-cogroup)
  * [sortByKey](#spark-transformation-sortbykey)
  * [combineByKey](#spark-transformation-combinebykey)
  * [pipe](#spark-transformation-pipe)
  * [aggregateByKey](#spark-transformation-aggregatebykey)
  * [coalesce](#spark-transformation-coalesce)
  * [repartition](#spark-transformation-repartition)

    <a name="spark-transformation-map"></a> map 
    multiplying each element of RDD by 2
    
               scala> xtemp.map(x => (x*2))
               
    <a name="spark-transformation-filter"></a>filter
    filter elements > 2
    
               scala> xtemp.filter(x => (x > 2))
    <a name="spark-transformation-flatmap"></a> flatMap
    
               scala> var list = List(1,2,3)
               scala> def g(v:Int) = List(v-1, v, v+1)
               scala> list.flatMap(x => g(x))
               res1: List[Int] = List(0,1,2,1,2,3,2,3,4)
               scala> list.map(x => g(x))
               res2: List[List[Int]]] = List(List(0, 1, 2), List(1, 2, 3), List(2, 3, 4))
               scala> list.map(x => g(x)).flatten
               res3: List[Int] = List(0,1,2,1,2,3,2,3,4)
    <a name="spark-transformation-groupbykey"></a>groupByKey 
    
              scala> xtemp.map(x => (x,1)).groupByKey().map(y => (y._1,y._2.sum))
    <a name="spark-transformation-reducebykey"></a>reduceByKey
    
              scala> xtemp.map(x => (x,1)).reduceByKey(_+_)
    [Avoid using groupByKey](https://databricks.gitbooks.io/databricks-spark-knowledge-base/content/best_practices/prefer_reducebykey_over_groupbykey.html)
    <a name="spark-transformation-mappartion-mappartitionswithindex"><a/>[mapPartitions & mapPartitionsWithIndex](http://apachesparkbook.blogspot.in/2015/11/mappartition-example.html)
    
    <a name="spark-transformation-union"></a>union
    
              scala> var rdd1 = sc.parallelize(Array("a","a","b"))
              scala> var rdd2 = sc.parallelize(Array("c","a","e"))
              scala> rdd1.union(rdd2)
              Array[String] = Array(a,a,b,c,a,e)
    <a name="spark-transformation-intersection"></a>intersection
    
              scala> rdd1.intersection(rdd2)
              Array[String] = Array(a)
    <a name="spark-transformation-join"></a>join
    
              scala> var rdd1 = sc.parallelize(Array(1,2))
              scala> var rdd2 = sc.parallelize(Array(2,3))
              scala> rdd1.map(x => (x,1)).join(rdd2.map(y => (y,2)))
              res4: Array[(Int,(Int,Int))] = Array(2,(1,2))
    <a name="spark-transformation-cartesian"></a>cartesian
    
              scala> rdd1.cartesian(rdd2)
              res5: Array[(Int,Int)] = Array((1,2),(1,3),(2,2),(2,3))
    <a name="spark-transformation-cogroup"></a>cogroup
    
              scala> var rdd1 = sc.parallelize(Array((1,2),(2,3),(2,4)))
              scala> var rdd2 = sc.parallelize(Array((2,6),(2,9)))
              scala> rdd1.cogroup(rdd2)
              
    <a name="spark-transformation-sortbykey"></a>sortByKey
    
              scala> var rdd1 = sc.parallelize(Array((2,3),(1,2)))
              scala> rdd1.sortByKey()
              Array((1,2),(2,3))
    <a name="spark-transformation-combinebykey"></a>[combineByKey](http://stackoverflow.com/questions/29246756/how-createcombiner-mergevalue-mergecombiner-works-in-combinebykey-in-spark-us)
      
              scala> val rdd = sc.parallelize(Array(("A", 1), ("B", 4), ("A", 2), ("B", 8), ("A", 3))) 
              scala> rdd.combineByKey(
                        (x:Int) => (x, 1),
                        (acc:(Int, Int), x) => (acc._1 + x, acc._2 + 1),
                        (acc1:(Int, Int), acc2:(Int, Int)) => (acc1._1 + acc2._1, acc1._2 + acc2._2))
  
    <a name="spark-transformation-aggregatebykey"></a>[aggregateByKey](http://codingjunkie.net/spark-agr-by-key/)
      
              scala> var keysWithValuesList = Array("foo=A", "foo=A", "foo=A", "foo=A", "foo=B", "bar=C", "bar=D", "bar=D")
              scala> var data = sc.parallelize(keysWithValuesList)
              scala> var kv = data.map(_.split("=")).map(x => (x._1,x._2)).cache()
              scala> var initialCount = 0;
              scala> var addToCounts = (n: Int, v: String) => n + 1
              scala> var sumPartitionCounts = (n1: Int, n2: Int) => n1 + n2
              scala> var countByKey = kv.aggregateByKey(initialCount)(addToCounts, sumPartitionCounts)
              scala> countByKey.collect
              res6: Array[(String, Int)] = Array((foo,5), (bar,3))
  
    <a name="spark-transformation-pipe"></a>[pipe](http://blog.madhukaraphatak.com/pipe-in-spark/)
      
    <a name="spark-transformation-coalesce"></a>coalesce
    
              scala> var rdd1 = sc.parallelize(1 to 10, 10)
              scala> var rdd2 = rdd1.coalesce(2, false)
              scala> rdd2.partitions.length
              res7: Int = 2
    <a name="spark-transformation-repartition"></a>repartition
    
              scala> var rdd2 = rdd1.repartition(2)
              scala> rdd2.partitions.length
              res8: Int = 2
  
####<a name="spark-action"></a>Actions

#####<a name="spark-action-example"></a>Worked out examples using Actions
 
  * [reduce](#spark-action-reduce)
  * [collect](#spark-action-collect)
  * [count](#spark-action-collect)
  * [take](#spark-action-take)
  * [takeSample](#spark-action-takesample)
  * [takeOrdered](#spark-action-takeordered)
  * [countByKey](#spark-action-countbykey)
  * [foreach](#spark-action-foreach)
  
    <a name="spark-action-reduce"></a>reduce
      
                scala> xtemp.reduce(_+_)
                Int = 8
    <a name="spark-action-collect"></a>collect
      
                scala> xtemp.collect
                res0: Array[Int] = Array(1,2,2,3)
    <a name="spark-action-count"></a>count
      
                scala> xtemp.count
                res9: Long = 4
    <a name="spark-action-take"></a>take
      
                scala> xtemp.take(2)
                res10: Array[Int] = Array(1,2)
    <a name="spark-action-takesample"></a>takeSample
      
                scala> xtemp.takeSample(true,2,13)
                res11: Array[Int] = Array(2,3)
    <a name="spark-action-takeordered"></a>takeOrdered
      
                scala> xtemp.take(2)
                res12: Array[Int] = Array(1,2)
    <a name="spark-action-countbykey"></a>countByKey
      
                scala> var keysWithValuesList = Array("foo=A", "foo=A", "foo=A", "foo=A", "foo=B", "bar=C", "bar=D", "bar=D")
                scala> var data = sc.parallelize(keysWithValuesList)
                scala> var kv = data.map(_.split("=")).map(x => (x._1,x._2)).cache()
                scala> kv.countByKey()
                res13: scala.collection.Map[String,Long] = Map(foo -> 5, bar -> 3)
    <a name="spark-action-foreach"></a>foreach
        
                scala> xtemp.foreach(x => println(x))
                2
                2
                1
                3

####<a name="spark-word-count"></a> word count
  
             scala> var textFile = sc.textFile("../README.md")
             scala> textFile.count()
             res0: Long = 95
             

####<a name="spark-shared-variables"></a>Shared Variables

  * #####<a name="spark-shared-variables-broadcast"></a>Broadcast Variables
    * [what are broadcast variables?](http://www.sparktutorials.net/spark-broadcast-variables---what-are-they-and-how-do-i-use-them)
  
  * #####<a name="spark-shared-variables-accumulators"></a>Accumulators
    * [What it is?](http://www.infoobjects.com/spark-accumulators/)
    * [when to use?](http://stackoverflow.com/questions/29494452/when-are-accumulators-truly-reliable)

####<a name="spark-streaming"></a>Spark Streaming

   * [Spark Streaming:what is it?](http://www.datanami.com/2015/11/30/spark-streaming-what-is-it-and-whos-using-it/)
   * [Guide to Apache Spark Streaming](https://opensource.com/business/15/4/guide-to-apache-spark-streaming)

####<a name="spark-sql"></a>SparkSQL

   * [SparkSQL and DataFrames](http://www.infoq.com/articles/apache-spark-sql)

####<a name="spark-mllib"></a>MLlib

   * [MLlib](http://stanford.edu/~rezab/sparkworkshop/slides/xiangrui.pdf)

####<a name="spark-graphx"></a>GraphX

   * [GraphX](http://ampcamp.berkeley.edu/big-data-mini-course/graph-analytics-with-graphx.html)
   
 
###<a name="spark-papers"></a>Papers
 
 * [Spark SQL: Relational Data Processing in Spark.](http://people.csail.mit.edu/matei/papers/2015/sigmod_spark_sql.pdf)Michael Armbrust, Reynold S. Xin, Cheng Lian, Yin Huai, Davies Liu, Joseph K. Bradley, Xiangrui Meng, Tomer Kaftan, Michael J. Franklin, Ali Ghodsi, Matei Zaharia. SIGMOD 2015. June 2015
 * [GraphX: Unifying Data-Parallel and Graph-Parallel Analytics.](https://amplab.cs.berkeley.edu/wp-content/uploads/2014/02/graphx.pdf)Reynold S. Xin, Daniel Crankshaw, Ankur Dave, Joseph E. Gonzalez, Michael J. Franklin, Ion Stoica. OSDI 2014. October 2014.
 * [Discretized Streams: Fault-Tolerant Streaming Computation at Scale.](http://people.csail.mit.edu/matei/papers/2013/sosp_spark_streaming.pdf)Matei Zaharia, Tathagata Das, Haoyuan Li, Timothy Hunter, Scott Shenker, Ion Stoica. SOSP 2013. November 2013.
 * [Shark: SQL and Rich Analytics at Scale.](http://people.csail.mit.edu/matei/papers/2013/sigmod_shark.pdf)Reynold S. Xin, Joshua Rosen, Matei Zaharia, Michael J. Franklin, Scott Shenker, Ion Stoica. SIGMOD 2013. June 2013.
 * [Discretized Streams: An Efficient and Fault-Tolerant Model for Stream Processing on Large Clusters.](http://people.csail.mit.edu/matei/papers/2012/hotcloud_spark_streaming.pdf)Matei Zaharia, Tathagata Das, Haoyuan Li, Scott Shenker, Ion Stoica. HotCloud 2012. June 2012
 * [Shark: Fast Data Analysis Using Coarse-grained Distributed Memory (demo).](http://people.csail.mit.edu/matei/papers/2012/sigmod_shark_demo.pdf)Cliff Engle, Antonio Lupher, Reynold S. Xin, Matei Zaharia, Haoyuan Li, Scott Shenker, Ion Stoica. SIGMOD 2012. May 2012
 * [Resilient Distributed Datasets: A Fault-Tolerant Abstraction for In-Memory Cluster Computing.](http://people.csail.mit.edu/matei/papers/2012/nsdi_spark.pdf)Matei Zaharia, Mosharaf Chowdhury, Tathagata Das, Ankur Dave, Justin Ma, Murphy McCauley, Michael J. Franklin, Scott Shenker, Ion Stoica. NSDI 2012. April 2012
 * [Spark: Cluster Computing with Working Sets.](http://people.csail.mit.edu/matei/papers/2010/hotcloud_spark.pdf)Matei Zaharia, Mosharaf Chowdhury, Michael J. Franklin, Scott Shenker, Ion Stoica. HotCloud 2010. June 2010
  
###<a name="spark-blogs"></a>Blogs:

 * [why apache spark is a crossover hit for data scientists | Cloudera](http://blog.cloudera.com/blog/2014/03/why-apache-spark-is-a-crossover-hit-for-data-scientists/)
 * [DeepSpark | Databricks](https://databricks.com/blog/2016/04/01/unreasonable-effectiveness-of-deep-learning-on-spark.html)
 * [Apache Spark Machine Learning Tutorial | MapR](https://www.mapr.com/blog/apache-spark-machine-learning-tutorial)
 * [Top Apache Spark Interview Questions | Edureka](http://www.edureka.co/blog/top-apache-spark-interview-questions-you-should-prepare-for-in-2016?utm_source=quora&utm_medium=crosspost&utm_campaign=social-media-edureka)
 * [Interview questions | Intellipaat](https://intellipaat.com/interview-question/apache-spark-interview-questions/)
 * [Spark Accumulators, what are they good for?](http://imranrashid.com/posts/Spark-Accumulators/)
 
###<a name="spark-books"></a>Books

* [Machine Learning with Spark](https://www.packtpub.com/big-data-and-business-intelligence/machine-learning-spark)
* [Fast Data Processing with Spark](https://www.packtpub.com/big-data-and-business-intelligence/fast-data-processing-spark)
* [Mastering Apache Spark](https://www.gitbook.com/book/jaceklaskowski/mastering-apache-spark/details)
* [Advanced Analytics with Spark](http://shop.oreilly.com/product/0636920035091.do)
* [Databricks Spark Reference Applications](https://www.gitbook.com/book/databricks/databricks-spark-reference-applications/details)
 
###<a name="spark-videos"></a>Videos

 * [Apache Spark | YouTube](https://www.youtube.com/user/TheApacheSpark)
 
###<a name="spark-use-case"></a>Use Case

 * [Predicting Telecom churn with Spark | Cloudera](https://blog.cloudera.com/blog/2016/02/how-to-predict-telco-churn-with-apache-spark-mllib/)
  
###<a name="spark-quora-resource"></a>Quora Resources

 * [What exactly is Apache Spark and how does it work](https://www.quora.com/What-exactly-is-Apache-Spark-and-how-does-it-work)
 * [Difference between Spark & Hadoop Map Reduce](https://www.quora.com/What-is-the-difference-between-Apache-Spark-and-Apache-Hadoop-Map-Reduce)

###<a name="spark-courses-certification"></a>Courses & Certifications

* [Introduction to Big Data with Apache Spark](https://courses.edx.org/courses/BerkeleyX/CS100.1x/1T2015/info) 
* [Scalable Machine Learning](https://courses.edx.org/courses/BerkeleyX/CS190.1x/1T2015/info)
* [Big Data mini course | AMP Camp Berkeley](http://ampcamp.berkeley.edu/big-data-mini-course-home/)
* [Apache Spark Scala Certification Training | SimpliLearn](http://www.simplilearn.com/big-data-and-analytics/apache-spark-scala-certification-training)


###<a name="spark-groups"></a>Groups

* [Spark Meetup](http://www.meetup.com/topics/spark/)
