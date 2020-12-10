# Bloaters

Bloaters are code, methods and classes that have increased to such gargantuan proportions that they’re hard to work with. Usually these smells don’t crop up right away, rather they accumulate over time as the program evolves (and especially when nobody makes an effort to eradicate them).

## Long Method

### Signs & Symptoms

A method contains too many lines of code. Generally, any method longer than ten lines should make you start asking questions.

### Remedy

As a rule of thumb, if you feel the need to comment on something inside a method, you should take this code and put it in a new method. Even a single line can and should be split off into a separate method, if it requires explanations. And if the method has a descriptive name, nobody will need to look at the code to see what it does.

- To reduce the length of a method body, use [Extract Method](https://refactoring.guru/extract-method).

- If local variables and parameters interfere with extracting a method, use [Replace Temp with Query](https://refactoring.guru/replace-temp-with-query), [Introduce Parameter Object](https://refactoring.guru/introduce-parameter-object) or [Preserve Whole Object](https://refactoring.guru/preserve-whole-object).

- If none of the previous recipes help, try moving the entire method to a separate object via [Replace Method with Method Object](https://refactoring.guru/replace-method-with-method-object).

- Conditional operators and loops are a good clue that code can be moved to a separate method. For conditionals, use [Decompose Conditional](https://refactoring.guru/decompose-conditional). If loops are in the way, try [Extract Method](https://refactoring.guru/extract-method).

## Large Class

### Signs & Symptoms

A class contains many fields/methods/lines of code.

### Remedy

When a class is wearing too many (functional) hats, think about splitting it up:

- [Extract Class](https://refactoring.guru/extract-class) helps if part of the behavior of the large class can be spun off into a separate component.

- [Extract Subclass](https://refactoring.guru/extract-subclass) helps if part of the behavior of the large class can be implemented in different ways or is used in rare cases.

- [Extract Interface](https://refactoring.guru/extract-interface) helps if it’s necessary to have a list of the operations and behaviors that the client can use.

- If a large class is responsible for the graphical interface, you may try to move some of its data and behavior to a separate domain object. In doing so, it may be necessary to store copies of some data in two places and keep the data consistent. [Duplicate Observed Data](https://refactoring.guru/duplicate-observed-data) offers a way to do this.

## Primitive Obsession

### Signs & Symptoms

- Use of primitives instead of small objects for simple tasks (such as currency, ranges, special strings for phone numbers, etc.)

- Use of constants for coding information (such as a constant USER_ADMIN_ROLE = 1 for referring to users with administrator rights.)

- Use of string constants as field names for use in data arrays.

### Remedy

- If you have a large variety of primitive fields, it may be possible to logically group some of them into their own class. Even better, move the behavior associated with this data into the class too. For this task, try [Replace Data Value with Object](https://refactoring.guru/replace-data-value-with-object).

- If the values of primitive fields are used in method parameters, go with [Introduce Parameter Object](https://refactoring.guru/introduce-parameter-object) or [Preserve Whole Object](https://refactoring.guru/preserve-whole-object).

- When complicated data is coded in variables, use [Replace Type Code with Class](https://refactoring.guru/replace-type-code-with-class), [Replace Type Code with Subclasses](https://refactoring.guru/replace-type-code-with-subclasses) or [Replace Type Code with State/Strategy](https://refactoring.guru/replace-type-code-with-state-strategy).

- If there are arrays among the variables, use [Replace Array with Object](https://refactoring.guru/replace-array-with-object).

## Long Parameter List

### Signs & Symptoms

More than three or four parameters for a method.

### Remedy

- Check what values are passed to parameters. If some of the arguments are just results of method calls of another object, use [Replace Parameter with Method Call](https://refactoring.guru/replace-parameter-with-method-call). This object can be placed in the field of its own class or passed as a method parameter.

- Instead of passing a group of data received from another object as parameters, pass the object itself to the method, by using [Preserve Whole Object](https://refactoring.guru/preserve-whole-object).

- If there are several unrelated data elements, sometimes you can merge them into a single parameter object via [Introduce Parameter Object](https://refactoring.guru/introduce-parameter-object).

### When to Ignore

Don't get rid of parameters if doing so would cause unwanted dependency between classes.

## Data Clumps

### Signs & Symptoms

Sometimes different parts of the code contain identical groups of variables (such as parameters for connecting to a database). These clumps should be turned into their own classes.

### Remedy

- If repeating data comprises the fields of a class, use [Extract Class](https://refactoring.guru/extract-class) to move the fields to their own class.

- If the same data clumps are passed in the parameters of methods, use [Introduce Parameter Object](https://refactoring.guru/introduce-parameter-object) to set them off as a class.

- If some of the data is passed to other methods, think about passing the entire data object to the method instead of just individual fields. [Preserve Whole Object](https://refactoring.guru/preserve-whole-object) will help with this.

- Look at the code used by these fields. It may be a good idea to move this code to a data class.

### When to Ignore

Passing an entire object in the parameters of a method, instead of passing just its values (primitive types), may create an undesirable dependency between the two classes.

## Next steps

In the next part, we will tackle a very nasty type of code smells: Object-Orientation Abusers
