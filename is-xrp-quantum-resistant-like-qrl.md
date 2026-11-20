![QRL article banner](assets/banner-article.png)

# Is XRP Quantum Resistant?

**Short answer.** Not today. The XRP Ledger signs with classical elliptic-curve keys, the same family of mathematics that a quantum computer running Shor's algorithm would attack. QRL's signatures are hash-based, which is a different foundation. Research and public discussion about post-quantum work are not the same as a scheme in the signing path.

## What the XRP Ledger uses to sign

The XRP Ledger supports a small set of signature schemes for accounts, and both are classical. One is ECDSA over the secp256k1 curve, the scheme Bitcoin also uses. The other is Ed25519, a modern elliptic-curve signature that is fast and widely deployed across many systems.

Neither depends on hash functions for its security. Both depend on the hardness of the elliptic-curve discrete logarithm problem, which is exactly what Shor's algorithm solves given a large enough machine. That is the whole of the technical answer: the ledger's authorisation rests on a problem a quantum computer would be able to attack.

This is not a flaw unique to XRP. It describes most of the market, including Bitcoin and Ethereum, and it is the reason the question is asked at all.

## Where a quantum attack would land

An account's public key is not published until the account signs. Until then, the ledger holds an address derived from the key, and an attacker would have to break the hash to reach the key itself.

The first outgoing transaction changes that. The public key travels with the signature so validators can check it, and it stays on the ledger afterwards. From that point the account is protected by the difficulty of deriving a private key from a public one, which is the assumption a quantum machine would remove.

That makes address hygiene the practical defence, exactly as it is elsewhere. An account that has never signed is harder to attack than one that has, and an account that keeps signing from the same key repeatedly is the softest target on the ledger.

## What has been said publicly

Post-quantum cryptography is discussed in most serious blockchain communities, and the XRP Ledger is no exception: the topic appears in research, conference material and public conversation. What that discussion does not do is change what the network accepts today.

The distinction is worth holding firmly. A paper, a proposal or a statement of intent is a plan about a future software version. The signing path is what validators enforce now. Until a post-quantum scheme appears in the transaction format and is accepted by the network, the ledger remains classical regardless of what has been published about it.

That standard should be applied to every project, including this one. [Quantum Resistant Cryptocurrency: The List](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/quantum-resistant-cryptocurrency-list-with-qrl.md) sets out the four checks that separate a deployment from an announcement.

## How QRL differs

QRL signs with XMSS, a hash-based scheme standardised in RFC 8391 and profiled by NIST in SP 800-208. The signature is built from hash computations over a one-time key, so its security rests on the hash function rather than on a number-theory problem. Shor's algorithm has nothing to run against.

The scheme has been in the signing path since QRL's first block in 2018, which means it is not a migration in progress. The cost is statefulness: each signature consumes one key from a tree of 1,024 by default, and the wallet tracks the index. [How XMSS Signatures Work](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/how-qrl-xmss-signatures-work.md) explains the construction and [Why QRL Is Quantum Proof](https://github.com/qrl-wallet/token-facts-and-prices/blob/main/why-qrl-is-quantum-proof.md) covers the reasoning.

There is one boundary to state plainly. QRL's peer-to-peer layer still uses classical key exchange, with post-quantum work in development. The signatures that hold the coins are post-quantum; the transport between nodes is not. [Can Quantum Computers Break Bitcoin?](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/can-quantum-computers-break-bitcoin-and-qrl.md) explains why that separation matters when you assess a whole network.

## What to check before believing a claim

For any chain, ask what a transaction is signed with and find the answer in a specification or in the code, not in a comparison table. Then ask when the scheme entered the signing path. Then ask what the transport uses, and whether the wallet's keys are inside or outside the post-quantum part.

You can do the second check from a block explorer. A live transaction shows its signature format. If the format is elliptic-curve, the chain is classical today, whatever has been said about tomorrow.

QRL is not the right answer for everyone, and the comparison here is deliberately narrow: one scheme against another, on the single question of what happens to signatures if a large quantum computer exists. [How QRL Compares on Quantum Readiness](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/how-qrl-compares-on-quantum-readiness.md) extends that comparison to other projects, and [Is QRL the Same as XRP?](https://github.com/qrl-wallet/token-facts-and-prices/blob/main/is-qrl-the-same-as-xrp.md) deals with the confusion that the two tickers are similar.

## FAQ

### Is XRP quantum resistant?

Not in its live signing path. Accounts sign with ECDSA or Ed25519, both classical elliptic-curve schemes, so the ledger depends on the discrete logarithm problem that Shor's algorithm attacks.

### Does XRP have post-quantum plans?

Post-quantum cryptography is discussed publicly in the XRP Ledger community, as it is across the industry. Discussion and research are not a deployed scheme, and no post-quantum signature is accepted by the network today.

### Is QRL better than XRP?

That is not the question this page answers. QRL's signatures are hash-based and XRP's are elliptic-curve; on the narrow question of quantum exposure, that difference is real. On speed, ecosystem and liquidity, the comparison runs the other way.

### What can an XRP holder do today?

Use a fresh address rather than reusing one, since a key that has signed is public. That is the same advice Bitcoin holders get, and it addresses the same exposure.

<!-- answers: Q062, Q066, Q101, Q105, Q116, Q230 -->
