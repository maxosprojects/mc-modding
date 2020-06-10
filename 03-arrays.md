---
layout: default
title: 03. Arrays
---

## Intro
The simplest type of collection in almost any programming language is `array`.

> In Java, any variable must be declared before it can be used.  
> Variable declaration must include the type of the variable followed by the name, like so
> ```java
> String someWords;
> ```

> Variables can be initialized (an initial value can be assigned) together with declaration, like so
> ```java
> String someWords = "words words words, some more words, yet more words...";
> String someMoreWords = "wasting bytes...we still have more bytes on the disk...";
> ```

# Fixed size
In Java, arrays have fixed size, which means that once an array is declared (just like any other variable) its size can't be changed. I.e. when you declare an array like this

```java
int[] someArray = { 1, 2, 3 };
```

it will forever be of size `3` - it can never contain fewer or more than `3` elements.  

> The things that an array (or any other collection) contains are called `elements`.

# Accessing array elements
Elements in arrays can only be accessed by their `index` and that `index` is `zero-based`. Like, number `1` in the example above can be accessed like so:

```java
someArray[0];
```
and number `2` can be accessed like so:

```java
someArray[1];
```

> The index of the last element of an array in Java is always `size_of_the_array - 1`. So, in the example above, where the size of the array is `3`, the index of the last element is `2` (that's the element that is number `3`)

So:
```java
someArray[2];
```
gives number `3`.

# Changing array elements
Elements of arrays can be replaced with elements of the same type as the array was declared to contain.  
In the example above, array `someArray` can only contain integers, which means that you 
can't shove it a `String` or a `double`.

Changing elements of arrays is as easy as accessing elements of arrays - by their `index`.

```java
someArray[2] = 5;
```

Now array `someArray` contains the following sequence: `1, 2, 5`.

# Finding length of array
Length of an array is available by the `length` property of the array.  
In the case of `someArray` from above that would be:

```java
someArray.length;
```
