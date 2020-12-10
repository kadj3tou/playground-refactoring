# Couplers

All the smells in this category contribute to excessive coupling between classes or show what happens if coupling is replaced by excessive delegation.

## Feature Envy

### Signs & Symptoms

A method accesses the data of another object more than its own data.

### Remedy

As a basic rule, if things change at the same time, you should keep them in the same place. Usually data and functions that use this data are changed together (although exceptions are possible).

- If a method clearly should be moved to another place, use [Move Method](https://refactoring.guru/move-method).

- If only part of a method accesses the data of another object, use [Extract Method](https://refactoring.guru/extract-method) to move the part in question.

- If a method uses functions from several other classes, first determine which class contains most of the data used. Then place the method in this class along with the other data. Alternatively, use [Extract Method](https://refactoring.guru/extract-method) to split the method into several parts that can be placed in different places in different classes.

### When to Ignore

Sometimes behavior is purposefully kept separate from the class that holds the data. The usual advantage of this is the ability to dynamically change the behavior (see [Strategy](https://refactoring.guru/design-patterns/strategy), [Visitor](https://refactoring.guru/design-patterns/visitor) and other patterns).

## Inappropriate Intimacy

### Signs & Symptoms

One class uses the internal fields and methods of another class.

### Remedy

- The simplest solution is to use [Move Method](https://refactoring.guru/move-method) and [Move Field](https://refactoring.guru/move-field) to move parts of one class to the class in which those parts are used. But this works only if the first class truly doesn’t need these parts.

- Another solution is to use [Extract Class](https://refactoring.guru/extract-class) and [Hide Delegate](https://refactoring.guru/hide-delegate) on the class to make the code relations "official".

- If the classes are mutually interdependent, you should use [Change Bidirectional Association to Unidirectional](https://refactoring.guru/change-bidirectional-association-to-unidirectional).

- If this "intimacy" is between a subclass and the superclass, consider [Replace Delegation with Inheritance](https://refactoring.guru/replace-delegation-with-inheritance).

## Message Chains

### Signs & Symptoms

In code you see a series of calls resembling `$a->b()->c()->d()`.

### Remedy

- To delete a message chain, use [Hide Delegate](https://refactoring.guru/hide-delegate).

- Sometimes it’s better to think of why the end object is being used. Perhaps it would make sense to use [Extract Method](https://refactoring.guru/extract-method) for this functionality and move it to the beginning of the chain, by using [Move Method](https://refactoring.guru/move-method).

### When to Ignore

Overly aggressive delegate hiding can cause code in which it’s hard to see where the functionality is actually occurring. Which is another way of saying, avoid the Middle Man smell as well.

## Middle Man

### Signs & Symptoms

If a class performs only one action, delegating work to another class, why does it exist at all?

### Remedy

If most of a method’s classes delegate to another class, [Remove Middle Man](https://refactoring.guru/remove-middle-man) is in order.

### When to Ignore

Don’t delete middle man that have been created for a reason:

- A middle man may have been added to avoid interclass dependencies.

- Some design patterns create middle man on purpose (such as [Proxy](https://refactoring.guru/design-patterns/proxy) or [Decorator](https://refactoring.guru/design-patterns/decorator)).

## Next steps

In the last part, we will tackle other types of code smells.
