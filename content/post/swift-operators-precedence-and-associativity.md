+++
author = ""
categories = ["Tutorial"]
date = 2020-01-05T16:05:00Z
description = "Operators are what do the work of a program. They are the very execution of an executable; the teleological driver of every process. "
featuredimage = "https://res.cloudinary.com/diqqalzsx/image/upload/v1578315121/static/swift/swift-operators_vkyvni.jpg"
tags = ["Operator"]
title = "Swift Operators Precedence and Associativity"

+++
What would a program be without operators? A mishmash of classes, namespaces, conditionals, loops, and namespaces signifying nothing.

Operators are what do the work of a program. They are the very execution of an executable; the teleological driver of every process. Operators are a topic of great importance for developers and the focus of this week’s NSHipster article.

## Operator Precedence and Associativity

If we were to dissect an expression — say `1 + 2` — and decompose it into constituent parts, we would find one operator and two operands:

| 1 | + | 2 |
| --- | --- | --- |
| left operand | operator | right operand |

Expressions are expressed in a single, flat line of code, from which the compiler constructs an ast, or abstract syntax tree:

![1 + 2 AST](https://nshipster.com/assets/swift-operators-one-plus-two-8d9f1b1c942b777c400c285fef0b38e53ce8e9482290bfbe42575e3c25d527ed.svg)

For compound expressions, like `1 + 2 * 3` or `5 - 2 + 3`, the compiler uses rules for operator precedence and associativity to resolve the expression into a single value.

Operator precedence rules, [similar to the ones you learned in primary school](https://en.wikipedia.org/wiki/Order_of_operations), determine the order in which different kinds of operators are evaluated. In this case, multiplication has a higher precedence than addition, so `2 * 3` evaluates first.

| 1 | + | (2 * 3) |
| --- | --- | --- |
| left operand | operator | right operand |

![1 + 2 * 3 AST](https://nshipster.com/assets/swift-operators-one-plus-two-times-three-2bdfce3bb4459856b30f01fa80a5ef8bc64990f2767ddd5c82e662cf9192432c.svg)

Associativity determines the order in which operators with the same precedence are resolved. If an operator is left-associative, then the operand on the left-hand side is evaluated first: (`(5 - 2) + 3`); if right-associative, then the right-hand side operator is evaluated first: `5 - (2 + 3)`.

Arithmetic operators are left-associative, so `5 - 2 + 3` evaluates to `6`.

| (5 - 2) | + | 3 |
| --- | --- | --- |
| left operand | operator | right operand |

![5 - 2 + 3 AST](https://nshipster.com/assets/swift-operators-one-plus-two-plus-three-5863742dd5d28bc65cebf9f5781274fef3bc55c5d917a78e63fb4f5ba999079f.svg)

## Swift Operators

The Swift Standard Library includes most of the operators that a programmer might expect coming from another language in the C family, as well as a few convenient additions like the nil-coalescing operator (`??`) and pattern match operator (`~=`), as well as operators for type checking (`is`), type casting (`as`, `as?`, `as!`) and forming open or closed ranges (`...`, `..<`).

### Infix Operators

Swift uses infix notation for binary operators (as opposed to, say [Reverse Polish Notation](https://en.wikipedia.org/wiki/Reverse_Polish_notation)). The Infix operators are grouped below according to their associativity and precedence level, in descending order:

| BitwiseShiftPrecedence |
| --- | --- |
| << | Bitwise left shift |
| >> | Bitwise right shift |
| MultiplicationPrecedence |
| * | Multiply |
| / | Divide |
| % | Remainder |
| &* | Multiply, ignoring overflow |
| &/ | Divide, ignoring overflow |
| &% | Remainder, ignoring overflow |
| & | Bitwise AND |
| AdditionPrecedence |
| + | Add |
| - | Subtract |
| &+ | Add with overflow |
| &- | Subtract with overflow |
| \| | Bitwise OR |
| ^ | Bitwise XOR |
| RangeFormationPrecedence |
| ..< | Half-open range |
| ... | Closed range |
| CastingPrecedence |
| is | Type check |
| as | Type cast |
| NilCoalescingPrecedence |
| ?? | nil Coalescing |
| ComparisonPrecedence |
| < | Less than |
| <= | Less than or equal |
| > | Greater than |
| >= | Greater than or equal |
| == | Equal |
| != | Not equal |
| === | Identical |
| !== | Not identical |
| \~= | Pattern match |
| LogicalConjunctionPrecedence |
| && | Logical AND |
| LogicalDisjunctionPrecedence |
| \|\| | Logical OR |
| DefaultPrecedence |
| AssignmentPrecedence |
| = | Assign |
| *= | Multiply and assign |
| /= | Divide and assign |
| %= | Remainder and assign |
| += | Add and assign |
| -= | Subtract and assign |
| <<= | Left bit shift and assign |
| >>= | Right bit shift and assign |
| &= | Bitwise AND and assign |
| ^= | Bitwise XOR and assign |
| \|= | Bitwise OR and assign |
| &&= | Logical AND and assign |
| \|\|= | Logical OR and assign |

Operator precedence groups were originally defined with numerical precedence. For example, multiplicative operators defined a precedence value of 150, so they were evaluated before additive operators, which defined a precedence value of 140.

In Swift 3, operators changed to define precedence by partial ordering to form a dag or [directed acyclic graph](https://en.wikipedia.org/wiki/Directed_acyclic_graph). For detailed information about this change, read Swift Evolution proposal [SE-0077 “Improved operator declarations”](https://github.com/apple/swift-evolution/blob/master/proposals/0077-operator-precedence.md).

### Unary Operators

In addition to binary operators that take two operands, there are also unary operators, which take a single operand.

#### Prefix Operators

Prefix operators come before the expression they operate on. Swift defines a handful of these by default:

* `+`: Unary plus
* `-`: Unary minus
* `!`: Logical NOT
* `~`: Bitwise NOT

For example, the `!` prefix operator negates a logical value of its operand and the `-` prefix operator negates the numeric value of its operand.

    !true // false
    -(1.0 + 2.0) // -3.0
    

The increment/decrement (`++` / `--`) operators were removed in Swift 3. This was one of the first changes to be made as part of the [Swift Evolution process](https://github.com/apple/swift-evolution) after the language was released as open source. In [the proposal](https://github.com/apple/swift-evolution/blob/master/proposals/0004-remove-pre-post-inc-decrement.md), Chris Lattner describes how these operators can be confusing, and argues for why they aren’t needed in the language.

### Postfix Operators

Unary operators can also come after their operand, as is the case for the postfix variety. These are less common; the Swift Standard Library declares only the open-ended range postfix operator, `...`.

    let fruits = ["🍎", "🍌", "🍐", "🍊", "🍋"]
    fruits[3...] // ["🍊", "🍋"]
    

### Ternary Operators

The ternary `?:` operator is special. It takes three operands and functions like a single-line `if-else` statement: evaluate the logical condition on the left side of the `?` and produces the expression on the left or right-hand side of the `:` depending on the result:

    true ? "Yes" : "No" // "Yes"
    

In Swift, `TernaryPrecedence` is defined lower than `DefaultPrecedence` and higher than `AssignmentPrecedence`. But, in general, it’s better to keep ternary operator usage simple (or avoid them altogether).

## Operator Overloading

Once an operator is declared, it can be associated with a type method or top-level function. When an operator can resolve different functions depending on the types of operands, then we say that the operator is overloaded.

The most prominent examples of overloading can be found with the `+` operator. In many languages, `+` can be used to perform arithmetic addition (`1 + 2 => 3`) or concatenation for arrays and other collections (`[1] + [2] => [1, 2]` ).

Developers have the ability to overload standard operators by declaring a new function for the operator symbol with the appropriate number and type of arguments.

For example, to overload the `*` operator to repeat a `String` a specified number of times, you’d declare the following top-level function:

    func * (lhs: String, rhs: Int) -> String {
        guard rhs > 0 else {
            return ""
        }
    
        return String(repeating: lhs, count: rhs)
    }
    
    "hello" * 3 // hellohellohello
    

This kind of language use is, however, controversial. (Any C++ developer would be all too eager to regale you with horror stories of the non-deterministic havoc this can wreak)

Consider the following statement:

    [1, 2] + [3, 4] // [1, 2, 3, 4]
    

By default, the `+` operator concatenates the elements of both arrays, and is implemented using a generic function definition.

If you were to declare a specialized function that overloads the `+` for arrays of `Double` values to perform member-wise addition, it would override the previous concatenating behavior:

    // 👿
    func + (lhs: [Double], rhs: [Double]) -> [Double] {
        return zip(lhs, rhs).map(+)
    }
    
    [1.0, 3.0, 5.0] + [2.0, 4.0, 6.0] // [3.0, 7.0, 11.0]
    

Herein lies the original sin of operator overloading: **ambiguous semantics**.

It makes sense that `+` would work on numbers — that’s maths. But if you really think about it, _why should adding two strings together concatenate them_? `1 + 2` isn’t `12` ([except in Javascript](https://www.destroyallsoftware.com/talks/wat)). Is this really intuitive? …or is it just _familiar_.

Something to keep in mind when deciding whether to overload an existing operator.

By comparison, PHP uses `.` for string concatenation, whereas SQL uses `||`; Objective-C doesn’t have an operator, per se, but will append consecutive string literals with whitespace.

## Defining Custom Operators

One of the most exciting features of Swift (though also controversial) is the ability to define custom operators.

Consider the exponentiation operator, `**`, found in many programming languages, but missing from Swift. It raises the left-hand number to the power of the right-hand number. (The `^` symbol, commonly used for superscripts, is already used by the [bitwise XOR](https://en.wikipedia.org/wiki/Bitwise_operation#XOR) operator).

Exponentiation has a higher operator precedence than multiplication, and since Swift doesn’t have a built-in precedence group that we can use, we first need to declare one ourselves:

    precedencegroup ExponentiationPrecedence {
        associativity: right
        higherThan: MultiplicationPrecedence
    }
    

Now we can declare the operator itself:

    infix operator ** : ExponentiationPrecedence
    

Finally, we implement a top-level function using our new operator:

    import Darwin
    
    func ** (lhs: Double, rhs: Double) -> Double {
        return pow(lhs, rhs)
    }
    
    2 ** 3 // 8
    

We need to import the Darwin module to access the standard math function, `pow(_:_:)`. (Alternatively, we could import Foundation instead to the same effect.)

When you create a custom operator, consider providing a mutating variant as well:

    infix operator **= : AssignmentPrecedence
    func **= (lhs: inout Double, rhs: Double) {
        lhs = pow(lhs, rhs)
    }
    
    var n: Double = 10
    n **= 1 + 2 // n = 1000
    

### Use of Mathematical Symbols

A custom operator can use combinations of the characters `/`, `=`, `-`, `+`, `!`, `*`, `%`, `<`, `>`, `&`, `|`, `^`, or `~`, and any characters found in the [Mathematical Operators](https://en.wikipedia.org/wiki/Mathematical_Operators) Unicode block, among others.

This makes it possible to take the square root of a number with a single `√` prefix operator:

    import Darwin
    
    prefix operator √
    prefix func √ (_ value: Double) -> Double {
        return sqrt(value)
    }
    
    √4 // 2
    

Or consider the `±` operator, which can be used either as an infix or prefix operator to return a tuple with the sum and difference:

    infix operator ± : AdditionPrecedence
    func ± <T: Numeric>(lhs: T, rhs: T) -> (T, T) {
        return (lhs + rhs, lhs - rhs)
    }
    
    prefix operator ±
    prefix func ± <T: Numeric>(_ value: T) -> (T, T) {
        return 0 ± value
    }
    
    2 ± 3 // (5, -1)
    
    ±4 // (4, -4)
    

For more examples of functions using mathematical notation in Swift, check out [Euler](https://github.com/mattt/Euler).

Custom operators are hard to type, and therefore hard to use, so exercise restraint with exotic symbols. Code should be typed, not be copy-pasted.

When overriding or defining new operators in your own code, make sure to follow these guidelines:

1. Don’t create an operator unless its meaning is obvious and undisputed. Seek out any potential conflicts to ensure semantic consistency.
2. Pay attention to the precedence and associativity of custom operators, and only define new operator groups as necessary.
3. If it makes sense, consider implementing assigning variants for your custom operator (e.g. `+=` for `+`).