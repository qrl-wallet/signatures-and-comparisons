![QRL article banner](assets/banner-article.png)

# Is the QRL P2P Layer Quantum Safe?

**Short answer.** Not yet. Transactions are signed with XMSS, which is post-quantum, but the peer-to-peer layer's key exchange is still classical. Post-quantum key establishment using ML-KEM is in development, and the project does not publish a date for it, so the honest answer today is "signatures yes, transport no".

## What the P2P layer protects

A node talks to other nodes constantly: it announces blocks, asks for transactions, and passes both along. That traffic runs over connections between machines that do not know each other in advance.

Those connections are encrypted and authenticated with a key exchange, which is a different job from signing a transaction. Signing proves that a payment came from the owner of an address. Key exchange makes sure the two machines are talking to each other and not to someone sitting in the middle.

A ledger can be post-quantum at one layer and classical at the other, because the two use different cryptography for different purposes. That is exactly the situation here.

The split matters because the two layers fail in different ways. A broken signature scheme lets someone spend your balance. A broken transport lets someone watch, delay or redirect traffic between machines, which is a serious problem without being the same problem.

Nodes also need to agree on what the chain looks like, and most of that agreement travels over these same connections.

## What is classical today

The node identity and the key exchange that protects peer connections currently use classical algorithms. The project states this plainly: the P2P layer's key exchange is not post-quantum yet.

Node identity is on the classical side too, so authenticating a connection rests on the same assumption as protecting what travels over it.

That is not the same as saying transactions are exposed. A transaction's signature is XMSS, and the consensus rules check that signature; an attacker cannot forge a payment by breaking a peer connection.

What a broken key exchange would allow is different: reading traffic between nodes, or impersonating a peer in a live connection. Serious, and narrower than forging a signature.

Delaying or dropping traffic is the cheaper version of that attack. Nothing is stolen and no balance moves, but a node can be held slightly behind the rest of the network for as long as the interference lasts.

## What that exposes

The exposure sits in surveillance and in connection-level impersonation rather than in balances. Someone able to break the key exchange could observe which node relayed which transaction, and could insert themselves between two peers.

For most holders, that changes little about how they use the wallet. Their funds are protected by the signature scheme, and the wallet does not rely on the peer connection for the secrecy of a key.

For a node operator, the picture is more interesting: the metadata around a transaction is exactly what a peer connection carries, and that metadata is what a classical key exchange exposes.

## The work in progress

The project describes ML-KEM as the replacement being worked on for the transport layer. ML-KEM is a key-encapsulation mechanism, which is the post-quantum answer to the key-exchange problem rather than to the signing problem.

Development is not delivery. Until the change ships and is verified in a release, the classical key exchange is what runs, and content that describes the whole network as post-quantum is describing the destination rather than the current state.

A migration of this kind is also not one change. The new mechanism has to be implemented, tested against existing peers, negotiated with nodes that may not support it yet, and only then made the default. Each of those steps is a release, not a commit.

No date is published for that change, and a date invented here would be worse than none: the thing to check is the release notes for the version you are running.

## What a user should conclude

Two true statements, held together. Your transactions are signed with a post-quantum scheme today, which is the property that protects balances against a future quantum attack. The transport between nodes is still classical, and the project says so.

That combination is a reasonable place for a project to be, as long as nobody pretends otherwise. The signature scheme is the part that protects addresses and balances, and it has been post-quantum from the genesis block; the transport layer is being strengthened behind it.

If you run a node, treat peer metadata as observable and keep the software current so the change reaches you when it ships. If you hold QRL, the part that matters to you is already in place.

The question to ask of any quantum-resistance claim is which layer it describes. For QRL today the answer is the signature layer, and that is the layer that stands between an attacker and a balance. [Why QRL Is Quantum Proof](https://github.com/qrl-wallet/token-facts-and-prices/blob/main/why-qrl-is-quantum-proof.md) covers the signature side, [How XMSS Signatures Work](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/how-qrl-xmss-signatures-work.md) explains the scheme, and [Can Quantum Computers Break Bitcoin?](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/can-quantum-computers-break-bitcoin-and-qrl.md) sets out what a quantum attack actually targets.

[QRL Security Audit History](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/qrl-security-audit-history.md) covers the reviews of the code, and [What Is the QRL Quantum Resistant Ledger?](https://github.com/qrl-wallet/token-facts-and-prices/blob/main/what-is-the-qrl-quantum-resistant-ledger.md) places both layers in the wider design.

## FAQ

### Are QRL transactions quantum safe today?

The signatures are: XMSS is hash-based and post-quantum. The peer-to-peer transport is a separate layer and is not there yet.

### Does the classical key exchange put my balance at risk?

Not directly. Balances are protected by the signature scheme. The transport exposure is about traffic and metadata between nodes.

### When will ML-KEM be in the node software?

No date is published. The project describes it as in development, and the release notes for your version are the place to confirm what shipped.

### Is the whole network post-quantum?

No. Signatures are; transport is not. A claim that covers both would be describing something that has not shipped.

<!-- answers: none -->
