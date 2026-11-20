![QRL article banner](assets/banner-article.png)

# QRL Security Audit History

**Short answer.** QRL's cryptography and wallet have been reviewed by external firms: Red4Sec and x41 D-Sec in 2018, and Halborn in 2026. The project reports no cryptographic vulnerabilities in the current post-quantum library. An audit is a point-in-time examination of a stated scope, which is the honest measure of what any of those reviews can tell you.

## The 2018 reviews

Two firms reviewed the project in 2018, the year the network launched: Red4Sec and x41 D-Sec. What each of them examined is stated in its own report; the security page records the firms and the year rather than summarising a scope.

That timing matters. A 2018 review speaks to the implementation as it stood in 2018, against the code that existed then. It tells you that people outside the project examined it at that stage, and it tells you nothing about code written in 2026.

The reviews are usually described by the names of the firms, which is the right level of detail for a reader: who looked, in which year, and at what. Anything beyond that needs the report itself, because a summary cannot tell you what was in scope.

Two firms rather than one is also worth noticing. Two reports from the same year describe two sets of eyes; whether their scopes overlapped is a question for the reports themselves rather than for a summary of them.

## The 2026 review

Halborn reviewed the project again, in March 2026, with the current post-quantum library in scope. The project's own summary of the outcome is that no cryptographic vulnerabilities were found in that library.

That is the project speaking about its own review, and it should be read that way. The stronger claim is the one the report makes, and the report is the document to check if the distinction matters to you.

What the 2026 date buys is relevance. Code that did not exist in 2018 could not have been reviewed in 2018, so a recent review of the current library is the one that describes what is running now.

## What each covered

The three reviews were not the same exercise. The 2026 review is described as covering the current post-quantum library; for the 2018 work the scope lives in the reports, and a reader who needs it should go there rather than assume it matched the later one.

Scope is the first thing to look for in any report, and it is usually stated in the opening pages: which components, which versions, which parts explicitly excluded. A review of a cryptographic library is not a review of the wallet interface, and a review of the wallet is not a review of the consensus code.

Reading the scope also tells you what a "no findings" summary means. A clean report on a narrow scope is a clean report on that scope, and the same document can be silent on everything outside it.

Versions matter as much as components. A report names the code it examined, and the code in a later release has been edited since: fixes, dependencies, build changes. The report describes the version it saw, which is why the date on its cover is part of the finding.

## What an audit does not prove

An audit does not make software permanently safe, and it does not cover code written after it finished. Every review is a snapshot with a date on it.

It also cannot replace the checks you make yourself. A reviewed installer that you downloaded from a lookalike page is still the wrong file, and a reviewed wallet still hands its keys to anyone who reads your seed phrase.

What a review cannot do either is keep watching. A project can be reviewed once and changed for years afterwards, so a healthy record is a series of reviews rather than a single badge, and the gaps between them are where new code accumulates.

What a review does give you is evidence that someone qualified read the code with an adversarial eye and wrote down what they found. That is worth having, and it is a different thing from a promise about the future.

[Is the QRL Wallet Safe to Use?](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/is-qrl-wallet-safe-to-use.md) puts the reviews in the context of the risks a user actually faces, and [Is the QRL P2P Layer Quantum Safe?](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/is-qrl-p2p-layer-quantum-safe.md) covers the part of the protocol that is still being strengthened.

## Where the reports are

The project's security page lists the reviews and their dates, and that page is the place to start rather than a summary in a forum post.

If you want to go further, read the scope section of each report and compare it with what you care about: the signing code, the wallet file handling, the network layer. The answer to "was this audited" is usually "this part was, in this year, by this firm".

The date on a report is part of the finding. A 2018 report on a 2026 build describes history rather than the software you are running.

[How XMSS Signatures Work](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/how-qrl-xmss-signatures-work.md) covers the scheme the reviews examined, [QRL Wallet Source Code and Licence](https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/qrl-wallet-source-code-licence.md) covers the code being public in the first place, and [Is the QRL Project Still Active?](https://github.com/qrl-wallet/token-facts-and-prices/blob/main/is-the-qrl-project-still-active.md) covers the project's continued maintenance.

## FAQ

### Who has reviewed QRL?

Red4Sec and x41 D-Sec in 2018, and Halborn in March 2026, according to the project's security page.

### Does an audit mean the wallet is safe?

It means a stated scope was examined at a stated time. The code changed since, and your own download and backup habits matter as much as any review.

### What did the 2026 review cover?

The current post-quantum library. The project reports no cryptographic vulnerabilities found there, and the report itself is the document that states the scope.

### Are the reports public?

The security page lists the reviews and dates and is the place to check. Read the scope section before drawing conclusions from a summary.

<!-- answers: Q064, Q203 -->
