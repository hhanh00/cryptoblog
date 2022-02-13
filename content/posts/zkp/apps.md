---
title: "Applications of ZKP"
date: 2022-02-10T22:56:07+08:00
---

Today we look at some coins that use zk-proofs in
one way or another.

But let's start with what zk-proofs can do.

First of all, functions has the same expressive power
than programs. In other words, any program can be
converted into a function. For example, if a program
processes financial transactions and tracks account balances,
it can be rewritten as a function that returns new account
balances given current balances and transaction data.

Something like:

$$ f(\mathrm{inputs}) = \mathrm{outputs} $$

where outputs are the new state, usually public. 
Some of the inputs are public, in this example it would be
the previous account balances and the rest of the inputs are
secret. $f$ is the ZKP function or sometimes it is called the 
**statement**.

The ZK-Proof proves that you know the secret inputs
without giving any indication of what they are.

Currently, cryptocurrencies use ZK-Proofs in a few 
ways.

## L2 ZK-Rollups

Previously, we talked about smart contracts. Ethereum is
famously the first cryptocurrency to introduce them. They 
gained a lot of popularity and as a result the number of
transactions on the Ethereum blockchain grew significantly.
Along with it, transaction fees also increased. To a point
that it is no longer economical to directly call smart
contracts on Ethereum. 

A few teams work on reducing the strain on the blockchain (that's layer 1)
by transmitting and executing transactions off chain (that's layer 2).
ZKP are used in some of the Layer-2 solutions in order to
allow verification by smart contracts on the Layer 1. Ethereum has a few
of them: ZkSync, Aztec and Starkware.

A normal rollup contract is deployed on Ethereum. It 
verifies the validity of the zk proofs. Transactions
are processed off-chain.
Multiple transactions can be grouped, processed together
and submit a single zk proof on Ethereum.

Recently Polygon announced Miden, a rollup project for 
Ethereum VM.

## Privacy Coins

Privacy coins such as Zcash, Monero or Firo hide information
about transactions. Zcash encrypts all the amount and address
of the party involved. Monero mixes the real sender and receiver
with unrelated notes. In all cases, ZKP
are used to prove that the transaction remains valid.

## Succint Blockchain

Finally, the last coin we are considering today is
Mina (Protocol). They use ZKP to enable a fixed size
blockchain. For any other coin, the blockchain is
formed by chaining a series of blocks (hence the name).
Even if the data that ends up on chain is kept to a minimum
with Layer 2 systems, by nature the blockchain
grows indefinitively as more and more blocks are produced.

In Mina Protocol, the history, i.e. the previous blockchain
data serves as a hidden (or secret) input to the ZKP
function. Essentially, the statement means:
"I know a previous blockchain history and a series
of valid transactions, such as together they produce
this new block, and here's the proof."
Since the proof is part of the block, we have an instance
of a recursive ZKP because the ZKP is an input and
the function verifies its validity among other things.

## Conclusion

Here you have it. A few concrete examples of usage
of ZKP in production blockchains. I am sure there are
going to be many more projects using ZKP. The proving
systems keep getting better and better, and they
become more accessible to the non-experts.


