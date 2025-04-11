## The first example

This is how I envision writing code with Delta. The most important features are in place.

```
record Atom:
    const protons: Int
    const neutrons: Int
    const electrons: Int

# comment
# Implicitly, a builder is built so an object can be created in the following manner

const helium = Atom.builder()
    .protons(2)
    .neutrons(2)
    .electrons(2)
    .build()

def Atom.get_atomic_weight() -> Int:
    return self.protons + self.neutrons

union Dummy = [Int | Atom]

def do_something(something: Dummy) -> Int:
    return when something: # Yeah, pattern-matching. Compile-time checks if it is exhaustive.
        is Int -> return something
        is Atom -> something.get_atomic_weight()

print(do_something(10)) # prints 10
print(do_something(helium)) # prints 4
```
