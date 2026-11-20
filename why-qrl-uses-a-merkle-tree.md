![QRL article banner](assets/banner-article.png)

# Why QRL Uses a Merkle Tree

**Short answer.** A tree is what makes many one-time keys usable under a single address. The root is published once as the public key, and each spend proves its key with a short path of hashes leading back to that root. Without the tree, every key would need its own address and its own backup.

## The problem a tree solves

A hash-based key signs once. That is a property of the construction, not a limitation the wallet can wish away, so an address that is meant to be used more than once needs many keys.

The naive answer is to publish every one-time public key, which is unusable: the address would be enormous, and a verifier would have to check against a list that changes as keys are spent. At the default size that list holds 1,024 hash outputs, so the address would be a document rather than a string.

The Merkle tree answers it with a single commitment. Publish one value that depends on all the keys, and let each spend prove that its key is one of the committed ones. The address stays one fixed string, and the proof travels with the signature.

## Root as public key

The leaves of the tree are the one-time public keys. Pairs of leaves are hashed together into parents, pairs of parents are hashed again, and the process repeats until one value remains: the root.

That root is the address's public key, and the address is derived from it. The commitment is total: alter any leaf and every hash above it changes, so the root cannot be made to fit a tree it did not come from.

This is why the tree is fixed when the address is created. The root exists from that moment, and the leaves underneath it do too. There is no adding a leaf later without changing the root and therefore the address.

Because the root comes from the seed, it can be rebuilt anywhere. The same mnemonic produces the same leaves and the same root, which is what makes a restored wallet show the same address.

## The authentication path

To spend a leaf, the signer sends the leaf's one-time signature plus the siblings it needs to walk up the tree.

At each level the verifier hashes the current value together with its sibling, producing the parent, then moves up. Ten levels means ten hashes in sequence, ending at a value that must equal the root.

That path is the proof. It says "this key is under this root" without listing the other 1,023 keys, and it reveals nothing about the leaves that are not on the path.

## Cost per signature

The path is the price of the tree. A taller tree holds more keys and makes every signature longer, because there are more levels to climb.

For a height of 10 the path has ten entries, which is small enough that the cost is dominated by the one-time signature itself rather than the proof around it. That is a large part of why the default height is a practical choice rather than an arbitrary one.

The path also has to be carried with each transaction, and producing it depends on the leaves' positions in the tree, so the wallet assembles it when it signs.

Verification work grows with height, linearly, and not with how many leaves have been used. A wallet at its first signature and one at its thousandth verify in the same number of steps.

## Height and capacity

A tree of height h has 2 to the power of h leaves. Height 10 gives 1,024, which is the default for a QRL address; height 11 would give 2,048 and a longer path.

Height is set when the wallet is created and is not changed for an address that already exists, because changing it would mean a different root and therefore a different address.

Capacity is the limit that follows. An address can sign as many times as it has leaves, and no more, which is why the count matters and why https://github.com/qrl-wallet/wallet-setup-and-repair/blob/main/what-is-tree-height-in-qrl.md and https://github.com/qrl-wallet/wallet-setup-and-repair/blob/main/how-many-qrl-ots-keys-remain.md are the two pages to read together.

Creating an address therefore generates every leaf up front. The 1,024 keys exist before the first signature is made, which is why address creation takes a moment and why a taller tree takes longer still.

## Why not a different structure

Other arrangements exist, and the alternatives are covered on their own pages. What the tree gives QRL is a single published value, a proof that grows logarithmically with capacity, and a construction built only from hashes.

That combination is what the standard describes: XMSS is a Merkle tree of one-time keys with a defined one-time signature underneath.

A flat list would need a proof that grows with capacity, so a thousand signatures would mean a thousand hashes in the proof. The tree keeps that logarithmic, which is what makes the larger capacity practical rather than theoretical.

https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/how-qrl-xmss-signatures-work.md covers the signature end to end, https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/what-is-a-qrl-hash-based-signature.md covers the hash assumption, and https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/why-stateful-signatures-matter-in-qrl.md covers why the wallet has to remember where it is in the tree.

## FAQ

### Can more keys be added to an existing address?

No. The root fixes the leaves, so adding a leaf would produce a different root and a different address.

### What does the authentication path do?

It proves a one-time key belongs to the tree, using only the sibling hashes on the way to the root.

### Why does a taller tree make signatures bigger?

Because the path has one entry per level, so more levels mean more hashes carried with each signature.

### Is the tree the same as the address?

The address is derived from the tree's root. The tree itself is the key material underneath it.

<!-- answers: none -->
