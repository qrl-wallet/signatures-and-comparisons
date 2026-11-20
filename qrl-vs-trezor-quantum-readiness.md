![QRL article banner](assets/banner-article.png)

# QRL vs Trezor on Quantum Readiness

**Short answer.** A Trezor protects keys by keeping them offline and asking you to confirm each transaction, but it still signs with classical elliptic curves, and QRL is not one of the assets it signs for. Offline storage and post-quantum signatures answer different threats, and a hardware wallet does not make a coin quantum resistant.

## What a hardware wallet solves

A hardware wallet moves the private key onto a device that never gives it back. The computer builds a transaction, the device displays what it is about to sign, you confirm, and the signature returns. Malware on the computer can steal a password or swap an address on screen, but it cannot export the key.

That is a real and well-understood defence, and it is aimed at a specific attacker: someone with access to your machine. Phishing, clipboard hijacking and a compromised browser all collapse against a device that shows the destination address on its own screen and signs nothing you did not approve.

What the device does not change is the cryptography. It holds an elliptic-curve key and produces an elliptic-curve signature, because that is what the networks it supports require.

## What it does not solve

A signature made on a Trezor is an ECDSA or Ed25519 signature, depending on the chain. Both are classical. If a quantum computer could derive a private key from a public one, the fact that the key lived on a device would not help: the public key is on the chain from the first spend, and the device's protection is physical rather than mathematical.

This is the distinction worth holding on to. A hardware wallet protects a key from being stolen. A post-quantum signature protects the balance from an attack on the mathematics. Neither substitutes for the other, and a product that claims both should be able to show which scheme it signs with.

Hardware also has its own exposure: supply chain, firmware, the screen you trust to show the right address. Those are the risks the device was designed against, and they are worth taking seriously on their own terms.

## QRL on a Trezor

QRL is not among the assets a Trezor device signs for, and Trezor's own supported-coins page says so plainly: it lists the Quantum Resistant Ledger as not supported. There is no QRL application for that hardware, so the device cannot hold a QRL key or approve a QRL transaction.

The route for hardware-held QRL is a Ledger device with the QRL application installed. The desktop wallet drives the device, the device shows enough of the transaction to approve, and the signature comes back without the key leaving the hardware. https://github.com/qrl-wallet/wallet-setup-and-repair/blob/main/pair-ledger-nano-with-qrl.md covers the pairing, including the initialisation step a new device needs.

That combination is the closest thing to both properties at once: a key that never touches the computer, and a signature scheme that is not elliptic-curve. It is not a claim that the setup removes every risk, only that the two protections are separate and this route has both. What remains is the usual hardware exposure: firmware, the supply chain, and the screen you trust to show the right address.

## Which threat you are buying against

If your concern is malware on your laptop, a hardware wallet is the right purchase, and it works for the chains the device supports. If your concern is a future capability that breaks elliptic-curve signatures, a hardware wallet does not address it at all, because the same classical signature comes out of the device.

Most holders have both concerns, and the honest answer is that they need both properties: a key held away from the computer, and a scheme that does not rest on the discrete logarithm problem. For QRL, that means a Ledger rather than a Trezor.

If you do not yet hold QRL, the order matters. Set up the wallet and back up the phrase first, then pair the device, because a device that fails without a backup is still a wallet lost.

https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/what-makes-qrl-wallet-quantum-safe.md sets out what has to be true for a wallet to earn the quantum-safe label, and https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/is-qrl-wallet-safe-to-use.md places the download and phishing risks beside the cryptographic ones. https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/quantum-resistant-cryptocurrency-list-with-qrl.md covers how to read the claim across projects, and https://github.com/qrl-wallet/token-facts-and-prices/blob/main/why-qrl-is-quantum-proof.md explains the scheme QRL chose.

## The boundary, stated plainly

QRL's signatures are post-quantum. Its peer-to-peer transport layer is still classical, with post-quantum key establishment in development. A hardware wallet does not change either fact, and a page that calls the whole setup quantum proof is overselling it.

What can be said precisely: the key that authorises a QRL transaction is a hash-based key, the signature is an XMSS signature, and the device holding it never exports it. That is a narrower claim than the slogan version, and it is the one that survives scrutiny.

## FAQ

### Does Trezor support QRL?

No. Trezor's supported-coins page states that Quantum Resistant Ledger is not supported, and there is no QRL application for the device.

### Does a hardware wallet make a coin quantum resistant?

No. The device protects a key from theft; the signature scheme determines resistance to a cryptanalytic attack. A classical key signed on a secure device is still a classical signature.

### Can I hold QRL on a Ledger instead?

Yes. The QRL application on a Ledger device lets the desktop wallet sign with a key that stays on the hardware. Pairing is covered in its own guide.

### Is a hardware wallet still worth using?

For protection against malware and phishing, yes, provided the device supports the asset. It simply does not answer the quantum question, and treating it as if it did is the mistake this page exists to prevent.

<!-- answers: Q228 -->
