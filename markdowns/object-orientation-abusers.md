# Object-Orientation Abusers

All these code smells are incomplete or incorrect application of object-oriented programming principles.

## Switch Statements

### Signs & Symptoms

You have a complex `switch` operator or sequence of `if` statements.

### Remedy

- To isolate `switch` and put it in the right class, you may need [Extract Method](https://refactoring.guru/extract-method) and then [Move Method](https://refactoring.guru/move-method).

- If a `switch` is based on type code, such as when the program’s runtime mode is switched, use [Replace Type Code with Subclasses](https://refactoring.guru/replace-type-code-with-subclasses) or [Replace Type Code with State/Strategy](https://refactoring.guru/replace-type-code-with-state-strategy).

- After specifying the inheritance structure, use [Replace Conditional with Polymorphism](https://refactoring.guru/replace-conditional-with-polymorphism).

- If there aren’t too many conditions in the operator and they all call same method with different parameters, polymorphism will be superfluous. If this case, you can break that method into multiple smaller methods with [Replace Parameter with Explicit Methods](https://refactoring.guru/replace-parameter-with-explicit-methods) and change the `switch` accordingly.

- If one of the conditional options is `null`, use [Introduce Null Object](https://refactoring.guru/introduce-null-object).

### When to Ignore

When a `switch` operator performs simple actions, there’s no reason to make code changes.

Often `switch` operators are used by factory design patterns ([Factory Method](https://refactoring.guru/design-patterns/factory-method) or [Abstract Factory](https://refactoring.guru/design-patterns/abstract-factory)) to select a created class.

## Temporary Field

### Signs & Symptoms

Temporary fields get their values (and thus are needed by objects) only under certain circumstances. Outside of these circumstances, they’re empty.

### Remedy

- Temporary fields and all code operating on them can be put in a separate class via [Extract Class](https://refactoring.guru/extract-class). In other words, you’re creating a method object, achieving the same result as if you would perform [Replace Method with Method Object](https://refactoring.guru/replace-method-with-method-object).

- [Introduce Null Object](https://refactoring.guru/introduce-null-object) and integrate it in place of the conditional code which was used to check the temporary field values for existence.

## Refused Bequest

### Signs & Symptoms

If a subclass uses only some of the methods and properties inherited from its parents, the hierarchy is off-kilter. The unneeded methods may simply go unused or be redefined and give off exceptions.

### Remedy

- If inheritance makes no sense and the subclass really does have nothing in common with the superclass, eliminate inheritance in favor of [Replace Inheritance with Delegation](https://refactoring.guru/replace-inheritance-with-delegation).

- If inheritance is appropriate, get rid of unneeded fields and methods in the subclass. Extract all fields and methods needed by the subclass from the parent class, put them in a new subclass, and set both classes to inherit from it ([Extract Superclass](https://refactoring.guru/extract-superclass)).

## Alternative Classes with Different Interfaces

### Signs & Symptoms

Two classes perform identical functions but have different method names.

### Remedy

Try to put the interface of classes in terms of a common denominator:

- [Rename Method](https://refactoring.guru/rename-method)s to make them identical in all alternative classes.

- [Move Method](https://refactoring.guru/move-method), [Add Parameter](https://refactoring.guru/add-parameter) and [Parameterize Method](https://refactoring.guru/parameterize-method) to make the signature and implementation of methods the same.

- If only part of the functionality of the classes is duplicated, try using [Extract Superclass](https://refactoring.guru/extract-superclass). In this case, the existing classes will become subclasses.

- After you have determined which treatment method to use and implemented it, you may be able to delete one of the classes.

### When to Ignore

Sometimes merging classes is impossible or so difficult as to be pointless. One example is when the alternative classes are in different libraries that each have their own version of the class.

## Next steps

In the next part, we will tackle a type of code smells that impacts strongly the development of your application in the long run: Change Preventers
