---
layout: default
title: 06. Logic
---

Logic is one of the fundamental parts of software development. Almost every modern app (including mods) have some logic implemented in it.

Logic exists in many different forms. Let's look at one of them - boolean logic.

## Boolean logic
Boolean logic is probably the simplest form of logic because there are only two possible outcomes: `true` and `false`.  
However, the inputs are not necessarily boolean, though they could be.

For instance, inputs could be integer, strings or any other type, but they don't remain that way for long. The first operation they are involved in converts them all to boolean.

Let's look at an example:

```java
public boolean isGreater10(int input) {
  return input > 10;
}
```

In the example, the input of type `int` is compared to another `int`, the result of which is `boolean`.

## Logical operators
Here is a list of logical operators:

| Operator | Name               | Parameters                            | Description                                         | Example                           |
|----------|--------------------|---------------------------------------|-----------------------------------------------------|-----------------------------------|
| !        | NOT                | Boolean                               | Inverts boolean                                     | `!true` is equal `false`          |
| ==       | EQUALS             | Any object reference and or primitive | Compares two objects by reference and/or primitives | `10 == 10` is equal `true`        |
| &&       | AND                | Boolean                               | Logical AND                                         | `true && false`  is equal `false` |
| \|\|       | OR                 | Boolean                               | Logical OR                                          | `true \|\| false` is equal `true`   |
| >        | Greater than       | Any numbers                           | Compares two numbers                                | `10 > 5`  is equal `true`         |
| >=       | Greater or equal   | Any numbers                           | Compares two numbers                                | `10 >= 5`  is equal `true`        |
| <        | Less than          | Any numbers                           | Compares two numbers                                | `10 < 5`  is equal `false`        |
| <=       | Less than or equal | Any numbers                           | Compares two numbers                                | `10 <= 5`  is equal `false`       |

> `Comparison of objects by reference` is an important rule to remember.  
For instance, when comparing `String`s, never use the logical comparison (`==`). Instead, use the `equals()` method of the `String`.  
Logical comparison of objects must only be used when trying to find whether two variables reference `the same` object.

## Truth table
Certain logical operators have `truth tables` - how possible parameters are mapped to specific results.

For example, the `NOT` operator (`!`) has only two options. Its truth table looks like this:

| Input | Result |
|-------|--------|
| true  | false  |
| false | true   |

The `AND` operator (`&&`) has four options. Its truth table looks like this:

| Input 1 | Input 2 | Result |
|---------|---------|--------|
| true    | true    | true   |
| true    | false   | false  |
| false   | true    | false  |
| false   | false   | false  |

The `OR` operator (`||`) also has four options. Its truth table looks like this:

| Input 1 | Input 2 | Result |
|---------|---------|--------|
| true    | true    | true   |
| true    | false   | true   |
| false   | true    | true   |
| false   | false   | false  |

The rest of logical operators have unbound number of options, hence trying to build a truth table for those doesn't make much sense as it never ends.  
E.g. the `greater than` operator (`>`) has infinite possible inputs and infinite corresponding results.

## Logical expressions and logical groups
The simplest logical expression would be the `NOT` operator (`!`) with a parameter, as in an example in the `Logical operators` table above. All other expressions that involve single logical operator have two parameters.

However, there are cases when there are more than one parameter that needs to be taken into account.  
Like, the type of entity, whether the entity is old and whether it is day or night. That produces three parameters and the expression may look like this:

```java
public boolean isMobAndOldAndTimeOfDay(boolean mob, boolean old, boolean day) {
  return mob && old && day;
}
```

That example is relatively simple, but even that can be grouped, even though that won't change the meaning:

```java
public boolean isMobAndOldAndTimeOfDay(boolean mob, boolean old, boolean day) {
  return (mob && old) && day;
}
```

However, a similar expression but with different operators can be tricky:

```java
public boolean isMobAndOldOrTimeOfDay(boolean mob, boolean old, boolean day) {
  return mob && old || day;
}
```

How do we read that?

There are certain rules for operators in Java, which are called `"operator precedence"`.  
Here they are: [Operator precedence](https://docs.oracle.com/javase/tutorial/java/nutsandbolts/operators.html)

According to the operator precedence, first the `AND` operator must be evaluated, then the result of that must be evaluated with the `OR` operator.  
That can be grouped for easier evaluation like this:

```java
public boolean isMobAndOldOrTimeOfDay(boolean mob, boolean old, boolean day) {
  return (mob && old) || day;
}
```

Since the inputs are `boolean`, that expression also has a truth table.  
Since there are eight possible outcomes, to make it easier to spot the values we are going to replace `true` with `1` and `false` with `0`:

| Mob | Old | Day | Result |
|-----|-----|-----|--------|
| 1   | 1   | 1   | 1      |
| 1   | 1   | 0   | 1      |
| 1   | 0   | 1   | 0      |
| 1   | 0   | 0   | 0      |
| 0   | 1   | 1   | 0      |
| 0   | 1   | 0   | 0      |
| 0   | 0   | 1   | 0      |
| 0   | 0   | 0   | 0      |

In case the requirement states that the `OR` operator must be evaluated first, then the outcomes would be a bit different.  
Here is how it must look in code (parenthesis are no longer optional in that case) and its corresponding truth table:

```java
public boolean isMobAndOldOrTimeOfDay(boolean mob, boolean old, boolean day) {
  return mob && (old || day);
}
```

| Mob | Old | Day | Result |
|-----|-----|-----|--------|
| 1   | 1   | 1   | 1      |
| 1   | 1   | 0   | 1      |
| 1   | 0   | 1   | 1      |
| 1   | 0   | 0   | 0      |
| 0   | 1   | 1   | 0      |
| 0   | 1   | 0   | 0      |
| 0   | 0   | 1   | 0      |
| 0   | 0   | 0   | 0      |

As you can see, there is one more `true` outcome - three overall vs. the previous case where `AND` was evaluated first - two overall.

Using parenthesis, any number of groups can be created in an expression, but it is advised to create variables for some groups instead to make it easier to read and maintain the code when expression gets too complex.

The last example could be rewritten as follows (just for demonstration purposes, that expression isn't really complex yet):

```java
public boolean isMobAndOldOrTimeOfDay(boolean mob, boolean old, boolean day) {
  boolean isOldOrDay = old || day;
  return mob && isOldOrDay;
}
```
