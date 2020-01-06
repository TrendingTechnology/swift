+++
author = ""
categories = ["Tips"]
date = 2020-01-05T16:03:00Z
description = "One of Swift’s lesser known, but incredibly powerful language features is how the ~= operator lets us implement custom pattern matching variants between different types."
featuredimage = ""
tags = ["key path"]
title = "Using key paths in switch statements"

+++
One of Swift’s lesser known, but incredibly powerful language features is how the `~=` operator lets us implement custom pattern matching variants between different types. Those new pattern matching capabilities can then be used in `switch` statements, when using `if case` syntax, or within any other context in which pattern matching is supported.

Here’s how we could use that language feature to define a `~=` overload that matches a boolean key path into a type against an instance of that type:

    func ~=<T>(rhs: KeyPath<T, Bool>, lhs: T) -> Bool {
        lhs[keyPath: rhs]
    }

With the above in place, we can now simply use a key path to define a pattern, and mix those patterns freely with those that match against a value — which is really useful when using a `switch` statement to decide how to parse or handle a given value:

    func handle(_ character: Character) {
        switch character {
        case "<":
            parseElement()
        case "#":
            parseHashtag()
        case \.isNumber:
            parseNumber()
        case \.isNewline:
            startNewLine()
        default:
            parseAnyCharacter()
        }
    }