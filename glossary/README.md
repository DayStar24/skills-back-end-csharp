---
title: Glossary
currentMenu: glossary
---

**assembly**: A unit of compiled code that can be executed by the .NET runtime environment.

**class**: A blueprint, or template, for an object. Classes defining properties (data) and  methods (behavior) that each object created from the class template will have. In C#, a publicly available class is declared as follows:

    ```csharp
public class MyClass {
    // property and method definitions
}
```

**Common Language Runtime (CLR)**: The runtime environment for .NET applications. The CLR handles compilation and execution of .NET applications, along with providing built-in classes and other resources.

Source: [MSDN](https://msdn.microsoft.com/en-us/library/8bs2ecf4(v=vs.110).aspx)

**declaration**: To specify the name and data type of a variable or property. This may be done either in conjunction with or prior to initialization.

```csharp
// Declaration without initialization
string name;
```

```csharp
// Declaration with initialization
string name = "Michael";
```

**encapsulation**: The bundling of related data and behaviors that operate on that data, usually with restricted access to internal, non-public data and behaviors. In object-oriented programming, encapsulation is achieved through the use of objects.

Source: [Wikipedia](https://en.wikipedia.org/wiki/Encapsulation_(computer_programming))

**Integrated Development Environment (IDE)**: An application that provides access to and integration between software development tools that would otherwise be used independently, such as compilation, execution, access to documentation, built tools, source code management, and version control. Visual Studio is the most widely used C# and .NET IDE.

**inheritance**: A mechanism within object-oriented programming that allows one class to be based on another class, thus "inheriting" its properties and behaviors. Inheritance is also sometimes referred to as **subtyping**.

Source: [Wikipedia](https://en.wikipedia.org/wiki/Inheritance_(object-oriented_programming))

**initialize**: To assign a value to a declared variable or property for the first time. This may be done in conjunction with or after declaration.

<aside class="aside-example" markdown="1">

```csharp
// Initialization with declaration
string name = "Michael";
```

```csharp
// Separate declaration and initialization
string name;
name = "Michael";
```
</aside>

**instance**: An explicit object within a program.

<aside class="aside-example" markdown="1">
The variable `apple` is an instance of `Fruit`.

```csharp
Fruit apple = new Fruit("apple");
```
</aside>

**instance property (or instance variable)**: A property of a class that is non-static, so that each instance of the class has its own version of the property.

**object**: A value (i.e. a concrete unit within a program) created from a class. An object has a data type, which is the same as the name of the class it was created from.

```csharp
MyClass anObject = new Myclass( /* constructor parameters */ );
```

**polymorphism**: An object-oriented mechanism that allows for objects of different types to be used in the same way.

<aside class="aside-example" markdown="1">
Polymorphism may be realized via inheritance. Supposed classes `Dog` and `Cat` each extend the class `Pet`. Then variables and properties of type `Pet` may be assigned instances of `Dog` and `Cat`. Note, however, that in this case we can only use the properties and methods of `Pet`, and not those that belong to `Dog` and `Cat` but not `Pet`.
```java
Pet jack = new Dog("Jack");
Pet suki = new Cat("Suki");
```
</aside>

<aside class="aside-example" markdown="1">
Polymorphism may be realized via interfaces. An alternative design approach to the example above would be to have `Pet` be an interface, and then implement the `Pet` interface with the classes `Dog` and `Cat`. Then, similarly, variables and properties of type `Pet` may be assigned instances of `Dog` and `Cat`. As above, it is then only allowed to call methods that are part of the `Pet` interface.
</aside>
