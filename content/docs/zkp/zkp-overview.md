---
title: "Zero Knowledge Proof Overview"
date: 2022-02-10T11:04:58+08:00
weight: 10
---

We are going to spend quite some time discussing crypto,
maths and computer science so it is worth taking some
time to put things in perspective.

We are mostly interested in crypto currencies and
one of the main valuable properties is **decentralization**.

## Decentralization

When the system is centralized, there is a main entity
that oversees the entire management and operation.
Users implicitly trust this entity since anyway they
are not in charge of anything and most likely don't
have access to the records that would allow them to 
perform any verification.

However, if the system is decentralized, there are 
several or potentially a very large number of entities
that together make sure the system operates properly.

Moreover some system allow anyone to participate as
an management entity therefore they cannot be trusted
because noone is in the position of overseeing their 
honesty.

## Enter Crypto

Enter cryptography. Before cryptocurrencies, it was
mostly about encrypting and decrypting messages
but there is another very important application of
cryptography: Authentication.

And this was made possible with Public/Private Crypto.

### Public/Private Crytpo

In traditional crypto, you have a key, i.e. a secret
value that the sender and the receiver both know
but keep private.

The same secret value is used for encrypting and
decrypting. It is called *symetric* crypto.

With public/private crypto or *asymetric* crypto,
there are two keys: the secret key and the public key.

The public key can be easily derived from the secret key
but the other way is impossible (or practially impossible
with current technology for decades).

Messages are encrypted with the public key but they
can only be decrypted with the secret key. With this system,
the public key can be distributed so that the receiver
can get encrypted messages from anyone and yet be the
only person able to read them.

That's one of the application of public/private crypto.

The other popular application is authentication. These
crypto system have the ability to be used in "reverse":
Messages are encrypted with the secret key and
decrypted with the public key. One can prove his identity
but showing he/she knows the secret key that matches
a given public key. To do so, he/she encrypts a known
message with the secret key. When it gets decrypted
with the public key, we get back the original known message.
The actual process has more steps but in essence, making a *digital
signature* can be boiled down to this technique.

This is a zero knowledge proof.

We **proved** we know the secret key and therefore our identity,
while not revealing any information that could help other
parties discover the secret key. 

Cryptocurrencies are mainly using this form of cryptography
and very seldom the traditional encryption/decryption.

This is because they tend to put the focus on being trustless
rather than privacy. When you want to be trustless, you want
to allow anyone to verify your claims. But also, you don't
want to reveal your secrets. That's why Zero Knowledge Proofs
are gaining more and more traction.

## Smart Contracts

Though authentication or signatures are quite useful and 
are indeed in big part of the cryptocurrencies, i.e. Bitcoin
only uses digital signatures, there is a push towards extending
cryptocurrencies to more than tracking account balances.

The first cryptocurrency that introduced "smart contracts" is
Ethereum. Smart contracts are general programs which are
executed by many computers. With Bitcoin, computers deal with
account transactions, which are a specific type of program.

An account transaction transfers coins between sources and destinations.
Whereas a smart contract can be made to do more varied tasks.

## Sudoku contract

Suppose you have a Eth smart contract that implements the rules of Sudoku.
A puzzle has a set of given digits and the smart contract
verifies that the submitted solution is correct.
If it is, the contract could unlock some funds and reward the account
that submitted the solution.

All the computers in the Eth network perform the verification.
One of the core principle of a crypto currency system is that 
all the participants agree on the same state: Either the solution is
correct and the funds are paid, or the solution is incorrect and the
solution is rejected.

However, what if the person who found the solution does not want
to show it. Most likely, since we can't simply trust his word that
he has a valid solution, he will not get paid.

So it's either: 
- show me the solution and get paid, but then the solution is revealed
to the entire world,
- keep the solution but don't get paid

## Zero Knowledge Proofs

Zero Knowledge Proofs allow someone to prove that he has a solution
without revealing it.

In this hypothetical case, the verifiers are not interested in the solution itself.
It is very similar to the authentication scenario from earlier where
we wanted to show that we have the secret key without revealing it.

But in this case, this is not an arbitrary key but something that solves 
a specific problem.

The beauty of ZKP is that they can be made to show that you have the 
solution to a complex problem, without showing that solution.

It could be because the solution has private information, or it
could also be that the solution is very large.

## Caveats

ZKP are fairly new in cryptography and therefore still under a lot of research 
and development. In my opinion, we are experiencing the very early days, kind like the 60s
were for computers. Though the theory of computer science did not evolve 
significantly, today's computers are at least 10 000 times
more powerful than the ones from back then. Likewise for ZKP, in theory they could be
used in many applications, but in practice they are extremely difficult
to build and exhibiy poor performance issues.

It takes a lot of work and skill to properly use a ZKP system, similarly to how
it was tricky to use the first computers. At that time, due to their limited power and memory,
only very carefuly crafted software could run. 

The goal of this series of videos is to gain a moderate understanding of what ZKP
can do today and what they have in store for the near future.

Let's end this overview here. Next time, we will start looking at some of the usage of ZKP
that are already in production.
