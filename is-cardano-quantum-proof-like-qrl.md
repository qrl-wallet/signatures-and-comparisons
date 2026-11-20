![QRL article banner](assets/banner-article.png)

# Is Cardano Quantum Proof?

**Short answer.** Not today. Cardano signs transactions with Ed25519, a classical elliptic-curve scheme, so its authorisation rests on the discrete logarithm problem that Shor's algorithm would attack. Research and discussion about post-quantum work are not a live signing path. QRL's signatures are hash-based and have been since its first block.

## What Cardano signs with

Cardano's transaction signatures use Ed25519, the Edwards-curve signature scheme designed for speed and small keys. Addresses carry a verification key hash, and a spend is authorised by a signature made with the corresponding key.

Ed25519 is a good scheme for the job it was designed for. It is fast, its signatures are compact, and it is deployed so widely that its implementation has been examined by a large number of people. None of that changes what it depends on: the difficulty of deriving a private key from a public one on an elliptic curve.

That is the whole of the quantum question for Cardano. Shor's algorithm solves the discrete logarithm problem for a machine with enough stable qubits, and Ed25519 is built on exactly that problem.

## Where the exposure sits

A Cardano address does not publish its public key when it receives funds; it publishes a hash of the key. Until the key signs, an attacker would first have to break the hash to reach the key itself.

The first spend changes the situation. The transaction carries the public key so nodes can verify the signature, and that key stays on the chain. From that point the account is protected by an assumption a quantum computer would remove, and reusing the address keeps the same key in view.

This is the same exposure that Bitcoin has, for the same reason, and [Can Quantum Computers Break Bitcoin?](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/can-quantum-computers-break-bitcoin-and-qrl.md) treats that case in detail. It is also the reason address hygiene is advice worth taking before a machine exists: an address that has never signed is strictly harder to attack than one that has.

## What would have to change

A chain cannot swap its signature scheme quietly. The transaction format names the scheme, the wallets construct signatures in that format, the node software verifies them, and every tool that reads a transaction expects the same shape. Replacing Ed25519 with a hash-based or lattice-based scheme touches all of it.

Some of those changes are harder than others. A post-quantum signature is usually much larger than an Ed25519 one, which changes transaction sizes and the economics of block space. A stateful scheme adds a requirement the chain has never had: a key index that must move forward, which is why QRL's wallet behaves the way it does.

That is why "we are working on it" and "it is live" are different statements, and why the second one is the only one that protects a balance.

## Research versus deployment

Cardano's community, like most serious ones, discusses post-quantum cryptography. Papers, conference talks and proposals exist in the field, and some of them are about Cardano specifically. What none of that does is change what the network accepts today.

The test is mechanical. Open a transaction on a block explorer and look at the signature, or read the specification that names the scheme. If the format is Ed25519, the chain is classical now, whatever has been published about later work. A proposal is a lead; a deployment is a fact you can check.

Apply that test honestly in both directions. QRL's claim is that XMSS is in the signing path and has been since 2018, not that the scheme is fashionable or new. That is a smaller claim, and a checkable one.

## How QRL differs

QRL signs with XMSS, a hash-based scheme standardised in RFC 8391 and profiled by NIST in SP 800-208. A signature is built from hash computations over a one-time key, so its security rests on the hash function rather than on a number-theory problem. Shor's algorithm has nothing to run against it.

The trade is statefulness: each signature consumes one key from a tree of 1,024 by default, and the wallet tracks the index. [How XMSS Signatures Work](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/how-qrl-xmss-signatures-work.md) explains the construction, and [Why QRL Is Quantum Proof](https://github.com/qrl-wallet/token-facts-and-prices/blob/main/why-qrl-is-quantum-proof.md) covers the reasoning behind the choice.

QRL is also not post-quantum everywhere, and saying so matters. Its peer-to-peer layer still uses classical key exchange, with post-quantum work in development. The signatures that hold the coins are post-quantum; the transport between nodes is not.

## How to check a claim

Four questions settle it for any chain, and they work for Cardano, for Ethereum and for QRL. What scheme signs a transaction today? When did it enter the signing path? What does the transport layer use? And who outside the project examined the implementation?

A block explorer answers the first two for a live chain. The specification names the scheme, and the chain's history shows when it arrived. If the answer is a classical curve, the chain is not quantum proof today, and no amount of published research changes the answer.

[Quantum Resistant Cryptocurrency: The List](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/quantum-resistant-cryptocurrency-list-with-qrl.md) sets out how to read the label across projects, [Is XRP Quantum Resistant?](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/is-xrp-quantum-resistant-like-qrl.md) takes the same question to another chain, and [How QRL Compares on Quantum Readiness](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/how-qrl-compares-on-quantum-readiness.md) puts several approaches side by side without ranking them by price.

## FAQ

### Is Cardano quantum proof?

No. Its live transaction signatures are Ed25519, which is classical, so the network depends on the elliptic-curve discrete logarithm problem that Shor's algorithm attacks.

### Does Cardano have post-quantum work?

The topic is discussed in its research community, as it is across the industry. Published research and proposals are not a scheme in the signing path, and no post-quantum signature is accepted by the network today.

### Would a Cardano holder be affected the same way as a Bitcoin holder?

Broadly yes. A key becomes public when it signs, so an address that has never spent is better protected than one that has. The exposure is the same shape even though the implementations differ.

### What makes QRL different?

Its signatures are hash-based rather than elliptic-curve, and that scheme has been the one securing balances since 2018. The difference is the mathematics the signature depends on, not the marketing label.

<!-- answers: none -->
