---
title: "RSA - Our First Cryptosystem"
date: 2022-02-16T14:27:51+08:00
---

RSA is a public/private key cryptosystem
widely used currently.

With the knowledge of finite fields we
acquired, we can understand how it works.

We will not be able to prove that it is
safe against code breaking but generally
speaking, cryptoanalysis is beyond our scope.

The first step of any cryptosystem is key generation.

## Key Generation

First you pick two prime numbers $p$ and $q$.
Normally these would be very large but we are
gonna use $p=3$ and $q=5$ for now.

By the way, a prime number is an integer that
has *exactly* two dividers: 1 and itself.

For example, 2 is a prime number. So is 3, 5 and 7.
But 4 is not a prime number because $2 \times 2 = 4$.
1 is not a prime number because it has only one divider.

Now calculate $$n = pq$$
$n = 3 \times 5 = 15$.

Also calculate $$N = (p-1)(q-1)$$
$N = 2 \times 4 = 8$

$N$ should be kept secret.

Choose $e$ such as $e$ and $N$ don't have any divider
in common.

We pick $e = 3$

Find the inverse of $e$ in $F_N$. 

$$ de = 1 \pmod N $$

$d \times 3 = 1 \pmod 8 \implies d = 3$ because
$3 \times 3 = 9 = 1 \pmod 8$

The public key is $(n, e)$, i.e $(15, 3)$
and the secret key is $d$. 

$N$, $p$ and $q$ can be
discarded.

## Encryption and Decryption

You can encrypt using either $e$ or $d$
and decrypt with the other key. They can be
used interchangibly. We know $n$ because it is
part of the public key.

Suppose we use $e$ (and $n$)

To encrypt a message $m$, we calculate
$$ c = m^e \pmod n $$

To decrypt the cypher $c$, we do the same but with
other other key
$$ m = c^d \pmod n $$

Let's say $m = 2$. $$ c = 2^3 = 8 \pmod{15} $$

Then to decrypt, we calculate $c^3$ because $d=3$ (it's
a coincidence that $d=e$).

$$ 8^3 = 512 = 2 + 34 \times 15 = 2 \pmod{15} $$

and we got back our message $m$.

## Proof that it works

Basically, we have to prove that $$ c ^ d = m \pmod n $$

Put together,

\begin{align}
c &= m^e \pmod n \\\\
m'&= c^d \\\\
m'&= c^d \\\\
  &= (m^e)^d \\\\
  &= m^{ed} \\\\
\end{align}

and we want to prove that $m'=m$.

To do so, we are going to use a theorem
called Fermat's Little Theorem.

For any $a$ and prime $p$,
$$ a^{p-1} = 1 \pmod p $$

\begin{align}
m^{ed} &= m \pmod n \\\\
m^{ed} - m &= 0 \pmod n \\\\
&= kn \\\\
&= kpq \\\\
\end{align}

\begin{align}
m^{ed} &= m \pmod p\quad \mathrm{and} \\\\
m^{ed} &= m \pmod q \\\\
\end{align}

Let's prove the first equation. The second has the
same proof since $p$ and $q$ have the same properties.

If $m = 0 \pmod p$, $p$ divides $m$. $m^{ed}$ is
a multiple of $m$, therefore $p$ divides $m^{ed}$ too.
Then $m' = m^{ed} = 0 \pmod p$, and $m' = m$.

If $m \ne 0 \pmod p$, $m^{ed} = m^{ed-1}m$.

But $ed = 1 \pmod N$, therefore there is a $k$ 
such as $ed = kN + 1$

$$m^{ed-1} = m^{kN} = m^{k(p-1)(q-1)} = {m^{p-1}}^{k(q-1)}$$

$$ m^{p-1} = 1 \pmod p $$
So
$$ m^{ed-1} = {m^{p-1}}^{k(q-1)} = 1^{k(q-1)} = 1 \pmod p$$
Then
$$ m' = m^{ed} = m $$

All that is left to do is to prove Fermat's Little Theorem.

## Fermat Little Theorem Proof

Since $p$ is prime, $F_p$ is a field and ${1, 2, ..., p-1}$ form a group.

We saw earlier that the only tricky part is to prove
that every element of $F^*_p$ has an inverse.
We'll leave it aside because it is a bit more complex.

Let's consider ${1, a, a^2, ...}$ until it eventually
loops around (it has to because we have a finite 
number of elements). The lowest $k$ such as $a^k = 1$
is called the order of $a$ relative to $\times$.

We also so earlier that every sub group of a group
has a count of elements (cardinality)
that divides the cardinality of the group, here $p-1$.

$$ a^{p-1} = a^{kn} = 1^n = 1 \pmod p $$

## Proof that $F^*_p$ is a group

We use Beyzout's Lemma:

Given $a$ and $b$ and their greatest common divider $d$,
there are $x$ and $y$ such as

$$ ax + by = d $$

$x$ and $y$ are positive or negative integers.

The proof uses a common technique of algebra. Any non empty set of positive numbers has a smallest element.

If we consider $S = \left\\{ ax + by, \text{ such as } ax + by > 0 \right\\}$, it is not empty (it contains $a$ and $b$) therefore it has a smallest element $d$.

It turns out $d$ is the greatest common divider of $a$ 
and $b$.

If we divide $a$ by $d$, 

$$ a = dq + r $$

$q$ is the quotient and $r$ is the remainder. $r >= 0$

Then $r = a - dq = a - (ax+by)q = a(1-xq) -byq $

$r$ has the form $ax + by$ and hence $r = ax+by \ge 0$
which means $ r \in S \cup \\{0\\} $.
We also know $r < d$. So $r$ cannot be in $S$ since 
it's smaller than the smallest element of $S$.
Then it must be that $r = 0$ and $a = dq$.

$d$ divides $a$.

Likewise, we can prove than $d$ divides $b$.
$d$ is a common divider of $a$ and $b$.

Now we need to prove that it is the greatest common
divider.

Let's take any common divider $c$, $a = uc$ and $b = vc$

Then $$d = ax + by = ucx + vcy = (ux + vy)c $$

And $c$ divides $d$. Therefore $c \le d$.

By applying this lemma to our case, we can say
that there are $x$ and $y$ such as 

$$ ax + py = 1 $$

because $p$ is prime and the greatest common divider
of $a$ with a prime is 1.

This is the same as saying

$$ ax = 1 \pmod p $$

And $x$ is the inverse of $a$.

