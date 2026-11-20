![QRL article banner](assets/banner-article.png)

# What Is a Hash-Based Signature?

**Short answer.** A hash-based signature proves you know a secret using only a hash function. Its security rests on that function being one-way, rather than on a hard number-theory problem, which is why a quantum computer changes the threat very little. The cost is size: hash-based signatures are much larger than the elliptic-curve ones most wallets use.

## The idea

Every ordinary signature scheme rests on a problem believed to be hard: factoring large numbers, or finding discrete logarithms in some group. A hash-based scheme rests on something simpler and better understood. It assumes that a hash function cannot be inverted and that finding two inputs with the same output is impractical.

That assumption has been studied for decades and does not depend on the structure of a group. A quantum computer attacks factoring and discrete logarithms efficiently; against a hash function's preimage resistance it offers only a square-root speedup, which is answered by using a longer output.

The mechanics follow from that. A secret is hashed repeatedly to produce a public value. The signature reveals intermediate values, and the verifier hashes them forward to the public value. Anyone can check the result; nobody can run it backwards.

That public value is small, a string of hash output, and it does not grow with the number of signatures the key can make. An address built this way stays the same size whether it sits behind one signature or a thousand.

## Lamport and Winternitz lineage

The oldest construction is Lamport's, from the late 1970s. For each bit of the message digest it uses a pair of secret values, publishing their hashes as the public key. Signing reveals one secret per bit, chosen by whether that bit is zero or one, and the verifier hashes each revealed value to check it.

That works and is beautifully simple. It is also large: a signature carries one value per bit, and verification hashes each of them.

Winternitz's variant reduces the count by signing digits in base w rather than single bits, so each revealed value covers several bits at once. The signature shrinks and the computation grows, and the trade-off is tunable rather than fixed. Every practical hash-based scheme descends from one of those two ideas.

The digits need a checksum. Without one, a forger could pick digits that only require values already revealed and claim a different message, so the construction also signs the sum of the digits. That checksum is the detail that turns a smaller signature into a usable one.

## Why one-time

Both constructions share a weakness that is not a bug to be fixed but a property to be respected: a key signs once. Revealing the secret values for one digest tells a verifier what it needs, and revealing a second digest under the same key exposes more of the same secrets, enough to forge a third signature.

So hash-based signatures are one-time by nature. The fix is not a better key but more keys, which is what a Merkle tree provides: many one-time keys committed to by one public value.

That is also why the scheme is stateful. The signer has to know which keys are spent, and a wallet that forgets can be pushed into signing twice. [Why Stateful Signatures Matter in QRL](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/why-stateful-signatures-matter-in-qrl.md) covers what that means in practice.

## Sizes and costs

Hash-based signatures are larger than ECDSA or EdDSA signatures, by a wide margin, and a wallet using them stores more per address and sends more per transaction. The size buys the different security assumption, and the trade is deliberate rather than accidental.

Verification costs hashing rather than arithmetic, repeated once per element of the signature and once per level of the tree. The work is fixed by the scheme rather than by the message, and the wallet's own key generation at address creation is where the larger, one-off cost of building a tree lands.

There is no way to get the hash-based assumption with elliptic-curve sizes. Every scheme in the family pays in bytes, and the variants differ in how many.

Storage follows the same trade. A wallet holds the public keys of a whole tree per address, and what the backup actually contains is the seed that regenerates them. The cost is paid at signing and in the transaction, not in the phrase you write on paper.

## Where QRL uses it

QRL signs transactions with XMSS, a standardised hash-based scheme built from a Merkle tree of one-time keys. Each address has 1,024 keys by default, and each spend reveals one key plus the path proving it belongs to the address's tree.

The rest of the wallet is ordinary software around that: a local file, a password, a seed phrase. What changes is the signature under the transaction and the discipline around the key index.

[How XMSS Signatures Work](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/how-qrl-xmss-signatures-work.md) walks through a signature end to end, [Why QRL Uses a Merkle Tree](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/why-qrl-uses-a-merkle-tree.md) explains the structure that makes many keys usable under one address, and [Can Quantum Computers Break Bitcoin?](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/can-quantum-computers-break-bitcoin-and-qrl.md) covers the threat model the choice answers. [What Is the QRL Quantum Resistant Ledger?](https://github.com/qrl-wallet/token-facts-and-prices/blob/main/what-is-the-qrl-quantum-resistant-ledger.md) places the scheme in the wider project.

## FAQ

### Are hash-based signatures immune to all cryptanalysis?

No. They rest on a hash function, so a break in that function would matter. The point is that the assumption is narrower and better studied than the ones elliptic-curve schemes rely on.

### Why can a hash-based key only sign once?

Because revealing the secret values for two different messages exposes enough to forge with the same key. One signature is safe; two are not.

### Why are the signatures so large?

Each signature carries the revealed values plus the path through the tree, and both are made of hashes. There is no compact algebraic form to compress them into.

### Does QRL use a bespoke scheme?

No. QRL signs with XMSS, which is standardised: IETF RFC 8391 and NIST SP 800-208.

<!-- answers: none -->
