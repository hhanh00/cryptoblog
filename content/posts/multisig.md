---
title: "Multisig"
date: 2022-02-15T19:05:18+08:00
draft: true
---

### If you have any doubts about the questions below, please reach out to Zcash Foundation's Ecosystem Relations Manager, [decentralistdan](https://forum.zcashcommunity.com/u/decentralistdan/summary), on the [Zcash forums](https://forum.zcashcommunity.com/).

# Applicant background
Summarize you and/or your team’s background and experience. Demonstrate that you have the skills and expertise necessary for the project that you’re proposing. Institutional bona fides are not required, but we want to hear about your track record.

# Description of Problem or Opportunity  
Multisignature transactions have unique use-cases
not covered by regular transactions.
- 1 of n: Multiple people sharing the same account
and any person can spend. The accountant wants to keep
a record of who did the spending
- 2 of 2: Every party must sign to approve spending
- 2 of 3: Escrow account where two counterparties
can agree to spend but in case of a disagreement they
can engage of third party.
- n of n: High security vault

# Proposed Solution
The ZF has published the FROST scheme that allows
the creation of multi party Schnorr signatures.

I propose to use it as a foundation for Zcash
shielded transactions. There are several outstanding
design points to complete:

- Derivation of the nullifier keys, viewing keys, etc
in the context of a multisig account,
- Encoding of multisig keys
- The Zcash protocol rerandomizes the authorization signature
- The FROST protocol has several rounds. The exact
definition of the message exchanges have to be specified
- Currently, signing is a regular function. Because
of the multiple rounds involved, it needs to be 
refactored into several stages
- Signers must be able to safely check that the
request they receive is legitimate

# Solution Format
Each of the points mentioned in the previous section
must be addressed before implementation.

- I will work with the ZF/ECC to validate and audit
the design, especially regarding the cryptographic aspects.
- I will write and submit ZIPs as fit,
- I will define an API with input from the wallet owners
who are interested in this feature
- I will implement a library in rust for distributed
key generation and multisignatures (client and server)
- I will implement a (trustless) server that orchestrates the signing protocol and the distributed
key generation
- I will add test vectors and unit tests for both
client and servers
- I will write the documentation to help wallet owners. It remains their choice and responsibility to integrate.
- I will add multisignature to ZWallet

This project is for NU-5.

# Technical approach

## Key Generation
Users participate in a distributed key generation protocol with assistance from a server (hosted in the cloud).
After which, they are given a secret key share. Alternatively, if they want to do everything off line, they
can use a command line tool and transmit the data manually. Due to the nature of the protocol, this means sending
a files to each other party and therefore receiving N-1 files. Then the secret share and public key / viewing key
are calculated. This is similar to multi sig in Bitcoin which uses xprv and xpub keys to derive joint address.

## Signing a transaction

To spend from the multisig account, the initiator contacts the server passing the transaction data (inputs/outputs),
encrypted for each of the other parties. Other signers retrieve the signing request and calculate their signature
share (after confirmation from the user). The shares are aggregated to produce the final transaction and is transmited
to the network. The server only knows the IP and the timestamp of the transaction.

# How big of a problem would it be to not solve this problem?

Users can use transparent multisignatures but will not benefit from the privacy associated with shielded 
transactions.

# Execution risks

- Some cryptographic remaining work need design, specification, validation, implementation and audit. Therefore
there is dependency on ECC/ZF experts who are busy,
- ZIP may take longer than expected
- How multisignature addresses fit with UA is TBD

# Unintended Consequences
- Multisig accounts work differently than regular accounts and users need to be aware, specifically regarding
storage of their keys.
- The aggregator server must be up and running or multisig accounts will not work. However, a private
entity can always deploy their own instance.

# Evaluation plan

- Design Documentation
- ZIP
- API documentation
- Implementation as a rust crate
- Support in ZWallet 

# Schedule and Milestones

# Budget
