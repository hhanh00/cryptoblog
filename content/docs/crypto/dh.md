---
title: "Diffie Hellman"
date: 2022-02-18T11:49:09+08:00
weight: 40
---

Let's continue our exploration of popular cryptosystems with another
widely used protocol: The Diffie Hellman (DH) key agreement protocol.

When you connect to a `https` website, you are using the DH protocol.
It is how your client, i.e. your web browser negociates a unique encryption
key with the server.

We discussed RSA, a widely used public/private key crypto system and saw how it can
be used for encryption if you know the recipient's public key. 

However, it is not the best algorithm for large documents because RSA is too slow
and impractical. Instead, a symetric encryption system
such as AES is used. We will discuss AES in a later post. 

Symetric encryption is much faster and easier to implement
than Public/Private Key cryptosystems. The later use an abundance of mathematics
whereas the former operates by shifting and moving bits around. 

All of that
can be done easily done in hardware (and in software too).

Therefore, the stream of data exchanged between client and server is better encrypted
with AES than RSA.

But there is a problem. How do the client and the server agree on a key without 
communicating it beforehand?

When you access a website for the first time, 
obviously you never received any data before.
You can't have a key. And if the server sends you a key, it would be in clear text
and subject to interception by a malicious third-party.

How do you get a key when all your messages could be read during transport? 

Let's imagine you have a noisy postman who reads
all of your mail. In this situation, how can you
establish a common secret with your destination.
So that you can start encrypting your messages.

This is the goal of the Diffie Hellman protocol.

Let's review.

We want to connect to a particular destination. Let's say it's a website at `example.com`.
This website is registered and we can retrieve a public key. This key
represents its identity. We trust that in order to get this registration, they had to submit
some paperwork and the registrar made sure that they are who they claim.

Now when I want to connect to `example.com`, I want to be sure that I am connecting to
whoever has laid claim on that domain, i.e. whoever has registered.

One way we could do this is to put the responsibility of key maintenance on the registrar.
When I want to connect, I ask the registrar for a unique key and it generates a unique key for me and `example.com`. They send the key both to me
and `example.com` over a long term secure channel. 

But, if every time someone wanted to connect
they had to get a new key from the registrar, it would create a lot of work for them.

It'd better to have an algorithm where the *only* piece of information we need from `example.com`
is their public key. DH can do that.

The mathematics needed to *understand* DH are quite simple but again this is **not**
going to prove the safety of DH. It is one thing to create a lock, it is much harder
to prove that the lock is unpickable.

DH uses the same group we used for RSA: $(N_p^*, \times)$, i.e. the multiplicative
group of integers from $\\{1, 2, ..., p-1\\}$ where $p$ is a (large) prime number.

If we pick a number $g$, we know from previous video that $\\{1, g, g^2, g^3, ..., g^{p-1}\\}$
forms a group.

Basically, if we associate every number of $N_p^*$ by the formula:

$$ x \mapsto g^x $$

We "shuffled" the numbers of $N_p^*$. 

The most important thing to remember today is that this transformation is **very hard**
to reverse (in most of the cases). Very hard as in: it's gonna take a billion billion years for 
relatively "short" $p$ (only a few hundred bits).

This is called the "discrete logarithm problem". The function above was an "exponentialization"
because the $x$ is in the exponent. Therefore the reverse is a logarithm. It's a discrete
logarithm because we want the result to be an integer and not a real number. 

We will assume that solving the discrete logarithm problem is not efficient.

Now let's see how DH uses it.

Both server and client agree on a value for $g$. In fact, *everyone* agrees to use the same value
as it doesn't matter what value it is.

The server picks up a secret value $s$ and computes $x = g^s$. He registers $x$ so that anyone
who wants to communicate with it knows $x$. Yet, the value of $s$ remains private.

Then the client picks up a new random key, anything in $N_p^*$. Let's call it $s'$.

He calculates $x' = g^{s'}$ and sends it to the server. This value will be different from any other
value.

The server calculates $$S = x'^s = \\left(g^{s'}\\right)^s = g^{ss'}$$

On his side, the client calculates
$$ C = x^{s'} = \\left({g^s}\\right)^{s'} = g^{ss'} $$

And because $ss' = s's$, $$C = S$$

Now, they can use this value as their AES encryption key.

We can notice that all messages sent between client and server are hiding their true value by putting
it in $g^x$. If someone intercepts them, he will not be able to extract the value of $x$ by virtue
of the "discrete logarithm problem". 

An entire class of cryptosystems use this property. It's called ElGamal encryption and we will
see it several times in future sessions.

