---
title: "Hash Functions"
date: 2022-02-18T21:27:32+08:00
weight: 50
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
of technology. It's also called first image resistant.
- it should be collision resistant. It is "difficult" to find two messages
that have the same hash. 
- it should be second image resistant: In other words, if someone gives you the hash
value for some data, that data is the *only* known input that gives that hash
- and last but not least, the output should behave as closely as possible
to a uniform random function. Every value of the output domain should
be reachable equally and it is "difficult" to predict where the hash
would be

You get bonus points for an easily computable hash function.

SHA-256 is a crypto hash function and fulfills all these conditions.

They are rather strong and prevents hashes from showing partial vulnerabilities
such as the ability to compute the hash of a modified message without
knowing the message itself.

For instance if you have $M$ and $H(M)$, a hash function
is vulnerable to the "length extension attack"
if it lets an attacker compute $H(M|x)$ without knowing $M$.

The | is the append operator. $M|x$ means adding $x$ to the end of $M$.

## Applications of Hash Functions

Hash Functions have many usages. Here are a few of them.

### File Integrity

If you know the hash a file, any modification in the file will
result in a different hash. Therefore after downloading a file
you can compute its hash and compare it with the expected value.
If they are different, the file was tampered.

### Digital Signature

This is related to the previous usage. When a digital signature
is applied on a document, it includes a hash of the document
with some signature parameters. The exact algorithm will be discussed
in a later post.

Many high level crypto algorithms include hashes as a building block.

### Password

When users register on a website with a password, the website typically
does not store it (or at least it should not). Instead, it keeps 
a hash of the password. Later on, when the user wants to login,
the website hashes the password used during login and compares the result
with the recorded hash. If they match, the user provided the correct password.

In case of a data breach, a hacker who gets a hold of the website user accounts
would not be able to gain access to the real passwords but only their hashes.
Since users often reuse the same password on multiple websites, it is paramount
that passwords are not kept in clear.

### Proof of Work

Crypto Hashes are used in Bitcoin POW because of their ability to produce
apparently random numbers yet deterministically. The probability to
produce a hash number in a given range is only proportional to the length
of the range. In particular, previous attempts provide no help in 
finding a proper input.

For instance, there is a $1/256$ chance to find a hash that begins with $00$.
Similarly to the $50/50$ chance of flipping head/tail.

But with a hash function, everyone can verify that the input has the desired
hash value.

### Commitments

Commitments are used in many cases. They all have one thing in common.
The party $P$ who makes the commitment $C$, declares that it will
use a value $V$ such has $C = H(V)$. It reveals $C$, effectively
preventing itself from picking a different value of $V$ later.

Eventually, $P$ shows $V$ and allows other parties to check that
$C = H(V)$. It guarantees that they $V$ was not changed after $C$
was revealed.

Commitments are particulary useful when several parties work together
and are both expected to provide values independently.

In this case, they all choose a $V_i$ and exchange $C_i$.
Then they can all reveal their $V_i$ making it impossible for one of the
$V_i$ to be picked after another.

## Merkle Tree

We saw how to make a commitment to a value by using a hash function.
What if we want to commit to a list of values: $L = (V_1, V_2, \dots, V_n)$?

Obviously, we can simply calculate the hash over the entire list like this:
$$ h = H(V_1|V_2|\dots|V_n) $$

We reveal the list $L$ and the verifier checks that the hash matches.

However, we often are not interested in the entire list. Instead, we
want to prove that our value $v$ belongs to the list and that we
are not adding it after the fact.

We still want to commit to the list but now, the verifier does not need
to check every element. It wants to verify that the element $v = V_i$.
Therefore the prover commits to $h$ then later shows $(v, i)$. The
verifier could check that $v = V_i$ and $h = H(V_1|V_2|\dots|V_n)$
if he is also given $(V_1|V_2|\dots|V_n)$.

Clearly, this method is not optimal. The prover would need to send the 
complete list to the verifier when only one of them is of interest.

With a Merkle Tree, the algorithm can be greatly improved at the cost
of more hash calculations.

The prover has the list $L = (V_0, V_1, \dots, V_{n-1})$. (Indexing from 0)

This time, it does not hash all of $L$. Instead, it
pairs elements of $L$ and computes hashes on each pair.

$$h_i = H(V_{2i}, V_{2i+1})$$

If V has an odd number of elements, the list is padded with
a predesignated value to make it even.

It creates a new list of values $(h_0, h_1, \dots, h_i)$
