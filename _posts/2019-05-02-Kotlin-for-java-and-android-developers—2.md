---
layout: post
title:  "Kotlin for Java and Android Developers - Part 2"
author: atul
categories: [ technology, mobile development ]
image: assets/images/2019-05-02-Kotlin-for-java-and-android-developers-1-1.png
featured: no
hidden: false
---
In previous blog (Kotlin for Java and Android Developers —1) we have discussed about function, variables, classes, interfaces, modifiers and constructor. We will now explore functional programming with lambdas and how kotlin handles Nullable types.

### Lambdas

Lambda is the block of code which can be used as an object or we can say Lambda is a type of object which holds a block of code. Comparing it to java we can say a lambda is similar to an anonymous object with only one method.

```
// Java implementation
button.addActionListener(new ActionListener() {
    @Override
    public void actionPerformed(ActionEvent e) {
      /* actions on click */
    }
});
// Kotlin implementation
button.addActionListener { /* actions on click */ }
```
**How to write a Lambda expression**

<figure>
  <img src="{{site.baseurl}}/assets/images/2019-05-02-Kotlin-for-java-and-android-developers-2-2.png" alt="How to write Lambda Expressions"/>
  <figcaption>Lambda Expressions</figcaption>
</figure>

In Kotlin a lambda expression is always surrounded by curly braces. The arrow separates the argument list and the body of the lambda.

You can store a lambda expression in a variable and then treat this variable like a normal function.

```
val sum = { x: Int, y: Int -> x + y }
println(sum(1, 2))
```

-> is used to separate parameters and body. The body can be of multiple lines, the expression that is evaluated at last in the body will be used a return value of lambda.

lambda is similar to writing a function, the only difference is that lambda have no name.

```
fun sum(x: Int, y: Int) = x+y

```

If we define variable using val, we can’t update it to hold a new lambda. We can use var than we can hold new lambda any time we want

```
var sum = { x: Int, y: Int -> x + y }
sum = { y: Int -> y + 10 }
```

**Replace a single parameter with it**

```
val sum = { x: Int -> x + 5 }
```

If we have a lambda with one parameter, than we can omit that parameter and lambda can use that parameter using keyword it

```
val sum = { it + 5 }
```

{ it + 5 } is equivalent to { x -> x + 5 }


***Compiler cares about the type***

Let us consider a variable that holds reference to lambda with two Int and return an Int value


```
val calculated : (Int,Int) -> Int
```

If we try to assign a lambda with different type, it will not compile.

```
//This won't compile
calculated = { x double, y double -> x+y }
```

**Use unit to specify lambda has no return type**

```
val calculated : (Int,Int) -> Unit = { x, y -> print(x+y) }
```

***Passing Lambda to a function***

let us suppose we want to write function to convert Centigrade to Fahrenheit or Kilogram to pounds, that function will take a parameter and depending upon the formulae it converts the input and return a value. So we are planning to have two different functions with different formulae to achieve that. Now think as if we can pass a value and a formulae as a parameter to the function than we will be thinking of only one function. 

```
fun convert (value: Double ,formulae: (Double) -> Double) : Double {
   var result = formulae(value)
   return result
}
```

convert function will take a lambda as second parameter (Double) -> Double. We can invoke this function as

```
convert(30.0, { v: Double -> v * 1.8 + 32 })
```

Now this convert function will convert 30.0 degrees to Fahrenheit.

### Nullable types 

In java we often get NullPointerException in our code. We have to take care of our object to be null. In kotlin you will hardly ever get NullPointerException. 

A nullable type variables are those, which can hold null values in addition to its predefined data type. Any variable or property can be defined as nullable by including ? in the declaration.

```
var str : String? = "SomeValue"
// str can be assigned null value
str = null
```

while accessing properties and functions of a nullable type than we have to use ***safe call***.

? is the safe call operator, it allows us to safely access properties and functions of nullable type.

```
var car : Car? = Car()
// in kotlin
car?.drive()
// in java
if(car != null){
  car.drive()
}
```

drive() function is invoked only if car object is not null.

Use ***let*** to run the code if values are not null. 

```
// in java 
if(car != null) {
   System.out.prinlt(car.modelName);
}
```
```
// in kotlin with let
car?.let {
   println(car.modelName)
}
```

if car object is not null it will print it model name. 

***?.let*** allows to run the code only if the objects value is not null.

***Elvis Operator*** 

Now consider the following kotlin code that works in java

```
// to kotlin compiler this is unsafe code
if(car != null){
  println(car.modelName)
} else {
  println("Unknown")
}
```

In kotlin the compiler thinks there is a chance that the variable car may be updated in between the null check and function call or property access. So kotlin compiler will consider it as unsafe.

The Elvis operator ? : can be used in place of if expression. It returns the value on the left side of operator if it is not null else it returns the value on its right.

```
// kotlin code
car?.modelName ?: "Unknown"
```

Elvis operator first check the value on left side

  car?.modelName

If this value is nor null, Elvis operator will return its value. If in case it is null than it will return the value on right side (in this case “Unknown”)

### Conclusion
Lambdas are very important part of functional programming. In case of non functional programming, it accepts data input and provides a data output. Functional programs can read functions as input and can generate functions as output. Object oriented programs combine data with their functions, but in functional programming we combine functions with functions. That is why understanding of Lambda functions are so important in kotlin.




