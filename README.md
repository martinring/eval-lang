# The **eval** Programming Language 1.0

**eval** (*express(ive) versatile all-purpose language*) is a modern
general-purpose programming language with a focus on simplicity, safety and
soundness. **eval** is compiled to *JavaScript* which makes it a natural choice
for state of the art projects in the field of web technology.

- **Statically Typed**

  As opposed to many mainstream languages like Java, C#, C++, etc. for which
  soundness of the type system cannot be proven, eval has a verifiably sound **and** complete
  but yet flexible static type system, which is strictly more powerful than
  Hindley-Milner type systems and features:

  * Dependent types
  * Linear types
  * Intersection and Union types
  * Existential types
  * Gradual typing

- **Object Oriented**

  **eval** is a pure object oriented language, fulfilling all rules of object
  oriented languages as defined by Alan Kay.

- **Functional**

  **eval** is purely functional. Functions are first class citizens. **eval**
  features advanced functional concepts like

  * Strict and lazy evaluation
  * Ad-Hoc polymorphism through type classes
  * Automatic derivation of all type classes
  * Type signatures can include proof obligations which are checked by the compiler.

## [Try **eval** online!!](https://martinring.github.io/eval-lang/tryEval.html)

## Optimized Language Core

What further differentiates **eval** from other mainstream languages, is that
we are able to maintain on par expressitivity and computational universality
while optimizing the language core to eliminate declarations as well as type
signatures of all kinds.

## Standard Library

The standard library defines four types

  - `()` (Unit type)
  - `String`,
  - `α -> ⁠β` (Function type),
  - `IO α` (Abstracts away side effects in the style of Haskell `IO`)

As well as three type classes `ApplicativeFunctor`, `Monad`, `Monoid`.

In addition there exists one object `eval` of type `String -> IO ()`. The
function evaluates the provided String as a javascript program.

## Eval is bootstrapped!

The **eval** compiler is completely written in **eval**. Bootstrapping a
compiler hase several advantages (Source: Wikipedia):

- it is a non-trivial test of the language being compiled, and as such is a form of dogfooding.
- compiler developers only need to know the language being compiled.
- compiler development can be done in the higher level language being compiled.
- improvements to the compiler's back-end improve not only general purpose programs but also the compiler itself.
- it is a comprehensive consistency check as it should be able to reproduce its own object code.

Thanks to the
expressitivity of the **eval** programming language, the compiler consists of
just *0.001 KLOC*. See `evalc.eval` to get an idea of advanced programming in eval.

## Hello World

Here comes the obligatory hello world example:

    eval("alert('Hello World!')")

## Syntax

**eval** syntax is actually quite simple and can be expressed by the following
EBNF:

    Program = Expression;
    Expression = FunctionCall | Identifier | Literal;
    FunctionCall = Expression, '(', Expression, ')';
    Identifier = 'eval';
    Literal = StringLiteral;
    StringLiteral = '"', { StringCharacter }, '"';
    StringCharacter = AnyCharacterExceptDoubleQuotes | '\', '"';

Whitespace is not allowed in **eval** outside of string literals.

## Type-Checker

Thanks to the optimized language core it is possible to implement the type
checking very efficiently in one phase together with the syntax analysis by
allowing only correctly typed programs to be parsed.

A top level expression has to be of type `IO ()`. There is only one expression
which satisfies this type. Namely `eval(x)` where `x` is of type `String`. Only
string literals are of type `String` which boils down to the following regular
expression which does all the necessary name resolutions and type checks:

    /eval\("([^"]|\\")*"\)/


## License

**eval** is copyright 2016 by Martin Ring

MIT License
