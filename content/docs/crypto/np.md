---
title: "Hard Problems?"
date: 2022-02-13T11:52:10+08:00
weight: 20
---

Today we are going to discuss problem complexity.
We often hear "This problem is too hard for current
computer hardware, or this has an exponential growth..."

It is used so frequently that sometimes we lose track
of the real meaning of these terms, so today we want
to clarify definition because it is quite important
in the future discussions about algorithms.

First of all, let's talk about functions of one variable
$x$ over real numbers.

For example, $f(x) = x^2+5$.

We want to know how $f$ behaves as $x$ gets bigger.
That's called the "asymptotic" behavior of $f$.

In our example, $f$ grows indefinitively as $x$ grows, i.e
$f$ goes to the *infinity*. 
When something does that, we say it diverges.

That's the case for most of
the functions we will see, but the question is how fast
does $f$ grow?

For that, we need other well known functions to compare $f$ with.

## Polynomials

One of the possible choices are functions of the form 
$P_n(x) = x^n$ for some fixed value $n$ (it does not depend on $x$).

Then we calculate $ f / P_n $ and we determine if the result still
grows to the infinity or it eventually stops.

For $n=1$, 
$$f / P_1 = (x^2+5)/x = x + 5/x $$

Now the term $5/x$ will gets smaller and smaller as $x$ grows,
so the remaining interesting term is just $x$. That is still
going to the infinity. We need to increase $n$.

For $n=2$, $$f / P_2 = (x^2+5)/x^2 = 1 + 5/x^2 $$

$5/x^2$ gets smaller even faster so we can ignore it for
our asymptotic analysis and we can say that $f/P_2 <= 1 + 5$,
when $x >= 1$. $f/P_2$ does not diverge anymore.

We can say $f$ behaves asymptotically like $x^2$.
And write it as

$$ f = O(x^2) $$

If we continue to increase $n$, then we can see that $F/P$
now, not only is bounded but is going to $0$.

For example for $n=3$, $f/P_3 = 1/x + 5/x^3$ and this goes to $0$.

When there is a value for $n$ such as $ f = O(x^n) $, $f$ is 
said to have polynomial growth.

In computer science, problems are classified by how many
steps it takes to find a solution.

They come with a factor that represents their size.
For instance for the problem: "sort a list of numbers". The
size parameter is "how long is the list?". 

Let's say the list has $n$ numbers, what's the best algorithm?
Well, best is not very clear. Best by what? space used? time used?
in which case?
Then if we want a rough measure, we look at the asymptotic behavior.

## Bubble Sort

Bubble Sort is a simple sorting algorithm that works as follows:
- Go through the list, one by one, and swap two adjacent numbers
if they are out of order
- Repeat step 1 if at least two elements had to be swapped.

Example: with 1, 4, 2.
- First pass: 
  - compare 1, 4: no need to swap
  - compare 4, 2: swap. The list becomes 1, 2, 4
- Do a second pass because we had to swap something
  - compare 1, 2: no swap
  - compare 2, 4: no swap
- Finish because there was no swap. The list is sorted: 1, 2, 4.

Let's call $S(n)$ the number of steps that Bubble Sort takes to complete sorting a list of $n$ numbers.

$S = O(n^2)$ in the worst case and $S = O(n)$ in the best case.

It means that even if you give the best list of numbers to 
the Bubble Sort algorith, it will take a number of steps that is
proportional to the length of the list. And if you give it the
worst list, then it will take a number of steps that is proportional
to the square of the number of elements.

The best and worst lists depend on the algorithm but since in 
many case we don't get to choose it, we want to know how the
algorithm behaves in both cases.

For Bubble Sort, the best case is if the list is already sorted.
A worst case is when the smallest element of the list is in the 
last position. One pass only moves it by one step towards to head.

## Exponential Growth

Another class of functions is the exponential functions.

Polynomial functions have the form $ x^n $ for some constant $n$.

Exponential functions have the form $ n^x $ for some constant $n$.

We just swapped the $x$ and the $n$. That makes a huge difference.

For any value of $n > 1$, regardless how close it is to 1, 
$n^x$ will eventually outgrow $x^n$. For example, 

you can choose n=1.1
in $x^n$ and n=10 in $x^n$, the former will outgrow the later.

$1.1^{x} > x^{10}$ asymptotically (for values of $x$ large enough).
At around 700, the former overcomes the later and outpaces it very 
quickly after.

Incidentally, if you take a process that grows by a factor
at every step, the result is an exponential growth.

Let's say you have a disease that spreads to 10% more people
every month, it is $O(1.1^x)$

## Logarithmic Growth

Logarithmic is the inverse of exponential. If you have a function
$ y = O(n^x) $ then there is a $m$ such as $ x = \log_m(y) $

Maybe an example will help. Let's say $f(n)$ is the function that gives
the largest number that can be written with $n$ digits.

\begin{align}
f(1) &= 9 \\\\
f(2) &= 99 \\\\
f(5) &= 99999 \\\\
\end{align}

$f$ is not defined for values $x$ that are not integers. In other
words, $f(1.5)$ does not exist because $1.5$ digits does not mean
anything. But we can extend $f$ to values between integers.

$$ g(x) = 10^x - 1 $$

We can see that when x is in integer $f(x) = g(x)$.

Now, the reverse of $f$ is "how many digits do I need to write
this number?"

\begin{align}
f_i(9) &= 1 \\\\
f_i(99) &= 2 \\\\
f_i(99999) &= 5 \\\\
\end{align}

$f_i$ still grows to the infinity but its growth is very slow.
When x is multiplied by $10$, $f$ only grows by $1$.

Indeed $$f_i(x) = \left\lfloor \log_{10}(x+1) \right\rfloor $$

These are the three major classes of comparison functions: Polynomial, Exponential and Logarithmic.

But there are many others, we just don't encounter them as often as
these three.

## Problem Complexity

Back to our original question: What is a hard problem?

We can say: For this problem, the best algorithm we have will solve
it in $S(n)$ steps where $n$ is the "size".

For sorting a list, we have an algorithm (Bubble Sort) that does it in
$O(n^2)$ steps. But is it the best we can do?

Turns out, no. We can do better. There are algorithms that
can sort a list in $O(n\log n)$ steps.

Therefore sorting a list has $n\log n$ complexity. Because
$n\log n < n^2$, this problem has **polynomial complexity**

## Solving vs Verifying

So far we only considered the complexity of a solving algorithm.
If you are just interested in verifying a solution that was
given to you, the algorithm may be easier.

In the sorting example, Bubble sort has $O(n^2)$ complexity but
to check if a list is sorted, you just need to go through the items
and make sure that every element is less than the next one.
That can be done in $O(n)$ steps.

Problems that can be solved in polynomial time belong to the 
class **P**.

Problems that can be verified in polynomial time and can be solved
by brute force (i.e. trying everything) belong to the class **NP**.

The hardest problems in the **NP** class are called **NP-complete** 
problems. 

An NP-complete problem is such that *any* NP problem can be transformed
to it in polynomial time. Unfortunately, there are many useful NP-complete
problems

A popular example is the map coloring problem. Given a map of "countries",
i.e. a 2-D set of connected regions, color each region so that
no two regions with the same color share a border. You may only use 4 colors.

It is possible for any map but it is a NP-complete problem.

## In the context of ZK-Proofs

With ZK-Proofs, we have two parties involved. The Prover,
who has a solution and needs to produce a proof.
The verifiers who receives the proof and wants to verify it.

Generally speaking, we accept that the prover has to do 
additional work besides finding the solution in order to
calculate the proof but the verifier should do much less
work than solving the problem.

