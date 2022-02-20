---
title: "Group"
date: 2022-02-09T20:28:08+08:00
draft: true
---

## Relations

In the previous post, we talked about sets and the 
simple operations you can perform with them:
union, intersection, membership check, etc.

Today, we are going to discuss relation between 
set elements.

Let's give ourselves a couple of sets to work with.

In set A, we have a few letters: a, b, c, d, e
and in set B, we have a few numbers: 1, 2, 3, 4

We make a relation "R" by associating an element of A
to an element of B.

There is only one rule:
> You need to connect *one* element of A to *one* element of B

Anything else is allowed. For instance, some elements of A may
be unconnected and the same thing may apply for elements of B.
Or an element of one set can connect to more than one element
of the other set.

Relations don't have a particular direction. 

For example of a relation, we have equality but really, it could
be anything.

## Functions

Now, we choose one of the set as the starting set and the other
one is the destination. With functions, there is a direction.
> An element of the source set
*cannot* be associated to more than one element in the destination set.
It is "the" value of the function for a given element.

Therefore we can write the target of a function $f$ as
$ f(x) $

Let's look at a few examples.

Here's the definition of a function.

Do you notice something special?

The function maps values from the source set to different values in the
destination set. In other words, 

$$ \forall (x,y), x \ne y \Rightarrow f(x) \ne f(y) $$
$$ f(y) $$

Such function is called "injective". Injective functions are
particularly interesting because the reverse of relation, i.e
going from destination to the source is itself a function.

Moreover, when you have a function like this, you can
transform elements of the first set, $A$ into elements
of the destination set $B$.

Suppose you want to encrypt elements of $A$ but there
is no known good way for that in $A$. However, you know how
to do it in $B$. Usually $B$ is a set of integers because
they are extensively studied.

> Using a function to transform a problem from one domain
to another is commonly used and is a fundamental technique
we should remember.

We are going to see it several times so let's finish
on this point.
