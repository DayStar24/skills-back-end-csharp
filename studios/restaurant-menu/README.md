---
title: 'Studio: Restaurant Menu'
currentMenu: studios
---

Let's practice designing classes using the following scenario. You've been hired to create a web application for a local restaurant. They want to not only be able to display their current menu, but also edit it through an admin panel.

You're not going to build an actual application in this studio. Instead, you will focus on the *design* of a portion of this application. Object-oriented programming in C# requires more intentional, up-front planning than most programming you've done to-date.

## Design

For the restaurant application, you know you'll need to create classes to facilitate this behavior and represent the various components of the menu. After talking to the owner, you have these details:

- The menu consists of several menu items
- Each menu item has a price, description, and category (appetizer, main course, or dessert)
- It should be possible to display whether a menu item is new or not
- The app should know when the menu was last updated, so visitors can see that the restaurant is constantly changing and adding exciting new items

Starting with pen and paper (or your favorite notes application on your laptop), begin to sketch out the design for two classes, `Menu` and `MenuItem`. List the fields and properties that each should have, along with the data type and access level of each. Also consider whether any field should be `static` or `readonly`. Also consider what constructors your class might need, and whether any field should be `static` or `readonly`.

When thinking of data types, don't forget to consider collections (lists and dictionaries), and if using a collection type, to specify the type it will contain.

At this stage, don't think about how the application will work or behave; you should focus on the way that data will be represented within these classes, and how they should relate to each other.

<aside class="aside-note" markdown="1">
You may find it useful to use one or more of the classes provided by C#, such as [DateTime](https://msdn.microsoft.com/en-us/library/system.datetime(v=vs.110).aspx).
</aside>

## Presenting Your Design

Once you have sketched out your fields and properties, find a classmate to describe your design to. Class design can be subjective, so it's important to properly think and talk through your choices before coding.

While a classmate is presenting their design to you, ask questions about why they made the decisions that they did, and think about use cases that that might come up, to see if their design fits with those.

## Implementation

Within the `csharp-exercises` solution, create a new console project named `Restaurant`. Add classes `Menu` and `MenuItem` and add the fields and properties that you designed. Be sure to add custom getters and setters code as appropriate.
