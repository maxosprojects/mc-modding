---
layout: default
title: 01. Classes Intro
---

## Instance variables (A Bored Creeper story)
As an example, let's look at the `BoredCreeper` class.
The longer Bored Creeper walks without exploding, the more bored it gets.
![Bored Creeper](assets/img/01-creeper.jpg){: .center-image }

For the example's sake, let's say that the creeper is spawned (a.k.a `instantiated`, when talking Java) with `boredom` level of `0` and the maximum boredom level a creeper can have is `10,000`. In Java, that range of numbers fits well into an `int` (a.k.a `integer`, when talking human).

As you well know, what makes creeper a creeper is a set of specific traits. In this case we can say that the only trait that distinguishes Bored Creeper is his `boredom` *property* (a.k.a `field`, a.k.a `instance variable`, when talking Java).

So, a Bored Creeper class would look like the following:

```java
public class BoredCreeper {
  public int boredom = 0;
}
```

Now, I believe you would expect more than one `BoredCreeper` in the game (because it would be boring with just one bored creeper). You probably remember that you can instantiate the same class as many times as you like, and that is done by calling its constructor with the `new` keyword, like this:

```java
BoredCreeper creeper1 = new BoredCreeper();
BoredCreeper creeper2 = new BoredCreeper();
BoredCreeper creeper3 = new BoredCreeper();
```

Now, you've got three creepers, each of which has its own `boredom` field. That means that if you update the `boredom` field of `creeper1`, like this 
```java
creeper1.boredom = 500;
```
that doesn't affect other creepers (a.k.a `instances of class BoredCreeper`, when talking Java). That means that `creeper2.boredom` and `creeper3.boredom` are still `0`.

That is an important point to remember:
> All instances of a class are independent from each other and live their own lives even though they all come from the same class.

That is what classes are for. Now, think for a second, why was the word `class` picked for that role? As you well know, there are classes of animals, classes of vehicles and so on. Like, there is a vehicle class called `planes` and another vehicle class called `cars`. Vehicles in one class have some traits in common. Like, all `planes` have `wings` (which is a *property* of the class) and cars usually have four `wheels`.  
Just like that, `BoredCreeper` has a *property* `boredom` (a.k.a `field`, a.k.a `instance variable`, when talking Java). Now imagine that all planes shared the same pair of wings. That would be one weird class of vehicles, wouldn't it? Like, "today plane #2894 will have the wings, tomorrow - plane #8845".
!["wingless" plane](assets/img/01-wingless-plane.jpg){: .center-image }

And just like each plane in the `planes` class has its own pair of wings, each creeper has its own level of `boredom`, independent from other creepers (idk, maybe they get bored faster if they walk straight and slower when they walk in circles... open to interpretation), in which case `creeper1` can have the `500` level of `boredom` we discussed before, while other creepers' `boredom` is still at `0` (really lazy creepers those are).

Still have questions on anything above? I'd be happy to answer in an email!

Now that we know what `instance variable` is, we are ready to look at a `class variable`.

## Class variables
Still remember that each instance of a class (a.k.a Java object) has its own instance variables that are independent from any other instances of that class? Now, enter `class variables`!

`Class variable` is a variable that is shared by all instances of that class. For example:

```java
public class BoredCreeper {
  public static String COLOR = "GREEN";

  public int boredom = 0;
}
```

`BoredCreeper` here still has `instance variable` called `boredom`, but it now also has a `class variable` called `COLOR`, which kinda makes sense, right? There is no need for every instance of `BoredCreeper` to have their own `color` if they are all just green and never change color, right? I mean they could, but they are too lazy to do anything, remember?
![colorful creeper... weird...](assets/img/01-colorful-creeper.png){: .center-image }

But there should be a way for the dumb computer to tell which variable should be an `instance variable` (independent across instances) and which one - `class variable` (the same for all instances). And that is the `static` keyword, that you noticed already while I was still rambling about Java stuff.

So, the rule is simple:
> `Class variables` are shared by all instances of that class and they have `static` keyword to distinguish them.

> `Instance variable` only belongs to specific instance of a class (a.k.a `object`), meaning each instance of that class has its own `instance variables` that are not shared with other instances of that class.

Good. Now that we repeated the same thing bajillion number of times, we can move on to some other things.

## Access Levels
So far we've seen that the `BoredCreeper` class and all its variables are `public`. `Public` is not always great (like public bathrooms - not great).  

In software engineering `public` should be used cautiously. Without getting into the many details right now, just remember - exposing internal state of an object (a.k.a instance of a class) is frowned upon.

So, to be good software engineers, we will follow best software engineering practices and hide the internal state of the object like this:

```java
public class BoredCreeper {
  private static String COLOR = "GREEN";

  private int boredom = 0;
}
```

But, that means that those variables could be accessed only from within the class. What good would they do if no one is able to interact with that object? That would be like spawning creepers in another dimension that no one has access to.  

To fix that problem let's think how we want the creeper to be interacted with. As we established before, creepers get bored with time. So, let's say their boredom level increases with every game tick.  
That's good, now we know that there must be a way to tell the creeper to adjust his boredom level every tick. We will use a method for that since `boredom` variable is now private an no one except the creeper himself can change it. Here is the updated creeper class:

```java
public class BoredCreeper {
  private static String COLOR = "GREEN";

  private int boredom = 0;

  public void tick() {
    boredom = boredom + 1;
  }
}
```

There it is - one of the best software engineering practices in action - no one can change creeper's boredom level directly.

Another problem is that the creeper has his boredom level to himself and no one has any idea how bored the creeper is. Let's give the creeper a chance to share how bored he is with the world! Because there are no other problems in the world without that creeper expressing his bad mood... like there is always enough emeralds and stuff, right?

```java
public class BoredCreeper {
  private static String COLOR = "GREEN";

  private int boredom = 0;

  public void tick() {
    boredom = boredom + 1;
  }

  public getBoredomLevel() {
    return boredom;
  }
}
```

Now this is good software engineering (and it wasn't that hard, wasn't it?) - there is a way for the game to tell the creeper to adjust boredom level without exposing that variable to the world and at the same time we can always ask him what is his current boredom level (not that we would ever ask him that, who cares about that creeper, right?).
