---
title: "How ZKP are created"
date: 2022-02-12T12:36:37+08:00
draft: true
---

## The Major Steps

In this blog, we are going to review the major steps of the creation of
a ZKP.

Let's start with defining the problem.

We have a function $f$ (sometimes referred as the statement) such as
there is a set of public inputs ($I$), private inputs ($I'$)
and a set of outputs ($O$) for which

$$ f(I, I') = O $$

$I$ and $O$ are known and we want to prove that we have $I'$, without
revealing any information about $I'$ (except that it is a solution of course).

For example, in Zcash the zk snark statement for the output notes cover:
- Note integrity,
- Value commitment integrity,
- Decryption key integrity,
- and small order check

If these terms don't make sense yet, don't worry about it. But for example,
"Note integrity" means that the output note was formed correctly from the input
parameters: note value, recipient address.

The easiest one is the "decryption key integrity" which means that you know
the secret key that matches the public key used for decryption.
It can be expressed as an equality:

$$ \mathrm{epk} = \mathrm{esk}.g_d $$

The important thing to see is that this is a mathematical relation between
public values: epk and $g_d$, and the secret value esk.

($g_d$ is part of the address)
