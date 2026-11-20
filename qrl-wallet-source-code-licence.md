![QRL article banner](assets/banner-article.png)

# QRL Wallet Source Code and Licence

**Short answer.** The wallet is MIT-licensed and its source is public, so you can read it, build it and run a build you compiled yourself. MIT permits reuse and modification and comes with no warranty. The licence is a permission rather than a security claim: it lets you check the software, and checking is your job.

## The licence

The repository carries an MIT licence, identified as SPDX MIT in its licence metadata. That is one of the shortest and most permissive licences in common use.

In practice it grants the right to use, copy, modify, merge, publish, distribute, sublicense and sell copies of the software, provided the copyright notice and the licence text travel with it.

What it does not contain is an explicit patent grant. That is a difference from longer licences such as Apache 2.0, and it is the kind of detail worth knowing if you plan to build a product on the code rather than just read it.

It also states that the software comes with no warranty. That sentence is not boilerplate to skip: it means the authors are not promising that the code works, and the risk of running it sits with you.

## Where the source lives

The repository is public, with the application code, the release assets and the issue tracker in the same place. You can read the code that handles a wallet file before you trust a wallet file.

The issue tracker is part of that picture. Bugs that were reported and fixed, and reports that are still open, are visible there, which is often more informative than a summary of the project's quality.

The releases page is where the builds come from, and each asset is named for its platform and architecture. The build you install and the source you read should be the same version; a source tree from one release does not describe a binary from another.

The project states that releases publish SHA-256 checksums and GPG signatures. The latest release's asset list does not include a separate checksum file, so the value to compare against is the one published alongside the release; [Verify the QRL Installer](https://github.com/qrl-wallet/wallet-setup-and-repair/blob/main/verify-the-qrl-installer.md) describes the comparison.

## Building it yourself

With the source and a toolchain, you can compile the application rather than run someone else's binary. That is the strongest form of "I know what this program does", because the code you read is the code you run.

It is also more work than most people want, and it does not make the result identical to the published build by default. Comparing your binary with the release byte for byte only works where the build is reproducible, which is not something to assume without checking.

The practical version of this is a toolchain, the source at the matching tag, and the build steps the repository documents. If those steps are unclear for your platform, that is a reason to use a published asset with a checked hash rather than to improvise a build.

What a self-built copy gives you is independence from the download path: no lookalike page, no substituted file, no trust in a mirror. What it does not give you is a second opinion on the code, which is what a review provides.

[Run QRL Wallet on Linux](https://github.com/qrl-wallet/wallet-setup-and-repair/blob/main/run-qrl-wallet-on-linux.md) covers the platform where building from source is most common, and [QRL Security Audit History](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/qrl-security-audit-history.md) covers the reviews of the code itself.

## What MIT permits

Anyone can fork the wallet, change it, and publish the result under the same licence. That is the point of a permissive licence, and it is also why a modified build is not the same product.

A fork can change how keys are handled, add a fee, or remove a confirmation step. The licence allows all of it, and the project does not review what other people publish.

So the licence tells you the code is available; it does not tell you that every build claiming to be QRL is the one the project published. That distinction is the reason the hash check exists.

The same licence is why the code can be audited by anyone, not only by the firm the project hired. A reader with the time can check the claim rather than take it.

## Why this matters for a wallet

A wallet is a program that holds the thing an attacker wants. Closed-source wallets ask you to trust a binary; open-source wallets ask you to trust a process you can inspect.

That process has parts: the code is public, the licence permits reading and rebuilding, the reviews are listed with dates and each report carries its own scope, and the releases carry a value you can check. Each part is verifiable on its own.

None of it removes the need for care. A reviewed, MIT-licensed wallet installed from the wrong page is still the wrong program, and a correct build still hands everything to whoever reads your phrase.

The licence also settles a question people ask about trust: you are not relying on the authors' goodwill to inspect the software, because the terms allow it. Whether you do the inspecting, or pay someone to, is a separate decision. [Is the QRL Wallet Safe to Use?](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/is-qrl-wallet-safe-to-use.md) puts those pieces together, and [Who Created the QRL Network?](https://github.com/qrl-wallet/token-facts-and-prices/blob/main/who-created-the-qrl-network.md) covers who maintains the project.

## FAQ

### What licence is the wallet under?

MIT, identified as SPDX MIT in the repository's licence metadata.

### Can I sell a modified version?

The licence permits redistribution and modification, provided the copyright notice and licence text travel with it. A modified build is not the project's release.

### Does the licence mean the code is secure?

No. It means the code can be read. Security comes from the code being correct, from review, and from how it is used.

### Are the release downloads signed?

The project states that releases publish SHA-256 checksums and GPG signatures. The latest asset list has no separate checksum file, so use the value published with the release.

<!-- answers: Q178 -->
