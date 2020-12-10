# Dispensables

A dispensable is something pointless and unneeded whose absence would make the code cleaner, more efficient and easier to understand.

## Comments

### Signs & Symptoms

A method is filled with explanatory comments.

### Remedy

- If a comment is intended to explain a complex expression, the expression should be split into understandable subexpressions using [Extract Variable](https://refactoring.guru/extract-variable).

- If a comment explains a section of code, this section can be turned into a separate method via [Extract Method](https://refactoring.guru/extract-method). The name of the new method can be taken from the comment text itself, most likely.

- If a method has already been extracted, but comments are still necessary to explain what the method does, give the method a self-explanatory name. Use [Rename Method](https://refactoring.guru/rename-method) for this.

- If you need to assert rules about a state that’s necessary for the system to work, use [Introduce Assertion](https://refactoring.guru/introduce-assertion).

### When to Ignore

Comments can sometimes be useful:

- When explaining **why** something is being implemented in a particular way.

- When explaining complex algorithms (when all other methods for simplifying the algorithm have been tried and come up short).

## Duplicate Code

### Signs & Symptoms

Two code fragments look almost identical.

### Remedy

- If the same code is found in two or more methods in the same class: use [Extract Method](https://refactoring.guru/extract-method) and place calls for the new method in both places.

- If the same code is found in two subclasses of the same level:

  - Use [Extract Method](https://refactoring.guru/extract-method) for both classes, followed by [Pull Up Field](https://refactoring.guru/pull-up-field) for the fields used in the method that you’re pulling up.

  - If the duplicate code is inside a constructor, use [Pull Up Constructor Body](https://refactoring.guru/pull-up-constructor-body).

  - If the duplicate code is similar but not completely identical, use [Form Template Method](https://refactoring.guru/form-template-method).

  - If two methods do the same thing but use different algorithms, select the best algorithm and apply [Substitute Algorithm](https://refactoring.guru/substitute-algorithm).

- If duplicate code is found in two different classes:

  - If the classes aren’t part of a hierarchy, use [Extract Superclass](https://refactoring.guru/extract-superclass) in order to create a single superclass for these classes that maintains all the previous functionality.

  - If it’s difficult or impossible to create a superclass, use [Extract Class](https://refactoring.guru/extract-class) in one class and use the new component in the other.

- If a large number of conditional expressions are present and perform the same code (differing only in their conditions), merge these operators into a single condition using [Consolidate Conditional Expression](https://refactoring.guru/consolidate-conditional-expression) and use [Extract Method](https://refactoring.guru/extract-method) to place the condition in a separate method with an easy-to-understand name.

- If the same code is performed in all branches of a conditional expression: place the identical code outside of the condition tree by using [Consolidate Duplicate Conditional Fragments](https://refactoring.guru/consolidate-duplicate-conditional-fragments).

### When to Ignore

In very rare cases, merging two identical fragments of code can make the code less intuitive and obvious.

## Lazy Class

### Signs & Symptoms

Understanding and maintaining classes always costs time and money. So if a class doesn’t do enough to earn your attention, it should be deleted.

### Remedy

- Components that are near-useless should be given the [Inline Class](https://refactoring.guru/inline-class) treatment.

- For subclasses with few functions, try [Collapse Hierarchy](https://refactoring.guru/collapse-hierarchy).

### When to Ignore

Sometimes a _Lazy Class_ is created in order to delineate intentions for future development, In this case, try to maintain a balance between clarity and simplicity in your code.

## Data Class

### Signs & Symptoms

A data class refers to a class that contains only fields and crude methods for accessing them (getters and setters). These are simply containers for data used by other classes. These classes don’t contain any additional functionality and can’t independently operate on the data that they own.

### Remedy

- If a class contains public fields, use [Encapsulate Field](https://refactoring.guru/encapsulate-field) to hide them from direct access and require that access be performed via getters and setters only.

- Use [Encapsulate Collection](https://refactoring.guru/encapsulate-collection) for data stored in collections (such as arrays).

- Review the client code that uses the class. In it, you may find functionality that would be better located in the data class itself. If this is the case, use [Move Method](https://refactoring.guru/move-method) and [Extract Method](https://refactoring.guru/extract-method) to migrate this functionality to the data class.

- After the class has been filled with well thought-out methods, you may want to get rid of old methods for data access that give overly broad access to the class data. For this, [Remove Setting Method](https://refactoring.guru/remove-setting-method) and [Hide Method](https://refactoring.guru/hide-method) may be helpful.

## Dead Code

### Signs & Symptoms

A variable, parameter, field, method or class is no longer used (usually because it’s obsolete).

### Remedy

The quickest way to find dead code is to use a good [IDE](http://en.wikipedia.org/wiki/Integrated_development_environment).

- Delete unused code and unneeded files.

- In the case of an unnecessary class, [Inline Class](https://refactoring.guru/inline-class) or [Collapse Hierarchy](https://refactoring.guru/collapse-hierarchy) can be applied if a subclass or superclass is used.

- To remove unneeded parameters, use [Remove Parameter](https://refactoring.guru/remove-parameter).

## Speculative Generality

### Signs & Symptoms

There’s an unused class, method, field or parameter.

### Remedy

- For removing unused abstract classes, try [Collapse Hierarchy](https://refactoring.guru/collapse-hierarchy).

- Unnecessary delegation of functionality to another class can be eliminated via [Inline Class](https://refactoring.guru/inline-class).

- Unused methods? Use [Inline Method](https://refactoring.guru/inline-method) to get rid of them.

- Methods with unused parameters should be given a look with the help of [Remove Parameter](https://refactoring.guru/remove-parameter).

- Unused fields can be simply deleted.

### When to Ignore

- If you’re working on a framework, it’s eminently reasonable to create functionality not used in the framework itself, as long as the functionality is needed by the frameworks’s users.

- Before deleting elements, make sure that they aren’t used in unit tests. This happens if tests need a way to get certain internal information from a class or perform special testing-related actions.

## Next steps

In the next part, we will tackle a type of code smells that prevents your application from being maintained or evolving fastly: Couplers
