+++
author = ""
categories = ["Tips"]
date = 2020-01-05T16:03:00Z
description = "In Swift, it’s possible to satisfy a throwing function protocol requirement using a non-throwing function, which can be very useful in certain situations."
featuredimage = ""
tags = ["protocol "]
title = "Implementing throwing protocol functions as non-throwing"

+++
In Swift, it’s possible to satisfy a throwing function protocol requirement using a non-throwing function, which can be very useful in certain situations. For example, let’s say that we’ve defined a protocol for parsers that enable us tokenize a string in some way:

    protocol TokenParser {
        func parseToken(from string: String) throws -> Token
    }

While certain implementations of the above protocol will need to throw, that won’t necessarily be true for all conforming types. For example, the below `KeywordParser` throws, while `TextParser` doesn’t:

    struct KeywordParser: TokenParser {
        func parseToken(from string: String) throws -> Token {
            ...
        }
    }
    
    struct TextParser: TokenParser {
        // This will satisfy our protocol requirement, even though
        // this implementation doesn't actually throw:
        func parseToken(from string: String) -> Token {
            ...
        }
    }

Since the original declaration of our protocol function is marked as throwing, we’ll always need to call it with `try` when the exact conforming type isn’t known — regardless of whether the underlying implementation _actually_ throws:

    let parsers: [TokenParser] = ...
    
    for parser in parsers {
        // Since all we know about each parser within this iteration
        // is that it conforms to our 'TokenParser' protocol, we'll
        // need to use 'try' when calling its function:
        let token = try parser.parseToken(from: string)
    }

However, when dealing with a non-throwing conforming type directly, we can now omit the `try` keyword — even though the original protocol requirement was marked as throwing:

    let parser = TextParser()
    let text = parser.parseToken(from: string)

It’s a small feature, but the fact that we can implement a throwing function requirement using a non-throwing one gives us a slightly greater degree of flexibility when conforming to protocols that contain such functions.