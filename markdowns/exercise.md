# Refactoring exercise: the Gilded Rose

## Introduction

You will find the starter code in [the following repository](https://github.com/thomasdom/GildedRoseJavaStarter).

The goal is to refactor the code so it is cleaner, maintainable and evolutive.

The tricky part here is that you **cannot modify the Item class** (you can suppose that it is used somewhere else in other company's projects).

## Specification

Hi and welcome to team Gilded Rose. As you know, we are a small inn with a prime location in a
prominent city ran by a friendly innkeeper named Allison. We also buy and sell only the finest goods.
Unfortunately, our goods are constantly degrading in quality as they approach their sell by date. We
have a system in place that updates our inventory for us. It was developed by a no-nonsense type named
Leeroy, who has moved on to new adventures. Your task is to add the new feature to our system so that
we can begin selling a new category of items. First an introduction to our system:

- All items have a `sellIn` value which denotes the number of days we have to sell the item
- All items have a `quality` value which denotes how valuable the item is
- At the end of each day our system lowers both values for every item

Pretty simple, right? Well this is where it gets interesting:

- Once the sell by date has passed, Quality degrades twice as fast
- The Quality of an item is never negative
- "Aged Brie" actually increases in Quality the older it gets
- The Quality of an item is never more than 50
- "Sulfuras", being a legendary item, never has to be sold or decreases in Quality
- "Backstage passes", like aged brie, increases in Quality as its SellIn value approaches; Quality increases by 2 when there are 10 days or less and by 3 when there are 5 days or less but Quality drops to 0 after the concert

We have recently signed a supplier of conjured items. This requires an update to our system:

- "Conjured" items degrade in Quality twice as fast as normal items

Feel free to make any changes to the `updateQuality` method and add any new code as long as everything
still works correctly. However, do not alter the `Item` class or `items` property as those belong to the
goblin in the corner who will insta-rage and one-shot you as he doesn't believe in shared code
ownership (you can make the `updateQuality` method and `items` property static if you like, we'll cover
for you).

Just for clarification, an item can never have its Quality increase above 50, however "Sulfuras" is a
legendary item and as such its Quality is 80 and it never alters.

## Instructions

### Step 1: Create an `ItemBuilder` class

Create an `ItemBuilder` class that will, as its name suggests, build items. This class will be useful
only for our unit tests in this exercise, but can be useful for future project updates.

The `ItemBuilder` class must have 3 attributes:

- `name`, which is the name of the item
- `quality`, which represents the Quality of the item
- `sellIn`, which represents the number of days we have to sell the item

The `ItemBuilder` class must have a constructor and 5 methods:

- The constructor must set default values for the name, quality and sellIn
- The method `called` must set the name and return the builder
- The method `ofQuality` must set the quality value and return the builder
- The method `toBeSoldIn` must set the sellIn value and return the builder
- The method `pastExpirationDate` must set the sellIn value to `0` and return the builder
- Finally, the method `build` must return a new `Item` with the predefined values

Example of usage:

```java
Item item = new ItemBuilder().called("Any Item").pastExpirationDate().ofQuality(10).build();
```

### Step 2: Write unit tests against specifications

Write unit tests that cover current specifications without the conjured items improvement.

There are 11 unit tests to write:

1. It should lower quality and sellIn values of every item at the end of each day
2. It should lower quality twice as fast when past expiration date
3. It should never lower quality value below zero
4. It should increase aged brie quality at the end of each day
5. It should never increase aged brie quality above 50
6. It should never lower Sulfuras quality and sellIn value
7. It should increase backstage passes quality at the end of each day
8. It should never increase backstage passes quality above 50
9. It should increase backstage passes quality twice as fast when sellIn value is equal or less than 10
10. It should increase backstage passes quality thrice as fast when sellIn value is equal or less than 5
11. It should lower backstage passes quality to zero when past expiration date

You are given the first unit test below:

```java
@Test
public void should_lower_quality_and_sellIn_values_of_every_item_at_the_end_of_each_day() throws Exception {
    Item[] items = new Item[]{new ItemBuilder().called("Any Item").toBeSoldIn(10).ofQuality(10).build()};
    GildedRose app = new GildedRose(items);

    app.updateQuality();

    assertEquals(9, app.items[0].sellIn);
    assertEquals(9, app.items[0].quality);
}
```

The other 10 unit tests will look like this first unit test, but some values have to be changed to test properly a specification.

### Step 3: Write unit tests for conjured items

Write unit tests that cover conjured items new specification.

There are 2 unit tests to write:

1. It should lower conjured mana cake quality twice as fast
2. It should never lower conjured mana cake quality below zero

You can use the unit tests written above to write these two tests

### Step 4: Refactor the `for` loop

Currently, the `for` loop uses the old-style form with an increment value.

Refactor the `for` loop to be a "For-Of" loop type.

Example:

```java
for (Product p : products) {
    // Code
}
```

### Step 5: Extract methods

Using the [Extract Method](https://refactoring.guru/extract-method) refactoring technique,
refactor the `GildedRose` class to implement 3 new methods:

- A method that decreases the quality of an item by 1
- A method that increases the quality of an item by 1
- A method that checks if the item quality is under 50

Hint: choose carefully the names of your methods

### Step 6: Introduce constants

Using the [Replace Magic Number with Symbolic Constant](https://refactoring.guru/replace-magic-number-with-symbolic-constant) refactoring technique, create two new constants to represent the minimum and the maximum quality.

### Step 7: Comment common and specific item behaviors

This step does not improve the code, but is a very good preparation for the next steps.

Add comments in the code to be able to see which conditions refers to which item.

There are four types of behavior to comment:

- Normal item
- Legendary item
- Aged Brie item
- Backstage pass item

### Step 8: Define an Updater interface with some utility methods

Define an interface called `Updater` that contains at least a public method called `update`, taking a parameter of type `Item`.

This interface will be useful to implement the updaters.

### Step 9: Create an updater implementation for each item type (but not yet for conjuring items)

Create four classes that implements the `Updater` interface. These classes will be responsible for handling the day-to-day update for each item type.

There are 4 classes to create:

- `AgedBrieUpdater`: Will update the values for the Aged Brie item
- `BackstagePassUpdater`: Will update the values for the Backstage Pass item
- `LegendaryUpdater`: Will update the values for the Sulfuras item
- `CommonUpdater`: Will update the values for other items

These classes should be in a package called `updaters`.

Hints:

- You should define/move common behavior into the `Updater` interface
- There may be an updater whose `update` method may be empty
- Make sure that your code stays readable by using good names

### Step 10: Add an UpdaterFactory class

Create an `UpdaterFactory` class. This class will instantiate the correct `Updater` implementation
based on the item name.

This class must have a method called `updaterFor` which takes a parameter of type `Item`. This method
will create a new instance of the appropriate Updater classes created earlier to handle an item.

Example: if the item name is "Aged Brie", the `UpdaterFactory` class will instantiate an object of type `AgedBrieUpdater`.

Hints:

- Use a map with a key that represents the item type (legendary, aged brie, etc); The map values will be a list of the item names associated to the item type
- Use constants as keys for the map
- Use features of Java 8+ if possible

### Step 11: Refactor the GildedRose class to use updaters

Refactor the `updateQuality` method in the `GildedRose` class to use the updater factory for each item.

### Step 12: Handle conjuring items

Now it is time to implement the conjured items feature!

Using the concepts introduced earlier, create a `ConjuredItemsUpdater` class to handle its behavior.

Hint: Do not forget to use your new Updater class in the `UpdaterFactory`.

## General hints

- Take time to read carefully the specification
- One test won't pass until the step 12. It's normal! But be careful to check that the other tests passes before moving to the next step

## Conclusion

Hooray! If you managed to get here, you have refactored a simple app to be clean,
maintainable and prone to evolution.
