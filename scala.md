## Scala
1. [Scala 是一门怎样的语言，具有哪些优缺点？ - 紫杉的回答 - 知乎](https://www.zhihu.com/question/19748408/answer/62527490)
* python: 每个人都能使用的语言，但对于追求速度和效率的程序员来说就是噩梦。有限的数据结构（4个:List, Tuples, Dictionary, Sets）, 不能查看时间复杂度的调用方法。提高速度的方法：numpy/scipy，利用Cython将python编译为c++再利用CModule读回python环境的编译器，性能提升不少，但还是很慢。
* Java：第一个提供模块化的语言，使得企业化很方便。接口和虚拟类定义后，换谁（新手或明星程序员）都可以上。Java属于B&D捆绑和束缚类型的语言，因为新手和明星程序员不会像c++那样写出上百倍耗时差距的代码。进而带出Java的缺点之一 不易优化。需要对JVM进行优化，实际上增大了难度。
* Scala: 提供一整套工具(mutable, immutable, parallel数据结构)，让程序员自由选择合适的数据结构，并对其算法层面的特殊优化。Scala相对于Java的优势，相信程序员的优化能力。例如foreach是高度优化的，zipWithIndex实际上是两层循环最好该用Vector().indicies.foreach()或用.view来推迟执行
* Scala很有前途的语言：有一个社区专注于追求运行速度。例如利用miniboxing使得原生数据类型不必自动拆装箱。Scala没有传统意义的for 循环，利用宏来实现它叫做cfor速度超快。 Scala追求速度，可以看成JVM上的C++。 目前twitter 后台语言使用Scala
## install
1. Scala is unusual because it is usually installed for each of your Scala projects rather than being installed system-wide. 
Both of the above options manage (via sbt) a specific Scala version per Scala project you create.
2. Check if java is installed by "java -version"
3. [install scala in Intellij](https://www.scala-lang.org/download/)
  * build a minimal Scala project using [Intellij with the Scala plugin](https://docs.scala-lang.org/getting-started/intellij-track/getting-started-with-scala-in-intellij.html)
  * build a Scala project with [Intellij and SBT](https://docs.scala-lang.org/getting-started/intellij-track/building-a-scala-project-with-intellij-and-sbt.html)
  * sbt is a popular tool for compiling, running, and testing Scala projects of any size. 
Using a build tool such as sbt (or Maven/Gradle) becomes essential once you create projects with dependencies or more than one code
4. [Intellij module](https://www.jetbrains.com/help/idea/creating-and-managing-modules.html)
  * Module is an essential part of any project – it's created automatically together with a project.
  * Modules consist of a content root and a module file. 
    * A content root is a folder where you store your code. Usually, it contains subfolders for source code, unit tests, resource files, and so on. 
    * A module file (the .iml file) is used for keeping module configuration, including content or source roots, dependencies, framework-specific settings in facets, and so on.
## Basics
### type inference
### variables
### for loops
### Operators
### functions
### read from console in Scala
### exceptions
### Pattern matching

## More Basics
### Set
1. [scala.collection.immutable.Set API](https://www.scala-lang.org/api/2.12.1/scala/collection/immutable/Set.html)
2. common api: intersection, difference, add an element, remove an element, head, tail, isEmpty, contains, zipWithIndex
3. practise
```scala
object SetExample {
  def main(args: Array[String]): Unit = {
    val fruit = Set("apple", "orange", "banana")
    var moreFruit = Set("kiwi", "pineapple")
    var nums = Set(1, 2, 3, 4, 5)
    var moreNums = Set(6, 7, 8, 9)
    println(nums.contains(5))
    println(nums(3))
    var mixed = fruit ++ nums
    println(mixed)
    nums -= 5
    println(nums)
    println(nums & moreNums)
    println(moreFruit.head)
    println(moreFruit.tail)
    println(moreNums.isEmpty)
  }
}
```
### Map
1. [scala.collection.immutable.Map API](https://www.scala-lang.org/api/2.12.1/scala/collection/Map.html)
2. common api: get(), filter(), flatMap(),groupBy(), foreach(), zipWithIndex
3. practise
```scala
object MapExample {
  def main(args: Array[String]): Unit = {
    // initialization
    var groceries = Map(1 -> "milk", 2 -> "bread", 3 -> "juice", 4 ->"eggs")
    //add one pair to this map, return a new map
    groceries = groceries + (5 -> "fruit")
    //remove a key from this map, return a new map
    groceries = groceries - 2
    // retrieve
    println(groceries.get(3))
    println(groceries(3))
    println(groceries.getOrElse(6, "No Match"))
    //iterate
    for(v <- groceries.values) println(v)
    for(k <- groceries.keys) println(k)
    groceries.foreach(println)
    // swap k, v
    var z = for((k, v) <- groceries) yield (v,k)

  }
}
```
### Array
1. [scala.Array](https://www.scala-lang.org/api/current/scala/Array.html). The downside of an array is that it must be set to a fixed size. 
2. practise
```scala
object ArrayExample {
  def main(args: Array[String]): Unit = {
    // When type is Any, default value is null
    var nums = new Array[Any](5)
    // initialize
    var furniture = Array("chair", "tv", "table")
    // access by index
    println(furniture(0))
    // replace the 2nd element
    furniture(1) = "sofa"
    // iterate
    for( f<- furniture) println(f)

    var arr = Array(1,2,3,4,5,6)
    // initialize by another array
    var rs = for(n <- arr) yield 2*n
    var even = for(n <- arr if n%2 == 0) yield  n
    for(e <- even) println(e)
  }
}
```
### List

## Objects
