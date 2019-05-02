---
layout: post
title:  "Kotlin for Java and Android Developers — 1"
author: atul
categories: [ technology, mobile development ]
image: assets/images/2019-05-02-Kotlin-for-java-and-android-developers-1-1.png
featured: true
hidden: false
---

If you are an Android developer and writing Java code for a long time, it is easier to learn Kotlin. Google has announced official support for Kotlin. Kotlin can do all that Java can do. 

We will start from basics so that you can start coding in Kotlin after reading this blog. We will cover classes , functions, inheritance, constructor, interface and access modifiers in this blog.

###function

```
fun main(args: Array<String>) {
    println("Hello, world!")
}
```

In Kotlin we can declare a function using fun keyword. Unlike java, in kotlin function can be declared outside the class also.

The parameter type is written after its name. For example:

**args: Array<String>**

Semicolon is optional at the end of the statement.

```
fun max(a: Int, b: Int): Int {
            return if (a > b) a else b
}
```

Return type of function is defined after the parameters.

###Statements and expressions

An expression has a value. It can be used in another expression. A statement is always a top-level element in its enclosing block. It does not have its own value. All control structures are statements in Java. But in Kotlin, other than the loops (for, do, and do/ while) most control structures are expressions.

```
fun max(x: Int, y: Int): Int = if (x > y) x else y
```

We can omitt the return type for functions with an expression body.

```
fun max(x: Int, y: Int) = if (x > y) x else y
```

###Variables

Unlike Java, while declaring variable, there is no need to specify its type. Kotlin, allow us to omit the types from variable declarations.

```
val x = 42
val x : Int = 42
```

###Mutable and Immutable variables

There are two keywords to declare a variable:

val — Immutable variable declaration. If a variable is declared with val we can’t be reassigned a new value after it is initialised. It is equivalent to a final variable in Java.

var — Mutable variable declaration. We can change the value of such a variables.

```
val x: Int
if (checkSomeCondition()) {
 x = 10
}
else {
 x = 90
}
```

###String templates

In the code, you declare a variable name and then use it in the following string literal

```
// Kotlin implementation
val name = "Kotlin"
println("Hello, $name!")
// Java implementation
String name = "java";
System.out.println("Hello, "+name+"!");
```

###Classes and properties

```
/* Java */
public class Student {
  private final String name;
  public Student(String name) {
                this.name = name;
  }
  public String getName() {
                return name;
  } 
}
```

In Java, Inside constructor body we usually assigns the parameters to the corresponding fields declared in the class. In Kotlin, this logic can be expressed without writing any code for that.

```
/* Kotlin */
class Student(val name: String)
```

This type of classes containing only data but no code are known as value objects. In Kotlin, public is the default modifier on class.

Let’s define properties in class

```
class Student(
    val name: String,
    var isMarried: Boolean
)
```

Kotlin provide getter and setter methods for var and for val only getter method is available.

```
val student = Student("Abhinandan", true)
println(student.name)
println(student.isMarried)
```

**new** is not used in creating object. When we access the property directly, its getter is invoked. If the property name starts with **is**, get prefix is not added to getter and in the setter name, **is** is replaced with set.

###Structure of Kotlin code

Kotlin also support concept of packages as in Java. Package declaration will be the first line of code, followed by import statement. After import we can have all declarations like classes, functions, and properties. Declarations defined in other files in same package are directly accessible. If we want to access members from other package we have to use import command similar to java.

```
package com.demo
import java.util.Random
class Square(val side: Int) 
fun area(): Int {
    return 10
}
```

Kotlin has no distinction between importing classes and functions. We can import the top-level function by name.

```
package com.example
import com.demo.area
fun main(args: Array<String>) {
   println(area())
}
```

Unlike java package name, there is no relation to directory structure in kotlin. We can put multiple classes in the same file and specify a package name in that file. Kotlin doesn’t impose any restrictions on directory structure according to package name. If in java, package name is com.example than we must be having directory named com and its subdirectory named example. In kotlin it is not necessary.

###Interfaces

Kotlin uses the colon in place of extends and implements keywords used in Java. Similar to Java, a class can implement as many interfaces as it wants, but it can extend only one class

```
interface ActionListener {
    fun click()
}
```

We have declared an interface with a single abstract method named click. Any class implementing this interface need to provide an implementation to click method, else it will become abstract class.

```
class Button : ActionListener {
    override fun click() = println("Button clicked")
}
// Use this code as
Button().click()
```

The override modifier in Kotlin is similar to the @Override annotation in Java. In Kotlin the override modifier is mandatory if we are overriding a function.

Unlike java a function in an interface can have an implementation in Kotlin.

```
interface ActionListener {
    fun click()
    fun onPressed() = println("Button Pressed")
}
```

If a class implement this interface, it needs to override **click** method. It is not mandatory to override **onPressed** method. If a class implements multiple interfaces having same method with default implementation then that class must override this method else it will not compile.

```
interface MouseListener {
    fun onPressed() = println("Mouse Pressed")
}
class Button : ActionListener, MouseListener {
    override fun click() = println("Button clicked")
    
    override fun onPressed() {           
      super<ActionListener>.onPressed()
      super<MouseListener>.onPressed()
    }
}
```

We can use super to invoke default implementation from super interface. In Kotlin we put the base type name in angle brackets: 

super<ActionListener>.onPressed().

###Inheritance

In Java’s we have to explicitly specify final modifier on a classes or a methods . Kotlin’s classes and methods are by default final. So in Kotlin if we want to create subclass of a class than we have to use open modifier on class.

```
open class Button : ActionListener {
 
     //This is open function, we can override it in subclass
     open fun mousePressed() {}
     //This function is final, we cannot override it.
     fun mouseReleased() {}
     //This function overrides an open function so it is also open    
     override fun click() {}
}
```

if we override a member of a base class or interface, the overriding member will also be open by default. If required we can explicitly mark the overriding member as final.

```
open class Button : ActionListener {
    final override fun click() {}
}
```

###Access Modifiers

The the table listed below is for modifiers for classes in Kotlin. In case of interfaces, we don’t use final, open, or abstract. A member in an interface is always open. We can’t declare it as final. It is abstract if it has no body, but no need to specify abstract modifier.

###Modifiers for class

<figure>
  <img src="{{site.baseurl}}/assets/images/2019-05-02-Kotlin-for-java-and-android-developers-1-2.png" alt="Kotlin Class Modifiers"/>
  <figcaption>Kotlin Class Modifiers</figcaption>
</figure>

###Visibility modifiers

Similar to Java we have same **public**, **protected**, and **private** modifiers in Kotlin. But the default modifier is public. Kotlin uses packages only to organizing code it has nothing to do with visibility control like java.

Kotlin has a new visibility modifier - **internal**. rIit has visiblility inside a module. A module is a set of Kotlin files compiled together(like Android Studio or Eclipse Project). Internal modifier provides real encapsulation in Kotlin. In case of Java, the encapsulation can be easily broken, we can write an external code with the same packages name and thus get access to classes of that package declarations.

In Kotlin we can use **private** modifier on top-level declarations, including classes, functions, and properties. It restricts the visibility to within the file where they are declared.

<figure>
  <img src="{{site.baseurl}}/assets/images/2019-05-02-Kotlin-for-java-and-android-developers-1-3.png" alt="Kotlin Visibility Modifiers"/>
  <figcaption>Kotlin Visibility Modifiers</figcaption>
</figure>

In Java, we can access a protected member from the same package, but in Kotlin a protected member is only visible in the class and its subclasses.

###Primary Constructor

```
class Student(val nickname: String)
```

Generally declarations in a class go inside curly braces. But Student class has no curly braces. This block of code surrounded by parentheses is called a **primary constructor**.

```
class Student constructor(_name: String) {
    val name: String
    init {
        name = _name
    } 
}
```

The **init** keyword used to create an **initializer** block. Such blocks contain initialization code that’s executed when the class is created, and are intended to be used together with primary constructors. We can also omit the constructor keyword if there are no modifiers on the primary constructor.

```
class Student(_name: String) {
    val name = _name
}
```

If class has a superclass, the primary constructor also needs to initialize the superclass.

```
open class Animal(val name: String) { ... }
class Dog(name: String) : Animal(name) { ... }
```

If we don’t have any constructors for a class, a default constructor is available like java

```
open class Animal
class Dog: Animal()
```

###Secondary constructors

In Kotlin we have defined two secondary constructors.

```
open class BaseActivity {
    constructor(ctx: Context) {
         // some code 
    }
    constructor(ctx: Context, attr: AttributeSet) {
        // some code
    } 
}
```

class BaseActivity is open class we can create its subclass

```
class MyActivity : BaseActivity {
    constructor(ctx: Context): super(ctx) {}
    constructor(ctx: Context, attr: AttributeSet)
                             :  super(ctx, attr) {} 
}
```

super will invoke constructor of super class. Similar to java this() can be used to invoke constructor of same class.

```
class MyActivity : BaseActivity {
    constructor(ctx: Context): this(ctx,SOME_ATTR) {}
    constructor(ctx: Context, attr: AttributeSet)
                             :  super(ctx, attr) {} 
}
```

**Coming Next**

In next blog on Kotlin we will explore lambdas, Nullable types, Operator overloading and other conventions

