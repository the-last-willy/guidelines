# Debuggability

The purpose of this document is to present a coding style that makes debugging easier.

## Function calls

No non-trivial expression for function parameters.
Breaking in sub-expression is tedious.

**Consider storing sub-expressions into variables before passing them to a function.**

```cpp
// In order to step into `f`, you first have to step into `g`, step out and then step into `f`.
// These additional inputs are tedious.
f(g(x));

// Instead consider writing.
auto tmp = g(x);
f(tmp);

// The only downside besides the additional line of code is that `tmp` might need to be moved.
// As the subexpression went from being an r-value to an l-value.
// (I don't think compilers can optimize that given that it require to change semantics.)

// Trivial expressions are, given some value `x` :  `&x`, `*x`.
// You cannot step into these expressions.
// If these are overloaded, they might not be considered trivial anymore.
// You should still consider adhering to strict semantics and making them forcibly inlined
// so that you can't step into them.
```

## Member data

In order to debug member data, you might be a watchpoint.
These however might considerably slow the execution of the program.

One alternative to that is putting a breakpoint inside a setter.
Which means that you need to have a setter in the first place.

**Consider avoiding exposing directly member variables.**

It also needed to break inside the function body, not on the function itself.
Breaking on the function itself will break before the arguments are initialized.
Therefore losing useful information.
In order to be able to break inside a function body,
the function need to be more than one line long.

**Consider avoiding to write one line functions.**

C++ example:
```cpp
class {
  int priv;  
public:
  int pub; // Cannot break on pub.
  
  // Breaking on this line will break before `i` is initialized.
  // Stepping over will step out of the function.
  // Rendering debugging less useful as it makes getting the value of `i` here impossible.
  void assign_one_liner(int i) { priv = i; }
  
  void assign(int i) {
    priv = i; // Break here.
  }
};
```
