---
layout: default
title: 05. Constructors Intro
---

Now  that we know a little more on instances, instance variables and methods, let's look at constructors.

Constructors play vital role in object creation - they initialize newly created objects (a.k.a instances of classes).  

> Initialization is a process of assigning initial values to variables.

Constructors in Java can be easily spotted as they:
1. Are named after the class they are declared in.
2. They don't have a return type (return type is implied - an instance of that class).

Other than not having an explicit return type, constructors are just like any other methods. They can contain code that usually assigns initial values to instance variables - object initialization.

## Default constructor
Check out the `Simple` class below:

```java
class Simple {

}
```

You might ask "what does this class have to do with constructors? it doesn't have any". That's a valid question, but the answer is that class `Simple` does have one constructor. That's right, it isn't explicitly defined in code, but the compiler creates an implicit constructor in case no constructors are defined explicitly.

> Compiler is the app that compiles human-readable code (in this case - Java code) into binary instructions for the processor to execute. That is needed since computers are dumb and don't understand human language - they only execute binary instructions.

So, the binary file that compiler creates (that computer understands) for class `Simple` is equivalent to the code below:

```java
class Simple {
  
  public Simple() {

  }
}
```

Here you can see that class `Simple` has one constructor, without arguments. That is called `default constructor`.

> Default constructor is a constructor that is created by compiler in case no constructors are defined in the class - created by default.

Default constructor is a convenience feature in Java that lets developers omit constructors that don't take parameters and don't contain code, as you can see in the first example above.  
You may ask "why having that constructor at all in that case?". That is because when an object is created a constructor must be used together with the keyword `new`, you'll see an example below.

## Explicit constructors
In case you need to execute some code when an object is created, you can define constructors explicitly. When you do that, compiler no longer creates default constructor for that class.

> Compiler doesn't create default constructor when an explicit constructor is defined in the class.

You can create as many constructors as you need in the class with as many arguments as you need, including one without arguments, like so:

```java
class NotThatSimple {

  public NotThatSimple() {
    // do something
  }

  public NotThatSimple(String someStringArg) {
    // do something else, with the "someStringArg" argument
  }
}
```

## Using constructors
As mentioned above, constructors are required to be able to instantiate a class. They are referenced together with the keyword `new`.

Here is an example of how the two constructors in class `NotThatSimple` can be used.

```java
NotThatSimple instance1 = new NotThatSimple();
NotThatSimple instance2 = new NotThatSimple("some string");
```

And here is an example how to make an instance of class `Simple` using the implicit default constructor:

```java
Simple instance1 = new Simple();
```

Now, let's look at the class `Practice05Constructors` and tests in `Practice05ConstructorsTest`.

{% highlight java linenos %}
public class Practice05Constructors {

    private String name = "no args";

    public Practice05Constructors() {
      // we could do something here too
    }

    public Practice05Constructors(String newName) {
        name = newName;
    }

    public String getName() {
        return name;
    }
}
{% endhighlight %}

We'll refer to that as `sut` for brevity.

{% highlight java linenos %}
public class Practice05ConstructorsTest {

    @Test
    public void createInstanceWithoutArgs() {
        // Create instance without args
        Practice05Constructors instance = new Practice05Constructors();

        assertThat(instance).isNotNull();
        assertThat(instance.getName()).isEqualTo("no args");
    }

    @Test
    public void createInstanceWithArgs() {
        // Create instance with "new name" arg
        Practice05Constructors instance = new Practice05Constructors("new name");

        assertThat(instance).isNotNull();
        assertThat(instance.getName()).isEqualTo("new name");
    }
}
{% endhighlight %}

We'll refer to that as `test` for brevity.

Here is what to note:
1. <i class='fa fa-exclamation-triangle' style="color: #FFDC00"></i> Variable assignment that follows variable declaration (`sut` line 3) is executed before the constructor - very important to remember!
2. Test `createInstanceWithArgs()` refers to a constructor with `String` argument in `test` line 15.  
So, corresponding constructor is defined in `sut` line 9.
3. Test `createInstanceWithArgs()` asserts that `getName()` method must return string `"new name"`.  
We can see that `getName()` method returns variable `name` (`sut` line 14). That means that the string that is passed to the constructor when a new instance is created (`test` line 15), must be assigned to the `name` variable.  
That is done in `sut` line 10.
4. Test `createInstanceWithoutArgs()` refers to a constructor without arguments.  
However, we now have a constructor with arguments (`sut` line 9). And we know that default constructor is not created when an explicit constructor is defined.  
So, we have to create a constructor without arguments.  
That is done in `sut` line 5.
5. Test `createInstanceWithoutArgs()` asserts that method `getName()` must return `"no args"` string. That string is already assigned to the `name` variable in `sut` line 3.  
Since variable `name` is already returned by the `getName()` method, we don't need to do anything extra in the constructor in `sut` line 5.
