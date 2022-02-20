---
title: "Hash Functions"
date: 2022-02-18T21:27:32+08:00
draft: true
---

Today, we are going to step away from maths and
work with operators that work on bits
to form Cryptographic Hash Functions.

But first of all, what is a crypto hash function and
why are they extremely useful?

Let's start with what they do.

A hash function is a function that takes as
an input a sequence of bits. It doesn't have
to be of a particular length. It could be 0, 1,
or 1000000 bits. It doesn't have to be a multiple
of anything. You can pretty much feed any stream
of data in any format to a hash function.

The output will always be a series of bits of
a given length, which depends on the hash function.

We'll be using SHA-256 in the remaining of the post and
therefore the output is exactly 256 bits long, or 32 bytes
long.

You may think that 32 bytes is not much, but in fact
this represents $2^{256}$ different results or
around $10^{77}$. Scientists estimate the number of atoms
in the universe at around $10^{80}$.

Knowing the range of the output is not enough though. 
We should make sure that the hash function uses the entire
domain and is not in reality restricted to a tiny fraction of it.

A hash function must have the following properties:

- it should be a deterministic function: given the same input bits,
it should give out the same result,
- it is "difficult" to revert. Again, "difficult" as in computationally
untractable. It would take million of years to do with the current state
of technology.
- it should be collision resistant. It is "difficult" to find two messages
that have the same hash. In other words, if someone gives you the hash
value for some data, that data is the *only* known input that gives that hash
- and last but not least, the output should behave as closely as possible
to a uniform random function. Every value of the output domain should
be reachable equally and it is "difficult" to predict where the hash
would be

You get bonus points for an easily computable hash function.





