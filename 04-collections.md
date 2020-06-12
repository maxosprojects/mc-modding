---
layout: default
title: 04. Collections
---

## Intro
Now that you've got familiar with arrays, it's time to look at collections.

The meaning of the word "collection" is a group of items, usually of one kind.

In Java, there is a number of classes/interfaces all originating from one interface called `Collection`.  
Interface `Collection` defines a number of methods that all descendants inherit. For example, all implementations of `Collection` interface have methods `add()`, `remove()`, `contains()` and others to make it possible to do corresponding operations on collections.  
The entire list of all methods can be seen [in the official documentation](https://docs.oracle.com/javase/8/docs/api/java/util/Collection.html).

The most commonly used types of collections are `List` and `Set`. Those are interfaces, which means they are not implementations, but "contracts" that implementations must fulfil.  
For instance, in addition to all the methods that interface `Collection` enforces, `List` enforces some more, like `get(index)` (by index), `remove(index)`, which `Collection doesn't enforce.  

Here is the diagram that lists most commonly used Java collection interfaces and some of their actual implementations.

![colorful creeper... weird...](assets/img/04-collection-hierarchy.png){: .center-image }

On that diagram, brown boxes depict interfaces ("contracts") that implementations (actual classes - blue boxes) must fulfil.  
Like the most commonly used implementation of `List` is `ArrayList` and the most commonly used implementation of `Set` is `HashSet`.

> All implementations/descendants of `Collection` interface are dynamically sized, meaning, for example, you can add/remove elements to/from a `List`. That is something arrays can't do.

## List
`List` is just like an array - a collection of elements that can be accessed by index. However, as noted above, `List` can be resized, while array can't.

> `List` is ordered.

Example: from a list containing letters `a, b, c, d` you can get letter `a` by index `0`, letter `b` by index `1` and so on, and that order is preserved until the list is updated.  

Lists can be updated by removing an element by specific index, inserting new elements at specific index or just adding new elements at the end of the list.  

Here is the [official documentation on the `List` interface](https://docs.oracle.com/javase/8/docs/api/java/util/List.html).

## Using List
You can start with the most common implementation of `List` - `ArrayList`. Here is how a `List` is instantiated:

```java
List<String> mylist = new ArrayList<>();
```

It is a good practice to define variable types as interfaces, which is why the type for the `myList` variable is `List`. But, `List` is an interface and needs an implementation to be instantiated, which is why `ArrayList` is used.

Since `ArrayList` implements interface `List`, an instance of `ArrayList` can be assigned to a variable of type `List` (they are compatible, see diagram above).

It is also recommended to specify type of elements that `List` will contain in 99.9999% of cases. In our case, `myList` will contain `String`s, which is indicated in the angle brackets.

The `<>` used when calling the `ArrayList` constructor is called `diamond`. That is a way to tell Java to infer the type of elements the created `ArrayList` will contain from the definition of the variable that instance will be assigned to, which in this is case is `String`. That is how `generics` are treated, which is a bit advanced topic for you right now, so we'll get back to `generics` later.

Then you can add elements to that list like this:

```java
myList.add("some word");
myList.add("another word");
```

You can iterate over a list this way:

```java
for (String element : mylist) {
  System.out.println(element);
}
```

That will print the following in the terminal:

```
some word
another word
```

Every time you iterate over a list, variable `element` will get all the elements of the list one by one in the same order. That is because the "contract" of `List` says that the collection is ordered.

> Note: never add/remove elements to/from a `Collection` (which includes `List`, `Set` and others) while you're iterating over it (in that loop). You are free to do whatever you want with it before and after the loop.

## Set
`Set` doesn't have any operations by index, like `List` has.

> `Set` is also unordered and it eliminates duplicates.

Example: given you have an empty `Set` and you letters `a, b, c, b, d, a` one by one, at the end `Set` will have only four elements - `a, b, c, d` instead of six as letters `a` and `b` have duplicates and are ignored by the `Set` when you add them.

Another great feature of `Set` implementations is that they are usually very good at telling very fast whether specific element exists in the `Set`.  

That last feature of the `Set` will be very useful when you implement temperature updates in your mod.  
You've seen how many different biomes there are and you don't want to write as many `if()` blocks for each of the biomes, do you? Instead, you could create one `Set` (call it `coldBiomes`) and add all the cold biomes there, like `FROZEN_OCEAN`, `SNOWY_MOUNTAINS` and so on. Then you would create a `Set` (call is `warmBiomes`) and add all the warm biomes into it, like `DEEP_WARM_OCEAN`.  
Then you will only need two `if()` blocks to check whether the biome the player is in is warm or cold, instead of 74 `if()` blocks.  
See below how to do that kind of stuff.

Here is the [official documentation on the `Set` interface](https://docs.oracle.com/javase/8/docs/api/java/util/Set.html).

## Using Set
The most commonly used implementation of `Set` is `HashSet`. Here is how to instantiate it:

```java
Set<String> mySet = new HashSet<>();
```

See the explanation of the angle brackets above in the "Using List" section if you forgot. Same rules apply to `Set`s.

Then you can add elements to that set just like you did with `List`:

```java
mySet.add("some word");
mySet.add("another word");
```

You can iterate over a set the same way you did with list:

```java
for (String element : mySet) {
  System.out.println(element);
}
```

However, "contract" of `Set` doesn't say anything about the order of the elements in `Set`.  
So, one time when you iterate over it you may get this in the terminal:

```
some word
another word
```

and another time it could be

```
another word
some word
```

So, no guarantees as to the order the `Set` spits out those elements.

Here are the great parts about the `Set`:
- it will tell you very fast whether a phrase is in the `Set`
- it will ignore any subsequent duplicated phrases you may add

Of course the speed at which it will find the phrase in a `Set` of just five elements won't make much difference, but the difference will be significant on a `Set` of ten thousand phrases compared to a `List`.

## Map
To make things more confusing, there is also a `Map` interface with it's own implementations that belong to collections (as a group), but are not descendants of `Collection` interface. That is because `Map` always operates two items at a time - key and value, while `Collection` only operates values.

`Map` is essentially a lookup table that has values correspond to keys, like this:

| Key (e.g. person's name) | Value (e.g. person's age) |   |   |
|--------------------------|---------------------------|---|---|
| Brad                     | 23                        |   |   |
| Carl                     | 15                        |   |   |
| ...                      | ...                       |   |   |
|                          |                           |   |   |

Here is the [official documentation on the `Map` interface](https://docs.oracle.com/javase/8/docs/api/java/util/Map.html).

## Using Map
The most commonly used implementation of `Map` is `HashMap`. Here is how to instantiate it:

```java
Map<String, Integer> myMap = new HashSet<>();
```

Here, between the angle brackets you see the type that is used for the keys and the type that is used for values.

You can add new values for corresponding keys like this:

```java
myMap.put("Brad", 23);
myMap.put("Carl", 15);
```

You can iterate over a map in a few ways, but most of the time `Map`s are used to look up some values by their keys:

```java
Integer bradsAge = myMap.get("Brad");
Integer carlsAge = myMap.get("Carl");
```

If you ask a `Map` for a value by a non-existent key, it will return `null` instead, regardless of the type of values that `Map` operates on.

Just as implementations of `Set`, implementations of `Map` are usually very good at finding values by keys very fast.
