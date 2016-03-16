# Getting-Started-with-Apache-Spark
###Steps for running Spark on Windows:

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
  
###Steps for Hadoop2.6.0 installation on Ubuntu(Single Node Cluster)
http://www.bogotobogo.com/Hadoop/BigData_hadoop_Install_on_ubuntu_single_node_cluster.php


###Steps for Apache Spark installation on Ubuntu
http://blog.prabeeshk.com/blog/2014/10/31/install-apache-spark-on-ubuntu-14-dot-04/
  

##Scala Basics:

Simple hello world example:

            object Test{
            	def main(args: Array[String]): Unit = {
            	println("hello, world !")
            	}
            }
            Test.main(Array())
            
            hello, world !
            
  If and else:
  
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
  Loops:
  
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
            
  Anonymous function:
  
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
 
  Recursive function: 
  
            def factorial(number:Int) : Int = {
              if (number == 1)
                 return 1
              number * factorial (number - 1)
            }
            println(factorial(5))
            
            120
  
  Tail recursion:
  
            def factorial(accumulator: Int, number: Int) : Int = {
              if(number == 1)
                return accumulator
              factorial(number * accumulator, number - 1)
            }
            println(factorial(1,5))
            
            120
            
  Nested function:
  
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
  
  Classes:
  
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
  
  Objects:
  
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
  
  Case class: 
  
            case class Employee(EmployeeName:String,EmployeeAge:Int)
            var e = Employee("XYZ",22)
            
  Pattern Matching:
  
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
  
  Collections:
  
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
  
  Higher Order functions:
  
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

###Spark Introduction: 
  [apache-spark-introduction](http://www.infoq.com/articles/apache-spark-introduction)


###Worked out examples using different Transformations & Actions

  word count:
  
             scala> var textFile = sc.textFile("../README.md")
             scala> textFile.count()
             res0: Long = 95
  creating a new RDD[Int]: 
  
             scala> var xtemp = sc.parallelize(Array(1,2,2,4))
###Transformations:

  * map: multiplying each element of RDD by 2
  
             scala> xtemp.map(x => (x*2))
             
  * filter: filter elements > 2
  
             scala> xtemp.filter(x => (x > 2))
  * flatMap:
  
             scala> var list = List(1,2,3)
             scala> def g(v:Int) = List(v-1, v, v+1)
             scala> list.flatMap(x => g(x))
             res1: List[Int] = List(0,1,2,1,2,3,2,3,4)
             scala> list.map(x => g(x))
             res2: List[List[Int]]] = List(List(0, 1, 2), List(1, 2, 3), List(2, 3, 4))
             scala> list.map(x => g(x)).flatten
             res3: List[Int] = List(0,1,2,1,2,3,2,3,4)
  * groupByKey:  
  
            scala> xtemp.map(x => (x,1)).groupByKey().map(y => (y._1,y._2.sum))
  * reduceByKey:
  
            scala> xtemp.map(x => (x,1)).reduceByKey(_+_)
  [Avoid using groupByKey](https://databricks.gitbooks.io/databricks-spark-knowledge-base/content/best_practices/prefer_reducebykey_over_groupbykey.html)
  * [mapPartitions & mapPartitionsWithIndex:](http://apachesparkbook.blogspot.in/2015/11/mappartition-example.html)
  * union:
  
            scala> var rdd1 = sc.parallelize(Array("a","a","b"))
            scala> var rdd2 = sc.parallelize(Array("c","a","e"))
            scala> rdd1.union(rdd2)
            Array[String] = Array(a,a,b,c,a,e)
  * intersection:
  
            scala> rdd1.intersection(rdd2)
            Array[String] = Array(a)
  * join:
  
            scala> var rdd1 = sc.parallelize(Array(1,2))
            scala> var rdd2 = sc.parallelize(Array(2,3))
            scala> rdd1.map(x => (x,1)).join(rdd2.map(y => (y,2)))
            res4: Array[(Int,(Int,Int))] = Array(2,(1,2))
  * cartesian:
  
            scala> rdd1.cartesian(rdd2)
            res5: Array[(Int,Int)] = Array((1,2),(1,3),(2,2),(2,3))
  * cogroup:
  
            scala> var rdd1 = sc.parallelize(Array((1,2),(2,3),(2,4)))
            scala> var rdd2 = sc.parallelize(Array((2,6),(2,9)))
            scala> rdd1.cogroup(rdd2)
            
  * sortByKey:
  
            scala> var rdd1 = sc.parallelize(Array((2,3),(1,2)))
            scala> rdd1.sortByKey()
            Array((1,2),(2,3))
  * [combineByKey](http://stackoverflow.com/questions/29246756/how-createcombiner-mergevalue-mergecombiner-works-in-combinebykey-in-spark-us):

            scala> val rdd = sc.parallelize(Array(("A", 1), ("B", 4), ("A", 2), ("B", 8), ("A", 3))) 
            scala> rdd.combineByKey(
                      (x:Int) => (x, 1),
                      (acc:(Int, Int), x) => (acc._1 + x, acc._2 + 1),
                      (acc1:(Int, Int), acc2:(Int, Int)) => (acc1._1 + acc2._1, acc1._2 + acc2._2))

  * [aggregateByKey:](http://codingjunkie.net/spark-agr-by-key/)
    
            scala> var keysWithValuesList = Array("foo=A", "foo=A", "foo=A", "foo=A", "foo=B", "bar=C", "bar=D", "bar=D")
            scala> var data = sc.parallelize(keysWithValuesList)
            scala> var kv = data.map(_.split("=")).map(x => (x._1,x._2)).cache()
            scala> var initialCount = 0;
            scala> var addToCounts = (n: Int, v: String) => n + 1
            scala> var sumPartitionCounts = (n1: Int, n2: Int) => n1 + n2
            scala> var countByKey = kv.aggregateByKey(initialCount)(addToCounts, sumPartitionCounts)
            scala> countByKey.collect
            res6: Array[(String, Int)] = Array((foo,5), (bar,3))

  * [pipe](http://blog.madhukaraphatak.com/pipe-in-spark/)
  * coalesce:
  
            scala> var rdd1 = sc.parallelize(1 to 10, 10)
            scala> var rdd2 = rdd1.coalesce(2, false)
            scala> rdd2.partitions.length
            res7: Int = 2
  * repartition
  
            scala> var rdd2 = rdd1.repartition(2)
            scala> rdd2.partitions.length
            res8: Int = 2

###Actions:
  
  * reduce:
  
            scala> xtemp.reduce(_+_)
            Int = 8
  * collect:
  
            scala> xtemp.collect
            res0: Array[Int] = Array(1,2,2,3)
  * count:
  
            scala> xtemp.count
            res9: Long = 4
  * take:
  
            scala> xtemp.take(2)
            res10: Array[Int] = Array(1,2)
  * takeSample:
  
            scala> xtemp.takeSample(true,2,13)
            res11: Array[Int] = Array(2,3)
  * takeOrdered:
  
            scala> xtemp.take(2)
            res12: Array[Int] = Array(1,2)
  * countByKey:
  
            scala> var keysWithValuesList = Array("foo=A", "foo=A", "foo=A", "foo=A", "foo=B", "bar=C", "bar=D", "bar=D")
            scala> var data = sc.parallelize(keysWithValuesList)
            scala> var kv = data.map(_.split("=")).map(x => (x._1,x._2)).cache()
            scala> kv.countByKey()
            res13: scala.collection.Map[String,Long] = Map(foo -> 5, bar -> 3)
  * forEach:
    
            scala> xtemp.foreach(x => println(x))
            2
            2
            1
            3
 
