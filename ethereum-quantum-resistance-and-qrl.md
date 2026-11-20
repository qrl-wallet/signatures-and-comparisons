![QRL article banner](assets/banner-article.png)

# Is Ethereum Quantum Resistant?

**Short answer.** Not in its account signatures. Ethereum authorises transactions with ECDSA over the secp256k1 curve, and its consensus layer uses BLS signatures, both classical schemes. Post-quantum work is discussed and proposed, but no post-quantum signature scheme secures accounts on the network today. QRL's difference is that its scheme is already the one holding balances.

## How Ethereum signs today

An Ethereum account is controlled by a key pair. A transaction is signed with ECDSA over secp256k1, the same curve Bitcoin uses, and the signature travels with the transaction so nodes can verify it. Contract accounts have their own logic, but the key that authorises a transfer from an externally owned account is an elliptic-curve key.

Consensus is a second layer with its own cryptography. Validators sign attestations with BLS signatures, which are also built on elliptic curves, chosen because they aggregate efficiently when many validators sign the same thing.

Both layers therefore depend on the same family of mathematics. That is the technical answer to the question, and it does not depend on anyone's opinion about timelines.

## Where the exposure sits

An account's public key is not on the chain until the account sends something. Addresses are derived from the key, and until a transaction is signed, an attacker would need to break the hash to reach the key.

The first outgoing transaction publishes the key, and it stays published. From that moment the account's security rests on the difficulty of deriving a private key from a public one, which is the assumption a quantum machine would remove. An account that keeps receiving at the same address after spending is the most exposed shape: the key is public and the balance sits behind it.

This is why the practical advice for Ethereum holders is the same as for Bitcoin holders. Use fresh addresses, and treat a key that has signed as public. [Can Quantum Computers Break Bitcoin?](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/can-quantum-computers-break-bitcoin-and-qrl.md) explains the mechanism in full.

## What is proposed

Post-quantum cryptography is an active research area in the Ethereum ecosystem, and proposals for quantum-resistant signatures exist in the wider field. What matters for a holder is the difference between a proposal and a deployment: a proposal describes software that could be built, and a deployment is software the network runs and enforces.

Changing the signature scheme on Ethereum is not a small patch. It touches the transaction format, every wallet, every tool that reads a transaction, and the gas economics of a signature that is much larger than an elliptic-curve one. Any honest description of the work says it is substantial and that no date is settled.

It is also worth separating two questions that get mixed together: whether a chain could migrate, and whether a holder should wait for it. The first is an engineering programme without a settled schedule. The second is a decision about exposure today, and waiting does not reduce the number of keys already published on the chain.

That does not make Ethereum unusual. It describes the position most large networks are in, including Bitcoin. The interesting question is not who has a plan, but whose live software already signs with a post-quantum scheme.

## How QRL differs

QRL signs with XMSS, a hash-based scheme standardised in RFC 8391 and profiled by NIST in SP 800-208. The signature is built from hash computations over a one-time key, so its security rests on the hash function rather than on a number-theory problem. Shor's algorithm has nothing to attack.

It has been the signing scheme since QRL's first block in 2018, which is the part that distinguishes a property from an intention. The cost is statefulness: every signature consumes one key from a tree of 1,024 by default, and the wallet tracks which comes next. [How XMSS Signatures Work](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/how-qrl-xmss-signatures-work.md) explains the construction and [Why QRL Is Quantum Proof](https://github.com/qrl-wallet/token-facts-and-prices/blob/main/why-qrl-is-quantum-proof.md) covers the reasoning.

The boundary is worth stating. QRL's peer-to-peer transport is still classical, with post-quantum key establishment in development. The signatures are post-quantum; the transport is not.

## What a holder can do

For an Ethereum balance, the steps that help today are the ones that limit how long a key stays exposed: use a fresh address rather than reusing one, and avoid holding a large balance behind a key that has already signed many times.

For a balance held for years, the deeper question is which scheme protects it. [What Makes a Wallet Quantum Safe?](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/what-makes-qrl-wallet-quantum-safe.md) sets out what has to be true for a wallet to earn that label, and [Quantum Resistant Cryptocurrency: The List](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/quantum-resistant-cryptocurrency-list-with-qrl.md) separates projects whose signatures are post-quantum from those still discussing it.

[How QRL Compares on Quantum Readiness](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/how-qrl-compares-on-quantum-readiness.md) places QRL beside other approaches without ranking them by market size, because market size is not a cryptographic property.

## FAQ

### Is Ethereum quantum resistant?

No. Accounts sign with ECDSA and validators sign with BLS, both classical elliptic-curve schemes, so the network depends on the discrete logarithm problem that Shor's algorithm attacks.

### Does Ethereum have a post-quantum plan?

Post-quantum signatures are discussed and proposed in its research community. No post-quantum account scheme is live, and no settled date exists for one.

### Are contract accounts different?

A contract executes code rather than signing with a key, but the account that deploys or controls it is still authorised by a classical key. The exposure sits with the key that can move the funds.

### What would a holder notice if the scheme changed?

Larger signatures, different transaction formats and new wallet software, since a post-quantum signature is much bigger than an elliptic-curve one. None of that is a reason to postpone protecting a balance today.

<!-- answers: none -->
