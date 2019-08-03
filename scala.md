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
### List

## Objects
