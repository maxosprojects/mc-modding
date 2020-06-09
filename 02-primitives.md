---
layout: default
title: 02. Primitives
---

## "Primi-what?"
Primitives in Java are special data types. Variables of primitive types do not represent any object and are not instances of any class.

The most common example of a primitive type is `int`. Variables of type `int` still represent integer numbers, but they are not of type `Integer`.  
Variables of primitive types don't have any methods or fields because they are not instances of any class.

## Relationship to objects
All primitive types have object counterparts. Here is the full list of primitive types in Java: [Java Primitive Types](https://docs.oracle.com/javase/tutorial/java/nutsandbolts/datatypes.html)

So, `int` has a related type `Integer` and `boolean` has a related type `Boolean`.  
They are also compatible with their counterparts. It is ok to do things like that:

```java
int intVariable = 10;
Integer integerVariable = 20;
intVariable = integerVariable;
integerVariable = intVariable;
```

That is because Java compiler does things for you behind the scenes so that you don't have to write extra code. That is called "Autoboxing" - Java wraps `int` value of `intVariable` into `Integer` when you do `integerVariable = intVariable` and unwraps it when you do `intVariable = integerVariable` - "boxes" and "unboxes" them.

Ok, that was a bit of a detour with the autoboxing. But the most important thing to remember from that is that primitive types are compatible with their counterparts and in most cases can be used interchangeably. But, of course, they are not "cross-compatible", like assigning a variable of type `Double` to a variable of type `int` doesn't work.

To see what `int` is actually missing from not being an `Integer` have a look the [Integer's javadoc](https://docs.oracle.com/javase/8/docs/api/java/lang/Integer.html)

> Javadoc is a special documentation format that can be added to methods and classes and that is processed by special java tools into nice documentation like [Integer's javadoc](https://docs.oracle.com/javase/8/docs/api/java/lang/Integer.html)

## Literals
You can find a very good explanation of literals here [Java Primitive Types](https://docs.oracle.com/javase/tutorial/java/nutsandbolts/datatypes.html) in the "Literals" section.  

Also, as you've seen before (and actually used in your mod), a `long` literal differs from an `int` literal by the character `L` added to the end, like `10L` is number `10` represented as `long`.
