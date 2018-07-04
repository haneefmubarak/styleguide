C (language)
============

The Basics
----------

### Characters / Encoding:
 - Use only the basic ASCII set (no extended characters)
 - Escape all other characters as needed
 - When possible, use idiomatic escapes (ie: `'\n'` for a line-feed)
 - Otherwise, use the hexadecimal representation of a character (ie: `0x04` for end-of-transmission)

### Indentation:
 - Use hard tabs
 - Tabs should be configured to display as `8` (eight) spaces

### Window:
 - Consider the window to be `50 x 100` (fifty rows by one-hundred columns)
 - This means that the code should be shorter than with window-width of 100 characters
 - It also means that you should tradeoff between being verbose and concise to maximize readability
   	relevance within any given window-height of 50 lines

Functions
---------

### Declarations

All non-`static` functions should be declared prior to use, usually in a header file. The
declaration and surrounding comments should concisely and precisely document the purpose and
arguments of a given function and/or set of similar/related functions. This is further elaborated
upon in [HeaderFiles].

 - Always `typedef` return values as needed; you should not form complex types in the declaration
 - Functions returning a function pointer may *sometimes* be an exception to this, exercise caution
 - If needed, `typedef` arguments; this rule is more flexible, please utilize good judgement
 - Almost invariably, a function should not have more than `8` (eight) arguments; strongly consider
   	`typedef`-ing one or more `struct`s to pass the relevant arguments in such a case
 - When reasonably feasible, mark arguments that are pointers as `const`
 - If there are multiple non-`const` arguments that are pointers to the same or compatible types,
   	use `restrict` on each of said arguments where it can be predetermined that said argument
   	will never point to or within the same object or array thereof as any of the other
   	arguments of the same or compatible types.
 - When a`struct` being passed in is simple (less-than-or-equal to `8` (eight) total basic-type
   	members), lively (less-than-or-equal to `2` (two) basic-type members will be unused by
   	the callee), and is not `const`, consider passing said `struct` directly by value
 - Otherwise, pass the `struct` by reference (pointer)
 - If the return value is a `struct` that is not trivial (less-than-or-equal to `2` (two) total
   	basic-type members), consider returning via reference in an argument or returning a pointer
   	to the heap (`malloc()`; for particularly large structs)
