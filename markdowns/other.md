# Other Smells

Below are the smells which don’t fall into any broad category.

## Incomplete Library Class

### Signs & Symptoms

Sooner or later, [libraries](https://en.wikipedia.org/wiki/Library_(computing)) stop meeting user needs. The only solution to the problem—changing the library—is often impossible since the library is read-only.

### Remedy

- To introduce a few methods to a library class, use Introduce Foreign Method.

- For big changes in a class library, use Introduce Local Extension.

### When to Ignore

Extending a library can generate additional work if the changes to the library involve changes in code.
