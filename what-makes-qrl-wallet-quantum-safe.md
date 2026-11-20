![QRL article banner](assets/banner-article.png)

# What Makes a Wallet Quantum Safe?

**Short answer.** A wallet is quantum safe when the keys it signs with are post-quantum and the software handles them correctly. QRL's wallet signs with XMSS, keeps the keys on your machine and manages the one-time key index, which is why the label applies to it and not to a wallet that only stores classical keys offline.

## The four things that have to be true

The phrase gets applied to products that satisfy one of these conditions and fail the others, so it is worth separating them.

First, the signature scheme must not depend on factorisation or discrete logarithms. A hash-based or lattice-based scheme survives Shor's algorithm; an elliptic-curve one does not, however well it is implemented.

Second, the key must be generated and stored where you control it. A custodial service holds the key, which means the scheme protects the provider's balance rather than yours.

Third, the software must handle the scheme's requirements correctly. A stateful scheme needs an index that never repeats and never rewinds, and a wallet that gets that wrong is unsafe in a way no algorithm choice can fix.

Fourth, the backup must restore what the scheme needs. With a stateful scheme that includes the position in the key sequence, not just the seed.

All four are properties of the running software, which is why the question "is this wallet quantum safe" cannot be answered from a specification alone.

## Signature scheme

QRL signs with XMSS, standardised in RFC 8391 and profiled by NIST in SP 800-208. The private key is a seed from which a tree of one-time keys is derived, and each signature uses one leaf and reveals the path to the root. Security rests on the hash function.

Shor's algorithm has nothing to attack in that construction, because there is no hidden subgroup to find. Grover's algorithm gives a quadratic speedup for search, which is why hash lengths are chosen with margin, and that is a margin question rather than a break.

[How XMSS Signatures Work](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/how-qrl-xmss-signatures-work.md) covers the mechanics, and [Why QRL Is Quantum Proof](https://github.com/qrl-wallet/token-facts-and-prices/blob/main/why-qrl-is-quantum-proof.md) covers why the project chose this scheme over a lattice-based alternative.

## Key handling and the index

The wallet creates keys on your machine, encrypts them in a wallet file with a password you choose, and never registers anything with a server. There is no account and no email address, which means there is also no support desk that can reset a password.

The index is the part that makes QRL's wallet different from most. Each address has 1,024 signatures at the default tree height, and the index records which key comes next. Signing twice with the same index would expose the private material for that leaf, so the network rejects a repeated signature and the wallet tracks the count.

That is a real operational requirement, and [How Many QRL OTS Keys Remain?](https://github.com/qrl-wallet/wallet-setup-and-repair/blob/main/how-many-qrl-ots-keys-remain.md) explains how to read the count. A wallet is quantum safe only if it also handles this correctly; choosing the scheme does not by itself deliver the behaviour.

## Backup, and what it has to contain

The mnemonic rebuilds the seed and therefore every address the wallet ever derived. What it does not rebuild is how far you had walked through the tree. Restoring an old wallet file restores an old index, and signing from it can hand out a key that has already signed.

So the backup has two parts with different behaviour: the phrase, which is durable and reusable, and the index, which is positional. That is why restoring a backup to a second machine while the first is still in use is dangerous rather than convenient, and why a restored old file is best treated as a wallet to empty into a fresh address.

[Is the QRL Wallet Safe to Use?](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/is-qrl-wallet-safe-to-use.md) covers the download and phishing side of safety, which sits beside this and is not replaced by it.

## What the label does not cover

QRL's peer-to-peer layer still uses classical key exchange, with post-quantum key establishment in development. A wallet that signs post-quantum still talks to nodes over a transport that is not, and that is a separate exposure worth knowing about.

The label also does not cover you. A wallet whose phrase is photographed, typed into a website or stored in a cloud note is compromised regardless of its cryptography. The scheme protects the mathematics; the habits protect the key.

And it does not cover the download. A genuine wallet installed from a tampered file is a different program, which is why the digest on the release page matters as much as the signature scheme.

## How to test a claim

Ask what scheme signs a transaction, and find it in the specification rather than on a comparison table. Ask where the key is generated and stored. Ask how the software handles the scheme's state, if it has any. Ask what the backup restores. Ask which parts of the network the claim excludes.

A project that answers all five has earned the label. A project that answers with the label has not, and the questions are cheap to ask.

[Quantum Resistant Cryptocurrency: The List](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/quantum-resistant-cryptocurrency-list-with-qrl.md) applies that test across projects, and [Are Quantum Wallets Expensive?](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/are-qrl-wallets-expensive.md) covers what the software costs, which is nothing.

## FAQ

### Does a wallet need to be open source to be quantum safe?

Not strictly, but you cannot verify the scheme or the key handling without reading the code or trusting someone who did. QRL's wallet is MIT-licensed and its source is public.

### Is a hardware wallet quantum safe?

Only if the scheme it signs with is post-quantum. A device that holds a classical key signs classical signatures, however well it protects the key from theft.

### What happens if the key index is lost?

The phrase restores the keys but not the position in the sequence, so a restore must be treated carefully. Signing from a rewound index can reuse a key, which the network rejects and which exposes the leaf to anyone who saw both signatures.

### Does the P2P layer make the wallet unsafe?

It is a real limitation, not a reason to avoid the wallet. The signatures protecting balances are post-quantum; the transport between nodes is not yet, and the project says so.

<!-- answers: Q034, Q039, Q040, Q041, Q049, Q051, Q128, Q129, Q130, Q134, Q135, Q182, Q238, Q239, Q264 -->
