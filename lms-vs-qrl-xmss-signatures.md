![QRL article banner](assets/banner-article.png)

# LMS vs XMSS Signature Schemes

**Short answer.** LMS and XMSS are both hash-based and both stateful, and both are standardised in the same NIST publication. They differ in how the tree and the one-time keys underneath it are built, and in how each is specified, rather than in the threat they answer. QRL signs with XMSS.

## What both schemes share

Each is built only from a hash function. Neither depends on factoring or on discrete logarithms, so neither inherits the quantum weakness that elliptic-curve signatures have.

Each signs with one-time keys. A key signs once, and a second signature under the same key is a failure rather than a warning, which makes both schemes stateful: the signer has to know which keys are spent.

Each commits many one-time keys to a single public value using a tree. That value is what a verifier checks against, and it is why a single address or key identifier can be used for more than one signature.

Both are standardised rather than experimental. NIST SP 800-208, published in 2020, covers the stateful hash-based schemes, and the QRL documentation lists both RFC 8391 for XMSS and that publication among its references.

The shared design also means a shared failure mode. In both schemes a lost key index is the risk, and in both the remedy is the same: a backup that includes the state, not just the seed.

## LMS structure

LMS pairs a one-time signature component with a Merkle tree over the public keys it produces. The one-time layer is its own specification, and the tree layer is what turns a set of those keys into one identifier.

Capacity is raised by stacking trees rather than by growing a single one. A hierarchy of trees, each signing the root of the next, gives a much larger total number of signatures at the cost of a longer proof and more bookkeeping about where the hierarchy currently stands.

The result is a scheme that scales by composition. Each layer is simple; the complexity lives in the arrangement, and in the state that has to be tracked across layers.

Its specification treats the one-time layer and the tree layer as separate things, which is why questions about LMS variants usually turn on which layer the asker means.

## XMSS structure

XMSS pairs its own one-time signature construction with a binary hash tree, and the root is the public key. A signature carries the one-time signature, the leaf index and the authentication path to the root.

The one-time layer is built from hash chains with a checksum, which is where the Winternitz lineage shows. The tree is binary and balanced, so the path length is exactly the height, and the arithmetic of capacity is straightforward: height h gives 2 to the power of h signatures.

XMSS also has a multi-tree form, which composes trees the way the hierarchical variant does on the LMS side, so the scaling idea exists in both families even though the base construction differs.

## Multi-tree variants

Both schemes reach large capacities by composing trees rather than by building one enormous tree. Composition keeps each individual tree small enough to generate in reasonable time, while the identifier at the top stays fixed.

The cost is the same in both cases: more levels means a longer proof and more state to track. A scheme arranged to sign far more times is not free; it is a small tree repeated with a bookkeeping layer on top.

For a wallet, that trade is usually unnecessary. An address starts with 1,024 signatures, the wallet shows the count, and a new address restarts it, so capacity is managed by moving rather than by composing trees.

## Why QRL chose XMSS

What the record shows is what QRL uses: XMSS, signing from the genesis block, with 1,024 keys per address by default and a configurable tree height at creation.

XMSS was standardised by the IETF in RFC 8391 in 2018, and NIST listed it alongside LMS in SP 800-208 in 2020. A published standard with two independent specifications behind it is the kind of thing a ledger chooses when the signature scheme has to outlive the team that picked it.

What is not in the record is a published comparison study weighing the two schemes against each other, so the reasoning here is about consequences rather than motives. Either scheme would answer the quantum question; the difference is in the construction, the proof length at a given capacity and the tooling around it.

What follows from the choice is observable in the wallet: a tree fixed at creation, a count that starts at 1,024 and is shown to the user, and a signature that carries a path of ten hashes back to the root.

The practical comparison for a user is not LMS versus XMSS in the abstract. It is whether the wallet tracks the key index correctly, whether backups preserve it, and whether the address is moved before its keys run out. [Why Stateful Signatures Matter in QRL](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/why-stateful-signatures-matter-in-qrl.md) covers that shared obligation.

[How XMSS Signatures Work](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/how-qrl-xmss-signatures-work.md) walks through the XMSS signature, [What Is a Hash-Based Signature?](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/what-is-a-qrl-hash-based-signature.md) covers the hash assumption, and [Why QRL Uses a Merkle Tree](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/why-qrl-uses-a-merkle-tree.md) explains the structure both families rely on. [QRL Security Audit History](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/qrl-security-audit-history.md) covers the reviews of the implementation rather than the scheme.

## FAQ

### Is LMS weaker than XMSS?

Not on the evidence here. Both rest on hash functions, both are stateful, and both are standardised. Which is preferable depends on the criterion you are optimising for, such as proof length at a given capacity or the tooling available.

### Do both schemes need the key index tracked?

Yes. Both are stateful, so both require the signer to know which one-time keys have been used.

### Does QRL support LMS addresses?

QRL signs with XMSS. LMS is the neighbouring standard, not an alternative the wallet offers.

### Does a multi-tree variant give unlimited signatures?

No. It raises the total substantially, but the count is still finite and the index still has to be tracked.

<!-- answers: none -->
