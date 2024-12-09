# Functional JavaScript, v2

- Slides: <https://observablehq.com/embed/@anjana/what-is-functional-programming>
- Exercises: <https://functional-first-steps.netlify.app/1-intro/1-overview/>
- Repository: <https://github.com/vakila/functional-first-steps>

Huh, TIL TutorialKit: <https://tutorialkit.dev/>

Also, this article from Recurse Center: <https://codewords.recurse.com/issues/one/an-introduction-to-functional-programming>

## Pure Functions

No _side effects_ and it must be _deterministic_. Meaning, it must only return a
value and always returns the same output for the same input.

## Recursion

Avoiding mutable state by not using `for`, `while`, and similar.

Two main parts:

- The _base case(s)_, which are the condition(s) which the function returns an
  output, instead of...
- Calling itself, which is a _recursive case_

## High-Order Functions

"First-class functions" if functions can be passed as the input or output of
other functions. A "high-order function" is one that either takes or returns
another function.

## Closure

A function defined within another, which retains access to the outer scope.

"Partial application" is a common term. Also, "currying" is essentially just
refactoring the "arity" (number of arguments) of a function down to one by
nesting closure.

## Function Composition

Pipelines, yo.

## Immutability

Don't change _in-place_, instead _replace_. Immutable data structures are
typically trees so can swap out pointers to specific nodes.

TIL Immer, pretty slick: <https://immerjs.github.io/immer/>

## Recap

References & recommended reading: <https://functional-first-steps.netlify.app/8-outro/2-next/>

TIL JS pipeline operator proposal: <https://github.com/tc39/proposal-pipeline-operator>
