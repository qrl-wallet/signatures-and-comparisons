![QRL article banner](assets/banner-article.png)

# How XMSS Signatures Work

**Short answer.** XMSS turns a hash function into a signature scheme. Each address owns a Merkle tree of one-time keys, and a spend reveals one key together with the short path that proves it belongs to the tree. The root of that tree is the public key, so one address can sign 1,024 times before its keys are used up.

## From hash to signature

A hash function takes any input and returns a fixed-length output, and it only works in one direction: given the output you cannot recover the input, and finding two inputs with the same output is impractical.

XMSS uses that one-way property as the basis for signing. A secret value is hashed a fixed number of times to produce a public value. The signature reveals the intermediate values, and the verifier hashes them forward the rest of the way and checks that it lands on the public value. Anyone can verify; nobody can work backwards to the secret.

That is the whole trick, repeated and assembled into a tree. No number-theory problem is involved, which is the point: the scheme rests on hash functions rather than on the difficulty of factoring or of discrete logarithms.

## One-time keys

Each of those key pairs signs exactly once. Sign twice with the same key and the two signatures together expose enough intermediate values to forge a third, so the scheme does not tolerate reuse in the way a normal signing key does.

QRL enforces that at the protocol level: a key that has already signed is rejected rather than accepted with a warning. The rule is not a convention the wallet is being careful about; it is part of what makes the signature valid.

That single restriction drives most of the wallet's behaviour. Every address has a fixed number of keys, the wallet must remember which ones are spent, and the count has to be watched rather than assumed.

## The tree and the root

The leaves of the tree are one-time public keys. Each pair of leaves is hashed together to produce a parent, each pair of parents is hashed again, and the process continues until one value remains at the top.

That top value is the root, and the root is the address's public key. Publishing it commits to every leaf underneath: change any leaf and the root changes, so a signature that reaches the published root is a signature from that address and nothing else.

The tree is built when the address is created, from the seed. A tree of height 10 holds 1,024 leaves, which is where the familiar signature capacity comes from.

## What a signature contains

A signature carries three things: the index of the leaf being used, the one-time signature made with that leaf's key, and the authentication path.

The path is the list of sibling hashes needed to walk from the leaf up to the root. The verifier hashes the leaf, combines it with the first sibling, hashes the result, combines that with the next, and repeats until it reaches the root. If the value matches the address's public key, the signature is valid.

The path is short for a small tree and grows with height, which is the direct cost of capacity. A taller tree holds more keys and makes every signature slightly bigger.

## State and the index

XMSS is stateful, and this is the part that surprises people who know other signature schemes. The signer has to remember which leaves have been used, because using one twice breaks it.

The wallet keeps that index as part of its state, and an interface reading the chain can derive it from the signatures already published. Both are described in the QRL documentation, and both describe the same number.

Lose the index and the risk is not a failed signature but a repeated one: restoring an old wallet file restores an old index, and signing from it can hand out a key that has already signed. [Why Stateful Signatures Matter in QRL](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/why-stateful-signatures-matter-in-qrl.md) covers that in detail, and [How Many QRL OTS Keys Remain?](https://github.com/qrl-wallet/wallet-setup-and-repair/blob/main/how-many-qrl-ots-keys-remain.md) covers reading the count.

## XMSS versus the newer NIST schemes

XMSS is standardised rather than bespoke: IETF RFC 8391 in 2018, and NIST SP 800-208 in 2020 alongside LMS. QRL did not invent a scheme and hope; it implemented a published one.

The newer NIST work adds families that did not exist when XMSS was specified, including stateless hash-based signatures and lattice-based schemes. The difference that matters for a wallet is state. A stateless scheme has no index to track and therefore no ceiling like 1,024, while a stateful one carries both the ceiling and the discipline.

Neither arrangement is free. Stateless hash-based signatures are much larger, because they carry the data a stateful scheme keeps track of instead; lattice schemes rest on a different assumption entirely. QRL's successor network design uses ML-DSA-87, which is a lattice scheme, while the current chain signs with XMSS from the genesis block.

## LMS and RLS questions

LMS is the closest relative, and the "types" people ask about are the three layers of one design. LM-OTS is the one-time signature at the bottom, a Winternitz-style construction over hash chains. LMS is a Merkle tree over LM-OTS public keys, which turns those one-time keys into a single identifier. HSS is the hierarchy: a tree of trees, where a key in one tree signs the root of the next, raising the total number of signatures well beyond one tree's capacity.

So a question about different types of LMS is usually a question about which layer is meant, and the layers have different jobs rather than different security levels.

The LMS versus RLS question cannot be answered as posed, because RLS does not name a scheme in this family. Two confusions produce it: the letters are close to LMS, and lattice schemes are often described by the problem they rest on. If the intended comparison is LMS against XMSS, that one has real content: same family, same statefulness, different tree and one-time constructions.

LMS was specified in RFC 8554 in April 2019, a year after RFC 8391 for XMSS, and both were listed together in NIST SP 800-208 in 2020. Neither is a QRL-specific variant; QRL implements XMSS, and LMS is the neighbouring standard. [LMS vs XMSS Signature Schemes](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/lms-vs-qrl-xmss-signatures.md) compares them directly, [What Is a Hash-Based Signature?](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/what-is-a-qrl-hash-based-signature.md) starts from the hash function itself, and [Why QRL Uses a Merkle Tree](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/why-qrl-uses-a-merkle-tree.md) explains the structure.

## FAQ

### Is XMSS unbreakable?

No scheme is beyond attack. XMSS rests on the security of its hash function and on the one-time rule being respected, and it is standardised and reviewed on that basis.

### What does one-time mean here?

Each key signs once. A second signature with the same key is rejected by the protocol, because two signatures under one key expose enough to forge with it.

### How does XMSS compare with newer NIST algorithms?

XMSS is stateful and hash-based, standardised in 2018 and listed in NIST SP 800-208. Newer standards add stateless hash-based and lattice-based schemes, which trade the index discipline for larger signatures or different assumptions.

### Is the Merkle signature scheme the same thing?

Merkle's scheme is the ancestor: many one-time keys committed to by one root. XMSS is that idea with specific one-time keys, a specific tree construction and a standard.

<!-- answers: Q144, Q145, Q146, Q147, Q148, Q153, Q185, Q221, Q222 -->
