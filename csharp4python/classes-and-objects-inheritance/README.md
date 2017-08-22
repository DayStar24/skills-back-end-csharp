---
title: 'Classes and Objects: Inheritance'
currentMenu: csharp4python
---

Inheritance is the second of the **Three Pillars of Object-Oriented Programming** that we will encounter.

From our [Glossary](../../glossary/), here's a definition:

<aside class="aside-definition" markdown="1">
**inheritance**: A mechanism within object-oriented programming that allows one class to be based on another class, thus "inheriting" its properties and behaviors. Inheritance is also sometimes referred to as **subtyping**.
</aside>

## Inheritance in C&#35;

Inheritance in C# is very similar to the same concept in Python. We **extend** another class to inherit its data and behaviors (that is, fields, properties, and methods). Recall that in Python the syntax for inheritance was the following:

```python
class Cat:
    # ...code for the Cat class...

class HouseCat(Cat):
    # ...code for the HouseCat class...
```

Any fields and non-constructor methods in `Cat` would be available to each instance of `HouseCat`. We express the inheritance relationship in plain English by saying that a `HouseCat` *extends* `Cat`, or that a `HouseCat` *is a* `Cat`.

In C#, the syntax for extending a class requires a colon (`:`) separating the two class names.

```csharp
public class Cat
{
    // ...code for the Cat class...
}

public class HouseCat : Cat
{
    // ...code for the HouseCat class...
}
```

We say that `HouseCat` is a **subclass**, **derived class**, or **child class** of `Cat`, and we say that `Cat` is the **superclass**, **base class**, or **parent class** of `HouseCat`. In C#, a class may extend only one class, but classes may extend each other in turn, creating hierarchies of classes. We often visualize these by drawing each class as a box, with lines descending from the base class to the subclass.

<div style="text-align:center;"><img src="inheritance-basic.png" style="width:400px;" /></div>

The shaded portion of these boxes can include additional information about each class. We'll learn about what we might put here in the next lesson.

Inheritance is a useful mechanism for sharing data and behavior between related classes, and it effectively creates hierarchies of classes that have more and more specialized behavior as you go from base class to subclass.

When this happens, we can visualize the inheritance structure with a slightly more complex diagram.

![Inheritance Tree](inheritance-tree.png)

As with Python, fields and non-constructor methods are directly available to instances of the subclass, subject to any access modifiers. In general, this means that `private` and `internal` members of a base class are not accessible to a subclass. (However, if the subclass and base class are in the same assembly, `internal` would allow access to a member.)

<aside class="aside-note" markdown="1">
This is a good time to review [access modifiers in C#](../introduction-to-classes-and-objects/#access-modifiers) if anything in the last paragraph was fuzzy.
</aside>

For an example, let's revisit our `Cat` and `HouseCat` implementations from [Chapter 13 of Unit 1](https://runestone.launchcode.org/runestone/static/thinkcspy/ClassesDiggingDeeper/Inheritance.html), modified to illustrate some C#-specific concepts.

```csharp
public class Cat {

    public bool IsTired { get; set; } = false;
    public bool IsHungry { get; set; } = false;
    public double Weight { get; set; }

    // The biological Family for all cat species
    private string family = "Felidae";
    public string Family
    {
        get { return family; }
        private set { family = value; }
    }

    public Cat (double weight) {
        Weight = weight;
    }

    // A cat is rested and hungry after it sleeps
    public void Sleep()
    {
        IsTired = false;
        IsHungry = true;
    }

    // Eating makes a cat not hungry
    public void Eat()
    {

        // eating when not hungry makes a cat sleepy
        if (!IsHungry)
        {
            IsTired = true;
        }

        IsHungry = false;
    }

    public virtual string Noise ()
    {
        return "Meeeeeeooooowww!";
    }
}
```

```csharp
public class HouseCat : Cat
{
    public string Name { get; set; }

    private string species = "Felis catus";
    public string Species
    {
        get { return species; }
        private set { species = value; }
    }

    public HouseCat(string name, double weight) : base(weight)
    {
        Name = name;
    }

    public bool IsSatisfied()
    {
        return !IsHungry && !IsTired;
    }

    public override string Noise()
    {
        return "Hello, my name is " + Name + "!";
    }

    public string Purr()
    {
        return "I'm a HouseCat";
    }
}
```

The class `HouseCat` extends `Cat`, using several different inheritance features that we will explore in turn.

Notice that `Cat` has a private string field `family`, representing the biological family of all cats. This field is not directly accessible to `HouseCat` since it is private, however it may be read via the public property `Family`. The setter for `Family` is private, however, so it may only be set within `Cat`. It makes sense that the another class should not be able to change the biological family of a cat, since this field should rarely, if ever, change.

Methods of the base class `Cat` may be called on instances of the subclass `HouseCat` as if they were defined as part of the `HouseCat`.

```csharp
HouseCat garfield = new HouseCat("Garfield", 12);
garfield.Eat();
```

The `Eat` method was defined in `Cat`, but may be called on all `HouseCat` instances as well. We say: "`HouseCat` inherits the method `Eat` from `Cat`."

### Working With Constructors in Subclasses

We mentioned above that a subclass inherits all *non-constructor* methods from its base class. Indeed, when extending a class, we will not be able to create new instances of our subclass `HouseCat` using any constructors provided by `Cat`. For example, this code will not compile:

```csharp
HouseCat thumper = new HouseCat(8.4);
```

The base class `Cat` has a constructor that takes a single parameter of type `double`, but `HouseCat` does not have such a constructor, and `Cat` constructors are not inherited by `HouseCat`. If we wanted to use such a constructor in the subclass, we would have to explicitly provide it. We'll see how to do this relatively easily in a moment.

Let's look at the constructor included in `HouseCat`:

```csharp
public HouseCat(string name, double weight) : base(weight)
{
    Name = name;
}
```

Here we use the `:` operator in conjunction with the keyword `base` to specify that our constructor should call the base class constructor with the argument `weight`. This call to the base class constructor will run before the body of the subclass constructor executes. This is a useful way to ensure that we're fully initializing our objects.

You may leave out such a call to a base class constructor only when the base class has a default, or *no-arg*, constructor (that is, a constructor that takes no arguments). In such a case, the default constructor is implicitly called for you. Here's what this would look like in `HouseCat`, if `Cat` had a default constructor.

```csharp
public HouseCat(string name)
{
    Name = name;
}
```

Even though we don't explicitly specify that we want to call a constructor from `Cat`, the default constructor would be called (if it existed, which in this case it doesn't).

As a consequence of this constructor syntax, we can easily expose any constructor from the base class by providing a subclass constructor with the same signature and no body, and calling the base class constructor.

```csharp
public HouseCat(double weight) : base(weight) {}
```

<aside class="aside-warning" markdown="1">
This constructor is a bad one, and is included merely to introduce syntax and usage. We would not want to have a constructor for `HouseCat` that didn't initialize an essential property such as `Name`.
</aside>

### Overriding Base Class Behavior

Sometimes when extending a class, we'll want to modify behavior provided by the base class. This can be done by replacing the implementation of an inherited method by a completely new method implementation. For a given method, we can do this via **method overriding**, if the base class allows.

For a method in a base class to be overridden in a subclass, it must be marked as `virtual`. In our example, the `Noise` method of `Cat` is marked `virtual`, which means we may override it in `HouseCat`. When we override it, we must use the `override` keyword.

<aside class="aside-warning" markdown="1">
When overriding a method from a base class, the method signatures *must be exactly the same*. Recall that the signature of a method is the method name, along with it's return type, and the type and number of input parameters.
</aside>

<aside class="aside-warning" markdown="1">
Unlike in some other object-oriented languages (notably Java), in C# a method must explicitly allow itself to be overridden by using the `virtual` keyword.
</aside>

Here are the methods in question.

In `Cat`:

```csharp
public virtual string Noise()
{
    return "Meeeeeeooooowww!";
}
```

In `HouseCat`:

```csharp
public override string Noise()
{
    return "Hello, my name is " + Name + "!";
}
```

Here we override `Noise` in `HouseCat`. If we have a `HouseCat` object and call it's noise method, we will be using the method defined in `HouseCat`.

```csharp
Cat plainCat = new Cat(8.6);
HouseCat garfield = new HouseCat("Garfield", 12);

Console.WriteLine(plainCat.Noise()); // prints "Meeeeeeooooowww!"
Console.WriteLine(garfield.Noise()); // prints "Hello, my name is Garfield!"
```

<aside class="aside-warning" markdown="1">
When overriding a method from a base class, the method signatures *must be exactly the same*. Recall that the signature of a method is the method name and access level, along with it's return type, and the type and number of input parameters.

In this example, the signature of our method is:
```csharp
public string Noise();
```
</aside>

When overriding a method, we may call the method from the base class that we're overriding by using `base`:

```csharp
public override void Noise()
{
    if (IsSatisfied())
    {
        return "Hello, my name is " + Name + "!";
    }
    else
    {
        return base.Noise();
    }
}
```

This calls the overridden method in the base class via `base.Noise()`, carrying out the original behavior if the given conditional branch is reached.

### The Object Class

In a previous lesson, we introduced the "special" methods `Equals` and `ToString`, noting that all classes were provided default implementations of these methods that could be overridden.

In fact, these default methods are part of a class called `Object`. If a class does not explicitly extend another class, then it implicitly extends `Object`. So the default implementations of `Equals` and `ToString` (along with a few [other methods](https://msdn.microsoft.com/en-us/library/system.object(v=vs.110).aspx#Methods)) are made available to us via inheritance. Those that are marked `virtual` - such as `Equals` and `ToString` - may be overridden.

### Abstract Classes and Class Members

In this section we briefly introduce an intermediate object-oriented concept. We will not use it much in this course, but you're likely to encounter it in the "real world" and it is a useful one to know.

We noted in the introduction to this section that inheritance is a way to share behaviors among classes. You'll sometimes find yourself creating a base class as a way to share behaviors among related classes. However, in such situations it is not always desirable for instances of the base class to be created.

For example, suppose we began coding two classes, `HouseCat` and `Tiger`. Upon writing the code, we realized that there was some common data and behaviors. For example, they both make a noise, come from the same biological family, and get hungry. In order to reduce code repetition, we combined those in `Cat` (as above).

```csharp
public class Cat
{
    // Cat class definition
}

public class HouseCat : Cat
{
    // HouseCat class definition
}

public class Tiger : Cat
{
    // Tiger class definition
}
```

In reality, though, we might not want objects of type `Cat` to be created, since such a cat couldn't actually exist (a real cat would have a specific genus and species, for example). We could prevent objects of type `Cat` from being created, while still enabling sharing of behavior among its subclasses, by making `Cat` an **abstract class**.

```csharp
public abstract class Cat
{
    // Cat class definition
}
```

To reiterate, *abstract classes are classes that may not be instantiated*. In order to use the behavior of an abstract class, *we must extend it*.

We have a further tool that we may use here, which is an **abstract method**. An abstract method is a method in an abstract class that does not have a body. In other words, it does not have any associated code, only a signature. It must also be marked `abstract`.

In our abstract `Cat` class, it would make sense to make `Noise` abstract to force any class extending it to provide its own implementation of that behavior.

```csharp
public abstract class Cat
{
    public abstract string Noise();

    // More Cat class code...
}
```

Any class extending `Cat` is then forced to provide its own version of `Noise`, with the exact same method signature (but without the `abstract` keyword).

## Data Typing And Inheritance

When one class extends another, as `HouseCat` extends `Cat`, a field or local variable of the type of the parent class may hold an object that is of the type of the child class.

In other words, this is allowed:

```csharp
Cat suki = new HouseCat("Suki", 8);
```

This is acceptable because a `HouseCat` *is a* `Cat`. Furthermore, when we call methods on such an object, the compiler is smart enough to determine which method it should call. For example, the following call to `Noise()` will call the version defined in `HouseCat`:

```csharp
// Calls HouseCat's Noise() method
suki.Noise();
```

This only works for methods that are declared in the parent class, however. If we have a `HouseCat` object stored in a `Cat` variable or field, then it is *not* allowed to call methods that are only part `HouseCat`.

```csharp
// Results in a compiler error, since Cat
// doesn't have such a method
suki.IsSatisfied();
```

Here, `IsSatistfied()` is defined in `HouseCat`, and there is not a corresponding overridden method in `Cat`. If we were *really, really* sure that we had a `Cat` that was actually a `HouseCat`, we could call such a method by first casting:

```csharp
// As long as suki really is a HouseCat, this works
(suki as HouseCat).IsSatisfied();
```

The danger here is that if `suki` is in fact not a `HouseCat` (it was declared only as a `Cat`, after all) then we'll experience a runtime exception. A **runtime exception** is an error that occurs upon running the program, and is not found by the compiler beforehand. These are dangerous, and situations where they might come up should be avoided. So you should only cast an object to another type when you are very sure that it's safe to do so.

Storing objects of one type (e.g. `HouseCat`) in a variable or field of another "compatible" type (e.g. `Cat`) is an example of **polymorphism**. We'll have more to say about polymorphism in a future lesson.

## References

- [Inheritance in C# (msdn.microsoft.com)](https://msdn.microsoft.com/en-us/library/ms173149.aspx)
- [The override keyword (msdn.microsoft.com)](https://msdn.microsoft.com/en-us/library/ebca9ah3.aspx)
- [The virtual keyword (msdn.microsoft.com)](https://msdn.microsoft.com/en-us/library/9fkccyh4.aspx)
- [The Object Class (msdn.microsoft.com)](https://msdn.microsoft.com/en-us/library/system.object(v=vs.110).aspx)
- [Abstract Classes and Class Members](https://msdn.microsoft.com/en-us/library/ms173150.aspx)
