Document number:	NXXXX

Date:	XXXX-XX-XX

Project:	Programming Language C++, Evolution Working Group

Reply-to:	Gonzalo Brito Gadeschi <gonzalobg88@gmail.com>

# Range-Based For-Loops: allow iterators with different types

## I. Introduction

In the draft [N4128 - Ranges for the Standard Library, Revision 1](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2014/n4128.html) section [3.3.5](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2014/n4128.html#an-iterables-end-may-have-a-different-type-than-its-begin) *Eric Niebler et al.* show that by allowing the begin and end iterators of a range to have different types, range-based libraries can be:

- more efficient,
- more powerful, and
- easier to implement. 
 
The current specification of range-based for loops does not accept begin and end iterators with different types. The users of these libraries have to resort to macros similar in spirit to `BOOST_FOREACH`. This does discourage users from experimenting with these libraries resulting in a situation that is not beneficial for the C++ community.

In the standardese section below it is shown that removing this restriction is a minor non-breaking change. This change is the only core language change required to support the Iterables specified in [N4128](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2014/n4128.html), see section [3.3.9](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2014/n4128.html#range-based-for-loop-is-changed-to-accommodate-sentinels).

## II. Standardese

In 6.5.4.1, replace: 

```c++
{
  auto && __range = range-init;
  for ( auto __begin = begin-expr,
        __end = end-expr;
        __begin != __end;
        ++__begin ) {
    for-range-declaration = *__begin;
    statement
  }
}
```

with

```c++
{
  auto && __range = range-init;
  auto __begin = begin-expr;
  auto __end = end-expr;
  for ( ; __begin != __end; ++__begin ) {
      for-range-declaration = *__begin;
      statement
  }
}
```


## III. Acknowledgements

The standarese was stated as is in [N4128](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2014/n4128.html). All kudos go to Eric Niebler, Sean Parent, and Andrew Sutton for that proposal, and to Eric Niebler for the [range-v3 library](https://ericniebler.github.io/range-v3/).

## IV. References

Eric Niebler, Sean Parent, and Andrew Sutton, [N4128 - Ranges for the Standard Library, Revision 1](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2014/n4128.html).

Eric Niebler's [Range-v3: Range algorithms, views, and actions for the Standard Library documentation](https://ericniebler.github.io/range-v3/).
