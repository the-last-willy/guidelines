# Testability

Test driven development.

**Consider writing failing tests before implementing features.**

**Consider having a single failing test at a time.**

Writing multiples tests beforehand is useful.

When you're implementing new features, you should have at most one failing test at all times.
This makes catching regressions easier.

When you're refactoring, you should have no failing tests.
A failing test is a regression.

A nice side effect of that is focus.
You have a an objective : the failing test.
Another failing objective would be another failing test.
But since you only have one failing test.
You have a single target.
If you want to switch objective.
Disable the failing test and enable another one.

**Consider writing a minimal, reproducible example as a test case when debugging.**

Reactive programming or something like that.

Before attempting to debug a problem.

Map that problem into a test case

See [How to create a Minimal, Reproducible Example ](https://stackoverflow.com/help/minimal-reproducible-example).

