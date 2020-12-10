# Change Preventers

These smells mean that if you need to change something in one place in your code, you have to make many changes in other places too. Program development becomes much more complicated and expensive as a result.

## Divergent Change

Divergent Change is when many changes are made to a single class.

### Signs & Symptoms

You find yourself having to change many unrelated methods when you make changes to a class. For example, when adding a new product type you have to change the methods for finding, displaying, and ordering products.

### Remedy

- Split up the behavior of the class via [Extract Class](https://refactoring.guru/extract-class).

- If different classes have the same behavior, you may want to combine the classes through inheritance ([Extract Superclass](https://refactoring.guru/extract-superclass) and [Extract Subclass](https://refactoring.guru/extract-subclass)).

## Shotgun Surgery

Shotgun Surgery resembles Divergent Change but is actually the opposite smell. Divergent Change is when many changes are made to a single class. Shotgun Surgery refers to when a single change is made to multiple classes simultaneously.

### Signs & Symptoms

Making any modifications requires that you make many small changes to many different classes.

### Remedy

- Use [Move Method](https://refactoring.guru/move-method) and [Move Field](https://refactoring.guru/move-field) to move existing class behaviors into a single class. If there’s no class appropriate for this, create a new one.

- If moving code to the same class leaves the original classes almost empty, try to get rid of these now-redundant classes via [Inline Class](https://refactoring.guru/inline-class).

## Parallel Inheritance Hierarchies

### Signs & Symptoms

Whenever you create a subclass for a class, you find yourself needing to create a subclass for another class.

### Remedy

You may de-duplicate parallel class hierarchies in two steps. First, make instances of one hierarchy refer to instances of another hierarchy. Then, remove the hierarchy in the referred class, by using [Move Method](https://refactoring.guru/move-method) and [Move Field](https://refactoring.guru/move-field).

### When to Ignore

Sometimes having parallel class hierarchies is just a way to avoid even bigger mess with program architecture. If you find that your attempts to de-duplicate hierarchies produce even uglier code, just step out, revert all of your changes and get used to that code.

## Next steps

In the next part, we will tackle a type of code smells that makes your code a lot harder to read, and thus to maintain: Dispensables
