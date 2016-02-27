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
  
  Higher Order functionS:
  
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
