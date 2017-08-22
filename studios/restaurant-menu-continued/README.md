---
title: 'Studio: Restaurant Menu Continued'
currentMenu: studios
---

We began designing and implementing our `Menu` and `MenuItem` classes [last time](../restaurant-menu/). Let's continue working on these classes, adding some methods.

## Design

To review, here are the details you have from the restaurant owner:

- The menu consists of several menu items
- Each menu item has a price, description, and category (appetizer, main course, or dessert)
- It should be possible to display whether a menu item is new or not
- The app should know when the menu was last updated, so visitors can see that the restaurant is constantly changing and adding exciting new items

Based on these details, you'll need to include some methods:

- A way to add and remove menu items from the menu
- A way to tell if a menu item is new
- A way to tell when the menu was last updated
- A way to print out both a menu item and an entire menu
- A way to determine whether or not two menu items are equal

Starting with pen and paper (or your favorite notes application on your laptop), begin to sketch out the methods that you'll need for these classes. List the method names and access levels, along with the input parameter types and return types. Also consider whether any methods should be `static`.

<aside class="aside-note" markdown="1">
If you don't have an ID property on your `MenuItem` class then providing a `GetHashCode` method to supplement your `Equals` method will be beyond the scope of what we've learned so far. If this is the case for you, leave off `GetHashCode`. Visual Studio will give you a warning, but you will still be able to run your code.
</aside>

## Presenting Your Design

Once you have sketched out your methods, find a classmate to describe your design to. Class design can be subjective, so it's important to properly think and talk through your choices before coding.

While a classmate is presenting their design to you, ask questions about why they made the decisions that they did, and think about use cases that might come up, to see if their design accommodates those.

## Implementation

Within the `Restaurant` project in the `csharp-exercises` solution, begin adding the methods you designed to `Menu` and `MenuItem`. Within the `Program.cs` file, test your classes in the `Main` method by creating several menu items, adding them to a menu, and printing the menu to the screen.
