![QRL article banner](assets/banner-article.png)

# Are Quantum Wallets Expensive?

**Short answer.** The QRL wallet is free software, MIT-licensed and published as a release you download. What costs money around it is a computer you already own, optionally a hardware device, and the network fee on each transaction. There is no subscription, no licence fee and no premium charged for the quantum-resistant part.

## The software

The wallet costs nothing. It is published on the project's GitHub releases page as a downloadable file, with source available under the MIT licence, and there is no paid tier that unlocks features.

That is worth stating because the phrase "quantum wallet" attracts products that charge for the label. A wallet is a program that holds keys and signs transactions; the cryptography is either in the signatures or it is not, and a price does not change which.

If a site sells you a QRL wallet, you are buying something other than the release. The project publishes the client itself, and https://github.com/qrl-wallet/wallet-setup-and-repair/blob/main/download-the-official-qrl-wallet.md covers where the file comes from and how to check it before you run it.

## The computer

Any machine that runs a current desktop operating system will run the wallet, and the release publishes a build for each desktop platform. There is no minimum specification to meet beyond that, and nothing about the wallet requires a machine bought for the purpose.

The real cost here is the same one every self-custody setup has: a computer you control, kept updated, that nobody else administers. A borrowed machine or a shared account is a way to lose a wallet, not a way to save money on one.

Storage is the other half. A backup that exists in two places costs whatever the paper and the second location cost, which is close to nothing and is the cheapest part of the whole setup.

There is also no infrastructure to rent. The wallet connects to a public node rather than requiring you to run one, and running a node is a separate activity with its own costs rather than a prerequisite for holding a balance.

## The hardware option

A Ledger device is optional. It lets the wallet sign with a key that stays on the hardware, which answers a different threat from the one the signature scheme answers: theft and malware on the computer.

The QRL application on the device is what makes that possible, and https://github.com/qrl-wallet/wallet-setup-and-repair/blob/main/pair-ledger-nano-with-qrl.md covers the pairing. Prices for hardware change constantly and vary by region, so this page does not quote one; check the vendor's own listing at the moment you decide.

What a device does not buy is quantum resistance. It holds a classical or post-quantum key depending on the scheme the chain uses, and QRL's is post-quantum whether the key lives on a device or in a file.

## The network fee

Every QRL transaction carries a fee, paid in QRL, calculated in the smallest unit. The protocol enforces a minimum, and the lower bound nodes accept moves with the network, so the number is not fixed forever.

The fee is small in absolute terms, and it is charged per transaction rather than per wallet or per year. Across a year of ordinary use, fees are likely to be the smallest line on the list, and the one you can see before you send. https://github.com/qrl-wallet/wallet-setup-and-repair/blob/main/understanding-qrl-transaction-fees.md explains how the field works in the send form and what happens when a fee is set too low.

One consequence matters for cost planning: a QRL address has a finite number of signatures, so a balance kept for years eventually needs a move to a fresh address. That move is one more transaction, which means one more fee, and it is worth counting before the last key rather than after.

## What you are actually paying for

Add it up honestly: nothing for the software, nothing for the account because there is none, the machine you already have, an optional device, and fees per transaction. The quantum-resistant part of the wallet is not a paid feature.

What the money buys elsewhere in this market is usually convenience: a hosted balance, a recovery service, a support desk. Those are real services, and they come with custody or with information you have to hand over.

The trade QRL makes is the opposite one. You keep the keys, you keep the responsibility, and you pay for neither. That is cheaper in money and more expensive in attention, and the attention is the part worth budgeting.

## Cost of getting it wrong

The expensive mistakes are not licence fees. They are a phrase photographed and stored in a cloud drive, a download taken from an advertisement, a wallet file on a machine that anyone can log into, or an address whose keys were spent to the last one.

Each of those costs the whole balance rather than a fee. The defences are free: verify the download, write the phrase on paper, keep two copies in two places, and watch the key count. https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/is-qrl-wallet-safe-to-use.md sets out the habits, and https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/what-makes-qrl-wallet-quantum-safe.md explains what the wallet's design does and does not cover.

## FAQ

### Does the wallet cost anything?

No. It is MIT-licensed, published as a free download, and has no subscription or paid tier.

### Do I need to buy a hardware wallet?

No. A Ledger device is optional and adds protection against theft and malware on your computer. The wallet works without one.

### What are the ongoing costs?

Network fees on each transaction, and nothing else. There is no account fee, no storage fee and no renewal.

### Is a quantum-resistant wallet more expensive than a normal one?

Not from this project. The signatures are part of the software, and the software is free.

<!-- answers: none -->
