---
title: "Finite Fields"
date: 2022-02-12T21:01:42+08:00
---

In one of the previous posts, we discussed finite sets: Sets with
a non infinite number of elements.

We also talked about functions from sets to sets and a particular
type of function that is quite useful, the 1 to 1 functions.
They map each element from the source set to exactly unique one element of
the destination set and vice-versa.

We can map any finite set to the set of integers from 0 to $n-1$, 
where $n$ is the number of elements of the set. It can be done by 
simply labeling elements as "first", "second", "third", etc.

From now on, we will only be interested in these finite sets: $N_p = [0, \dots, n-1]$

In it, we can define the classic addition and multiplication. The only difference is that
since the result exceeds must be in the set, we subtract or add multiples of $n$ until it does.

For example, if $n = 60$,

\begin{align}
10 + 20 & = 30 \\\\
45 + 15 & = 0 \\\\
45 + 30 & = 15 \\\\
45 + 45 & = 30 \\\\
\end{align}

You probably have recognized the behavior of minutes in the hour.

Multiplication works the same way:

\begin{align}
5 \times 10 & = 50 \\\\
10 \times 20 & = 20 \\\\
\end{align}

The last one is because $ 10 \times 20 = 200 = 180 + 20 = 60 \times 3 + 20 $. Multiples of 60 are discarded, 
so the result is $20$.

## Groups

$N_p$ with the + operator, form an algebric group: $(N_p, +)$. Because together they have a set of properties:
- there is neutral element: $0$,
- $+$ is associative: $(a + b) + c = a + (b + c)$,
- every element has an opposite: $a + (-a) = (-a) + a = 0$

These properties come from the underlying $+$ (the one that works in $N$).
The only remaining property to have is that $ a + b $ belongs to $N_p$.

## Commutative Group

If in $+$ also commutes, i.e, if $ a + b = b + a $, then $(N_p, +)$ is a commutative group.

## Sub-Group

$N_p$ can also contain groups that are made of elements of $N_p$. Such a group is called
a sub-group.

It's not always the case, but for instance can you find sub-groups of $N_{60}$ ?

If instead of taking every element of $N_{60}$, we take only $0, 10, 20, 30, 40, 50$
we have a sub-group.

The three properties above are clearly still met and we can also see that
whenever we add 2 of these numbers, the result is still among these numbers.

Can you find more sub-groups? 

Yes, in fact any divider of 60 forms a sub-group: 2, 3, 4, 5, 6, 10, 12, 15, 20, 30.

## Fields

Let's now consider the multiplication in combination with the addition.

$(N_p, +, \times)$

For this to be field, 
- $(N_p, +)$ is a commutative group with neutral element $0$,
- $(N_p, \times)$ is a commutative group with neutral element $1$,
- $\times$ distributes over $+$: $(a + b) \times c = a \times c + b \times c$

Again, nothing very special **but** this time $N_p$ is not always a field.
The problem is that the multiplicative inverse may not exist for every element of $N_p$.

In fact, $p$ must be a prime number or a power of a prime number.

When $N_p$ is a field, the convention is to use the letter F: $F_p$.

All the calculations in cryptography are performed in a finite field $F_p$.
$p$ is a very large prime number. For Bitcoin, $p$ is

\begin{align}
 p & = 2^{256} - 2^{32} - 2^9 - 2^8 - 2^7 - 2^6 - 2^4 - 1  \\\\
 & = 115792089237316195423570985008687907853269984665640564039457584007908834671663 \\\\
\end{align}

