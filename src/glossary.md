# Glossary and Anti-Glossary

This document provides definitions and explanations for terms used throughout the project and a list of terms that should not be used.

## Table of Contents

- [Glossary and Anti-Glossary](#glossary-and-anti-glossary)
  - [Table of Contents](#table-of-contents)
  - [Glossary](#glossary)
    - [Actor](#actor)
    - [Bond](#bond)
    - [Collateral](#collateral)
    - [Collator](#collator)
    - [Committed Capacity](#committed-capacity)
    - [Commitment of Data](#commitment-of-data)
    - [Commitment of Replication](#commitment-of-replication)
    - [Crowdloan](#crowdloan)
    - [Deadline](#deadline)
    - [Extrinsics](#extrinsics)
    - [Fault](#fault)
    - [Full Node](#full-node)
    - [Invulnerable](#invulnerable)
    - [Node](#node)
    - [Parachain](#parachain)
    - [Partition](#partition)
    - [Planck](#planck)
    - [Polkadot](#polkadot)
  - [Proofs](#proofs)
    - [Proving Period](#proving-period)
    - [Relay Chain](#relay-chain)
    - [Sector](#sector)
    - [Session](#session)
    - [Slashing](#slashing)
    - [Slot Auction](#slot-auction)
    - [Staking](#staking)
    - [Storage Provider](#storage-provider)
    - [Storage User](#storage-user)
    - [System Parachain](#system-parachain)
  - [Anti-Glossary](#anti-glossary)
    - [Term to Avoid: Miner](#term-to-avoid-miner)
    - [Term to Avoid: Pledge](#term-to-avoid-pledge)

## Glossary

This section lists terms used throughout the project.

### Actor

In [Filecoin](https://spec.filecoin.io/#section-glossary.filecoin),
an [actor](https://spec.filecoin.io/#section-glossary.actor) is an on-chain object with its state and set of
methods. [Actors](https://spec.filecoin.io/#section-glossary.actor) define how
the [Filecoin](https://spec.filecoin.io/#section-glossary.filecoin) network manages and updates its global state.

### Bond

This term is used in:

- Parachain [Slot Auction](#slot-auction). To bid in an auction, [parachain](#parachain) teams agree to lock up (or
  bond) a portion of DOT tokens for the duration of the lease. While bonded for a lease, the DOT cannot be used for
  other activities like staking or transfers.

- [Collator](#collator) slot auction (selection mechanism). It is used as a deposit to become a collator. Candidates can
  register by placing the minimum bond. Then, if an account wants to participate in the [collator](#collator) slot
  auction, they have to replace an existing candidate by placing a more significant deposit (bond).

### Collateral

[Collaterals](https://spec.filecoin.io/#section-glossary.collateral) are assets locked up or deposited as a form of security
to mitigate risks and ensure the performance of specific actions. Collateral acts as a guarantee that an
individual will fulfil their obligations. Failing to meet obligations or behaving maliciously can result in the loss of
staked assets or collateral as a penalty for non-compliance or misconduct by [slashing](#slashing).

### Collator

[Collators](https://wiki.polkadot.network/docs/learn-collator) maintain [parachains](#parachain) by
collecting [parachain](#parachain) transactions from users and producing state transition proofs
for [Relay Chain](#relay-chain) validators. In other words, collators maintain [parachains](#parachain) by
aggregating [parachain](#parachain) transactions into [parachain](#parachain) block candidates and producing state
transition proofs (Proof-of-Validity, PoV) for validators. They must provide a financial
commitment ([collateral](#collateral)) to ensure they are incentivized to perform their duties correctly and
to dissuade malicious behaviour.

### Committed Capacity

The [Committed Capacity](https://spec.filecoin.io/#section-glossary.capacity-commitment) (CC) is one of three types of
deals in which there is effectively no deal, and the [Storage Provider](#storage-provider) stores random data inside the
sector instead of customer data.

If a [storage provider](#storage-provider) doesn't find any available deal proposals appealing, they can alternatively
make a capacity commitment, filling a sector with arbitrary data, rather than with client data. Maintaining this sector
allows the [storage provider](#storage-provider) to provably demonstrate that they are reserving space on behalf of the
network.

### Commitment of Data

This value is also known as `commD` or `unsealed_cid`.
As the storage miner receives each piece of client data, they place it into a sector. Sectors are the fundamental units of storage in Filecoin,
and can contain pieces from multiple deals and clients.

Once a sector is full, a CommD (Commitment of Data, aka UnsealedSectorCID) is produced, representing the root node of all the piece CIDs contained in the sector.

### Commitment of Replication

The terms `commR`, `sealed_cid`, `commitment of replication` are interchangeable.
During sealing, the sector data (identified by the CommD) is encoded through a sequence of graph and hashing processes to create a unique replica.
The root hash of the merkle tree of the resulting replica is the CommRLast.

The CommRLast is then hashed together with the CommC (another merkle root output from Proof of Replication).
This generates the CommR (Commitment of Replication, aka SealedSectorCID), which is recorded to the public blockchain.
The CommRLast is saved privately by the miner for future use in Proof of Spacetime, but is not saved to the chain.

### Crowdloan

Projects can raise DOT tokens from the community
through [crowdloans](https://wiki.polkadot.network/docs/learn-crowdloans). Participants pledge their DOT tokens to help
the project win a parachain slot auction. If successful, the tokens are locked up for the duration of the parachain
lease, and participants might receive rewards or tokens from the project in return.

### Deadline

A deadline is one of the multiple points during a proving period when proofs for some partitions are due.

For more information on deadlines, read the original Filecoin specification:
<https://spec.filecoin.io/#section-algorithms.pos.post.design>

### Extrinsics

From the [Polkadot Wiki][2]:

> Within each functional pallet on the blockchain, one can call its functions and execute them successfully, provided they have the permission to do so. Because these calls originate **outside of the blockchain runtime**, such transactions are referred to as **extrinsics**.

### Fault

A fault happens when a proof is not submitted within the [proving period](#proving-period).
For a sector to stop being considered in proving periods, it needs to be declared as faulty
— indicating the storage provider is aware of the faulty sector and will be working to restore it.
If a sector is faulty for too long, it will be terminated and the deal will be slashed.

For more information on faults, read the original Filecoin specification:
<https://spec.filecoin.io/#section-glossary.fault>

### Full Node

A device (computer) that fully downloads and stores the entire blockchain of the parachain, validating and relaying
transactions and blocks within the network. It is one of the [node](#node) types.

### Invulnerable

A status assigned to certain [collators](#collator) that makes them exempt from being removed from the active set of
[collators](#collator).

### Node

A device (computer) that participates in running the protocol software of a decentralized network; in other words, a
participant of the blockchain network who runs it locally.

### Parachain

A parachain is a specialized blockchain that runs in parallel to other parachains within a larger network, benefiting
from shared security and interoperability, and can be validated by the validators of the [Relay Chain](#relay-chain).

### Partition

Partitions are logical groups[^logical] of sectors to be proven together.

The number of sectors to be proven at once is 2349[^computational_limit], as defined by Filecoin.

For more information on partitions, read the original Filecoin specification:
<https://spec.filecoin.io/#section-algorithms.pos.post.constants--terminology>

[^logical]: They do not reflect the physical storage state, only existing in the context of deadlines and proofs.
[^computational_limit]: Filecoin defined the limit at 2349 to cope with computational limits, [as described in the specification](https://spec.filecoin.io/#section-algorithms.pos.post.windowpost).


### Planck

From the [Polkadot Wiki][1]:

> The smallest unit for the account balance on Substrate based blockchains (Polkadot, Kusama, etc.) is Planck (a reference to Planck Length, the smallest possible distance in the physical Universe).
> DOT's Planck is like BTC's [Satoshi](https://en.bitcoin.it/wiki/Satoshi_(unit)) or ETH's [Wei](https://ethereum.org/en/developers/docs/intro-to-ether/#denominations). Polkadot's native token DOT equals to \\(10^{10}\\) Planck and Kusama's native token KSM equals to \\(10^{12}\\) Planck.


### Polkadot

“Layer-0” blockchain platform designed to facilitate interoperability, scalability and security among different
“Layer-1” blockchains, called [parachains](#parachain).

## Proofs

Cryptographic evidence used to verify that storage providers have received, are storing, and are continuously
maintaining data as promised.

There are two main types of proofs:

- <a id="porep"></a> **Proof-of-Replication (PoRep):** In order to register a sector with the network, the
  sector has to be sealed. Sealing is a computation-heavy process that produces a unique representation of the data in
  the form of a proof, called Proof-of-Replication or PoRep.

- <a id="post"></a> **Proof-of-Spacetime (PoSt):** Used to verify that the storage provider continues to store the
  data over time. [Storage providers](#storage-provider) must periodically generate and submit proofs to show that they
  are still maintaining the stored data as promised.

### Proving Period

A proving period is when storage providers' commitments are audited,
and they must prove they are still storing the data from the deals they signed
- the average period for proving all sectors maintained by a provider (default set to 24 hours).

For more information on proving periods, read the original Filecoin specification:
- Proving periods in the context of Window Proof of Spacetime — <https://spec.filecoin.io/#section-algorithms.pos.post.windowpost>
- Proving periods in the context of Filecoin's system design — <https://spec.filecoin.io/#section-algorithms.pos.post.design>

### Relay Chain

The Relay Chain in [Polkadot](#polkadot) is the central chain (blockchain) responsible for the network's shared
security, consensus, and cross-chain interoperability.

### Sector

The sector is the default unit of storage that providers put in the network.
A sector is a contiguous array of bytes on which a storage provider puts together, seals,and performs Proofs of Spacetime on.
Storage providers store data on the network in fixed-size sectors.

For more information on sectors, read the original Filecoin specification:
<https://spec.filecoin.io/#section-glossary.sector>

### Session

A predefined period during which a set of [collators](#collator) remains constant.

### Slashing

The process of penalizing network participants, including [validators](#validators), [nominators](#nominators),
and [collators](#collator), for various protocol violations. These violations could include producing invalid blocks,
equivocation (double signing), inability of the [Storage Provider](#storage-provider) to [prove](#proofs) that the data
is stored and maintained as promised, or other malicious activities. As a result of slashing, participants may face a
reduction in their [staked](#staking) funds or other penalties depending on the severity of the violation.

### Slot Auction

To secure a [parachain](#parachain) slot, a project must win an auction by [pledging](#term-to-avoid-pledge) (locking
up) a significant amount of DOT tokens. These tokens are used as [collateral](#collateral) to secure the slot for a
specified period. Once the slot is secured, the project can launch and operate its [parachain](#parachain).

### Staking

Staking is when DOT holders lock up their tokens to support the network's security and operations. In
return, they can earn rewards. There are two main roles involved in staking:

- <a name="validators"></a>**Validators**: 
  Validators produce new blocks, validate transactions, and secure the network.
  They are selected based on their stake and performance.
  Validators must run a [node](#node) and have the technical capability to maintain it.

- <a name="nominators"></a>**Nominators**: Nominators support the network by backing (nominating) validators they trust
  with their DOT tokens. Nominators share in the rewards earned by the validators they support. This allows DOT holders
  who don't want to run a validator node to still participate in the network's security and earn rewards.

Our parachain will use staking to back up the [collators](#collator) similarly to "Nominators".
In this regard, "Nominators" will fall to [Storage Providers](#storage-provider),
while " Validators" will be assigned to [Collators](#collator) accordingly.

### Storage Provider

The user who offers storage space on their devices to store data for others.

### Storage User

**_Aka Client:_** The user who initiates storage deals by providing data to be stored on the network by the [Storage
Provider](#storage-provider).

### System Parachain

[System-level chains](https://wiki.polkadot.network/docs/learn-system-chains) move functionality from
the [Relay Chain](#relay-chain) into [parachains](#parachain), minimizing the administrative use of
the [Relay Chain](#relay-chain). For example, a governance [parachain](#parachain) could move all
the [Polkadot](#polkadot) governance processes from the [Relay Chain](#relay-chain) into a [parachain](#parachain).

## Anti-Glossary

This section lists terms that should not be used within the project, along with preferred alternatives.

### Term to Avoid: Miner

In [Filecoin](https://spec.filecoin.io/#section-glossary.filecoin), a "Lotus Miner" is responsible for storage-related
operations, such as sealing
sectors ([PoRep (Proof-of-Replication)](https://spec.filecoin.io/#section-algorithms.pos.porep)), proving storage
([PoSt (Proof-of-Spacetime)](https://spec.filecoin.io/#section-algorithms.pos.post)), and participating in
the [Filecoin](https://spec.filecoin.io/#section-glossary.filecoin) network as a storage miner.

**Reason**: In the [Filecoin](https://spec.filecoin.io/#section-glossary.filecoin) network,
the miner simultaneously plays the roles of [storage provider](#storage-provider) and block producer.
However, this term cannot be used in the [Polkadot](#polkadot) ecosystem because there are no block producers in [parachains](#parachain);
the [Relay Chain](#relay-chain) is responsible for block production. [Parachains](#parachain) can only prepare block
candidates via the [Collator](#collator) node and pass them to the [Relay Chain](#relay-chain).

### Term to Avoid: Pledge

It's better to apply this term within its proper context rather than avoiding it altogether. It's easy to confuse it
with [staking](#staking), but they have distinct meanings.

**Reason**: Pledging generally refers to locking up tokens as [collateral](#collateral) to participate in certain
network activities or services like: [Parachain Slot Auctions](#slot-auction) and [Crowdloans](#crowdloan).

[1]: https://wiki.polkadot.network/docs/learn-DOT#the-planck-unit
[2]: https://wiki.polkadot.network/docs/learn-transactions#pallets-and-extrinsics
