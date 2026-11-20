![QRL article banner](assets/banner-article.png)

# Can Quantum Computers Break Bitcoin?

**Short answer.** A quantum computer large enough to run Shor's algorithm could recover a private key from an exposed elliptic-curve public key, and that is how Bitcoin and most other chains sign today. QRL's signatures rest on hash functions instead, so that particular attack does not apply to them. No machine of that size is known to exist, and no credible date for one has been published.

## What Shor's algorithm breaks

Shor's algorithm solves two mathematical problems that classical computers cannot solve efficiently: integer factorisation and the discrete logarithm. Most public-key cryptography in use today is built on one of them.

RSA rests on factorisation. Elliptic-curve signatures, which Bitcoin uses, rest on the discrete logarithm over a curve. A machine running Shor's algorithm with enough stable qubits could take a public key and produce the matching private key. Nothing about that attack is speculative in principle: it is a known algorithm, and the engineering is the open question.

The distinction that matters for a wallet is which problem its signatures depend on. A scheme built from hash functions depends on neither factorisation nor discrete logarithms, so Shor's algorithm gives an attacker nothing to run against it.

## Which keys are exposed and when

A Bitcoin address does not publish its public key when it receives coins. It publishes a hash of it. That is why an address that has only received is relatively well protected: an attacker with a quantum computer would first have to break the hash to reach the key.

The exposure starts when you spend. A transaction carries the public key so that nodes can check the signature, and from that moment the key is on the chain permanently. Coins sent to that address later sit behind a key that is already public. Address reuse is therefore the behaviour that turns a future capability into a present risk.

Older outputs are a second category. Early Bitcoin outputs paid to a public key directly rather than to an address hash, so their keys have been visible since the day they were created. Any honest assessment of the risk has to separate those coins from coins held in addresses that have never signed.

## Why the timeline is unknown

Building a machine that runs Shor's algorithm at cryptographic scale is not a matter of adding qubits. The qubits have to be stable, error-corrected and available in large numbers for long enough to complete the computation. Published estimates vary by orders of magnitude, and they depend on engineering assumptions rather than on a proven design.

That is why no date belongs in a serious answer. A date is a prediction about hardware, funding and engineering at once, and the people closest to the work decline to give one. The useful posture is to ask what happens to your holdings if the capability arrives, not to argue about which year it arrives in.

There is also a quieter risk that arrives earlier than a full break: data recorded today can be attacked later. A public key that is already on a chain does not need to be captured again when the hardware improves.

## What QRL does instead

QRL signs with XMSS, a hash-based scheme standardised in RFC 8391 and profiled by NIST in SP 800-208. A signature is built from hash computations over a one-time key, and its security rests on the hash function rather than on a hard number-theory problem. Shor's algorithm has no purchase on it.

The trade is that the keys are stateful. Each signature consumes one key from a tree of finite size, 1,024 by default, and the wallet tracks which one comes next. [How XMSS Signatures Work](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/how-qrl-xmss-signatures-work.md) explains the construction, and [Why Stateful Signatures Matter in QRL](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/why-stateful-signatures-matter-in-qrl.md) covers what that discipline asks of a holder.

QRL has run this scheme since its 2018 launch rather than announcing it as future work. Its cryptography has been reviewed by external firms in 2018 and again in 2026, and [QRL Security Audit History](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/qrl-security-audit-history.md) sets out what each review covered.

## What the label does not cover

A post-quantum signature does not make every part of a network post-quantum. QRL's peer-to-peer layer still uses classical key exchange, with post-quantum key establishment in development. That is a transport risk rather than a signature risk, and [Is the QRL P2P Layer Quantum Safe?](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/is-qrl-p2p-layer-quantum-safe.md) treats it on its own terms.

It is also worth being precise about what a quantum machine would and would not do to a hash-based chain. Grover's algorithm gives a quadratic speedup for search, which is why the usual estimate is that a 256-bit hash retains roughly the security of a 128-bit one against it. That is a margin question, not a break, and it is the reason hash lengths are chosen with room to spare.

## What a Bitcoin holder can do today

The practical advice does not depend on a date. Stop reusing addresses, because a fresh address per payment keeps your public key off the chain until you spend. Treat a spent address as exposed and move the remaining balance to a new one. Avoid typing an address you have not checked, since that risk is live now while the quantum one is not.

For a balance you intend to hold for years, the question becomes which signature scheme protects it. [Quantum Resistant Cryptocurrency: The List](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/quantum-resistant-cryptocurrency-list-with-qrl.md) sets out how to read that claim across projects, and [Why QRL Is Quantum Proof](https://github.com/qrl-wallet/token-facts-and-prices/blob/main/why-qrl-is-quantum-proof.md) explains the reasoning behind the scheme QRL chose.

## FAQ

### Is Bitcoin already broken?

No. No quantum computer has been shown to break elliptic-curve signatures at cryptographic scale, and Bitcoin's signatures are unchanged. The exposure is a future capability applied to keys that are public today.

### Does a quantum computer break the hash in a Bitcoin address?

Not in any practical sense. Shor's algorithm does not apply to hashes, and Grover's search gives only a quadratic speedup, which a longer hash is chosen to absorb.

### Why does address reuse matter more than the machine?

Because a spent address has already published its public key. The attacker then needs only the machine, not a second step. An address that has never signed still hides its key behind a hash.

### Does QRL protect the whole network, or only the signatures?

Only the signatures, and that is the part holding the coins. The peer-to-peer transport is still classical, with post-quantum key establishment in development.

### Is there a date for a machine that could do this?

No credible one has been published. Estimates of the engineering effort vary widely, and the honest answer is that the timeline is unknown.

<!-- answers: Q065, Q099, Q119, Q232, Q260, Q261, Q262, Q271 -->
