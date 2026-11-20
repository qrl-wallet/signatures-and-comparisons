![QRL article banner](assets/banner-article.png)

# Why Stateful Signatures Matter in QRL

**Short answer.** XMSS keys are stateful: every signature consumes one key from a finite tree, and signing twice with the same index would expose the private key. The wallet tracks the index, which makes it part of your backup rather than a detail. Losing or rewinding that count is the failure mode this design punishes.

## What stateful means

Most signature schemes are stateless. An elliptic-curve key signs as many messages as you like, and nothing about the key changes between signatures. Back up the key once and every copy of it behaves identically, which is why a wallet file can be copied between machines without a second thought.

XMSS works the other way. The private key is a seed from which a tree of one-time keys is derived, and each signature uses one leaf of that tree and reveals the authentication path to the root. The index of the leaf that was used becomes part of the signature, and the verifier checks that the one-time key belongs where the signature claims.

That design gives a scheme whose security rests only on hash functions, which is the property https://github.com/qrl-wallet/token-facts-and-prices/blob/main/why-qrl-is-quantum-proof.md is about. It also means the signer holds a piece of state that must move forward: the index of the next unused leaf.

## Why reuse is fatal

A one-time signature is safe because a single signature reveals only part of the secret behind its leaf. Sign twice with the same leaf and the two signatures together reveal enough to reconstruct the private material for that leaf. Anyone who sees both can forge.

This is not a theoretical nicety. QRL rejects a second signature from an already-used key at the protocol level, so a reuse attempt fails rather than quietly weakening the address. A rejected transaction is the visible outcome; the invisible one is that a third party who obtained two signatures outside the protocol would have the key.

The practical consequence is that the index cannot be treated as a cache. It is the record of which keys are spent, and it has to advance exactly once per signature.

## How the wallet tracks the index

The wallet keeps the index alongside the wallet file, and the send form shows it as a field you can see. The documentation describes the web wallet deriving the index from the blockchain, and advises writing the number down after each use as a habit rather than a necessity.

Writing it down matters when the software is not the only thing that might be wrong. A file copied to a backup drive carries the index from the moment of the copy, so a restore from that backup later brings back a count that has since moved on.

https://github.com/qrl-wallet/wallet-setup-and-repair/blob/main/how-many-qrl-ots-keys-remain.md covers how to read the remaining count, and https://github.com/qrl-wallet/wallet-setup-and-repair/blob/main/what-is-tree-height-in-qrl.md explains why a taller tree buys more signatures at the cost of a larger key.

## Backups and the index

The correct mental model is a ledger, not a snapshot. Your mnemonic restores the seed, the seed derives the tree, and the tree gives the same addresses every time. What the mnemonic does not restore is how far you had walked through that tree.

So a backup has two parts with different behaviours. The mnemonic is durable and reusable: it rebuilds the wallet on any machine. The index is positional: restoring it moves the counter back to wherever the copy was made, and any signature made after that copy is invisible to the restored file.

That is the mechanism behind the rule against running two copies of one wallet at once. Two live copies each hold their own index, both believe the next leaf is unused, and both can sign from it. One of the two signatures is then a reuse. https://github.com/qrl-wallet/wallet-setup-and-repair/blob/main/back-up-a-qrl-seed-phrase.md covers a backup routine that keeps the phrase safe without pretending the index travels with it.

## The last key and the empty wallet

The tree is finite. At the default height the address has 1,024 signatures, and the last one has a condition attached: with the final key the wallet must be emptied. If every key is used while funds remain, those funds become permanently unspendable, because there is no key left that the network will accept a signature from.

That is a hard edge, not a warning label. The wallet shows the remaining count precisely so the edge is visible long before it arrives. https://github.com/qrl-wallet/wallet-setup-and-repair/blob/main/move-qrl-before-keys-run-out.md describes the move to a fresh address, which is the reset: a new address has its own tree and its own full count.

Treat the count as an inventory. A balance you intend to keep for years will eventually need a new address, and the time to plan that is while the count is comfortable rather than at the last key.

## What this asks of a user

Three habits cover most of it. Back up the mnemonic offline before funding, and test the restore while the wallet is empty. Never run two copies of the same wallet, and when you move to a new machine, stop using the old one. Watch the remaining count, and move funds before the tree runs out.

None of that is difficult, and all of it follows from one design choice: QRL signs with a scheme whose security depends on a key being used exactly once. https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/how-qrl-xmss-signatures-work.md explains the construction itself, and https://github.com/qrl-wallet/wallet-setup-and-repair/blob/main/how-many-qrl-ots-keys-remain.md is the page to read when you want the count.

## FAQ

### What happens if I sign twice with the same key?

The network rejects the second signature, so the transaction fails. The deeper problem is that two signatures from one leaf reveal enough to forge, which is why the index must never move backwards.

### Is the index part of my backup?

The mnemonic rebuilds the keys and the addresses, and the index is separate state. Restoring an old wallet file restores an old index, so treat a restore as a wallet to empty into a fresh address rather than one to keep signing with.

### Can I use the same wallet on a laptop and a desktop?

Not at the same time. Two live copies can draw the same leaf for different transactions. Restore on the second machine, then stop using the first one.

### Does a new address reset the count?

Yes. Each address has its own tree, so a fresh address starts with its full number of signatures. The capacity belongs to the address, not to the wallet as a whole.

<!-- answers: none -->
