# Creational Patterns
Here are my learning notes of Java Design Patterns: Creational on lynda
## Chapter 1: Creational Design Pattern
1. design pattern
* What: a way of structuring code to solve a specific problem.   
      a guideline or template on how to solve a commonly occurring problem.
      a design pattern allows you to reuse other people's knowledge
* Goal: to make code more elegant and flexible
* Challenge: knowing how to use the right design pattern in the right situation
2. creational design pattern 
* What: abstract the process of instantiating objects
* When: a system should not be dependent on how objects are created.
* How:
  * encapsulate knowledge about which concrete class the system should use
  * conceal how objects are created and put together.

## Chapter 2: Builder Pattern 
1. Why?   
* Avoid complex constructors
* Using Builder pattern makes object construction more **flexible**
* The builder pattern normally uses an **interface to define an abstract builder**
* The builder pattern can be used to **simplify adding objects to collections**
2. When?  Sometimes not all info is needed
3. How?
* first use telescoping constructor pattern(constructors with different combinations of parameters), but it is also too complex. Eg. the number of constructors with 8 parameters can be 2^8 -1. Code becomes very long.
* builder pattern is a better alternative. 
      * It keeps all the flexibility of the telescoping approach but without complexity. It moves the construction of complex objects out of the constructor. It also allows for different combinations of fields with one single construction process. 
      * Improve scalability

## Chapter 3: Singleton Pattern
1. Why?
Limit instances of a class to one. 
2. When? to create multiple instances of a class while still making sure that there is a way to access that one instance. 
## Chapter 4: Prototype Pattern 
## Chapter 5: Factory Method Pattern
## Chapter 6: Abstract Factories

# Structure Patterns
## Adapter
## Facade

# Behavior Patterns
## Observer 
1. what?  
* It's also known as Publish-Subscribe(Pub-Sub) Pattern. It defines one-to-many relationship between objects such as if one object is modified, its depenedent objects are to be notified automatically.  
* key objects: subject, observer. A subject might have many observers.
2. Why?  
* decouple, main consistance between related objects, increase the reusability 
* eg1: one application data object class; 3 presentation classes: spreedsheet object, char object and pie object
* eg2: 1 data object; 3 presentation classes: BinaryObserver, OctalObserver, HexaObserver
3. [Example Implements](https://www.tutorialspoint.com/design_pattern/observer_pattern.htm)

# Reference
1. https://www.tutorialspoint.com/design_pattern/observer_pattern.htm 
2. Design Patterns: Elements of Reusable Object-Oriented Software
3. Head First Design Patterns 
