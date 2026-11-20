![QRL article banner](assets/banner-article.png)

# What Reddit Says About QRL

**Short answer.** Community threads are useful for one thing: learning which failures people actually hit. They are unreliable for facts about supply, security or price, because a comment is not a source and a confident answer is not evidence. Treat every claim as a lead and check it against the repository, the release page or a block explorer.

## What the threads get right

The value of a forum is the failure report. Someone who cannot get a wallet to sync, or who sees a pending transfer that never confirms, is describing something that happened to them, and the replies often name a cause the documentation covers.

Those reports are worth reading as a list of symptoms. They tell you which pages matter, and they occasionally reveal a problem the project has not documented. A repeated report of the same failure at the same version is a signal.

The corollary is that a thread's value decays. A report about an older build may describe a defect that has since been fixed, and a reader who acts on it will chase a problem the current release does not have.

What they are not is a diagnosis. The same symptom has several causes, and a reply that fixed one person's machine may have nothing to do with yours.

## Recurring myths

Three confusions come up often enough to be worth naming.

The first is the theory that QRL is connected to a proposed global financial reset. It is not: QRL is an independent open-source blockchain, and the resemblance between the acronym and the theory's name is a coincidence that has been repeated into a rumour. https://github.com/qrl-wallet/token-facts-and-prices/blob/main/is-qrl-connected-to-the-qfs-theory.md treats it in full.

The second is the claim that the project has stopped work. It has not. Releases are published, the repository shows activity, and the wallet's current build is newer than most of the threads asserting otherwise. https://github.com/qrl-wallet/token-facts-and-prices/blob/main/is-the-qrl-project-still-active.md covers the evidence.

The third is the one-time key limit, usually stated as "the wallet only works 1,024 times". That is close to true and misses the important part: the limit belongs to an address, not to the wallet, and receiving does not consume a key. https://github.com/qrl-wallet/wallet-setup-and-repair/blob/main/how-many-qrl-ots-keys-remain.md explains the count, and https://github.com/qrl-wallet/wallet-setup-and-repair/blob/main/move-qrl-before-keys-run-out.md covers what to do as it runs out.

## The questions that come up most

Supply is asked constantly, usually with a number attached that nobody can source. The chain has a fixed maximum and a documented total in circulation; a comment that disputes either without linking anything is not a finding.

Price is asked more than anything else, and no forum has ever answered it. A thread predicting a price is a thread about the poster's position, not about the asset. The same applies to charts: a screenshot of a candle is not data about the asset.

Recovery is the third. Someone has lost a phrase, or a file, and asks whether the coins can be recovered. The answer is the same every time: without the phrase or the file, nobody can help, and anyone offering to is a thief. https://github.com/qrl-wallet/token-facts-and-prices/blob/main/qrl-token-supply-explained.md covers supply properly, and https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/is-qrl-wallet-safe-to-use.md covers the recovery boundary.

## How to check a claim

Four habits settle most of it. Find the primary document: a specification, a release page, or the code. Check the date, because a thread from three years ago describes software that has changed. Check whether the claim is about the chain or about a person's opinion. And check whether the person making it has any way to know.

A block explorer answers questions about transactions and balances directly. The release page answers questions about what ships. The repository's issue tracker answers questions about known defects. Between those three, most forum claims can be confirmed or dropped in a minute.

It also helps to separate what a comment asserts from what it assumes. Two people can agree on a symptom and disagree on the cause, and only the first of those is evidence.

What none of that requires is trusting the person who told you. That is the point: the sources are public, and a claim that cannot be checked against them is a claim to set aside rather than repeat.

## Where the primary sources are

The wallet's repository holds the code, the releases and the issue tracker. The project's documentation covers the wallet's behaviour, including the send form's fields and the key index. The explorer shows what the chain recorded.

Those three are enough to check almost anything a thread asserts about QRL. When they disagree with a comment, they win, and when a comment has no source at all, it is not evidence in either direction. None of them requires an account, which means a reader can check a claim without joining the conversation about it.

## FAQ

### Is Reddit a reliable source on QRL?

For failure reports, sometimes. For supply, security or price, no. A comment is a lead, and the check is against a primary source.

### Does the project run a subreddit?

There is a community forum, and this page does not vouch for any particular one. Treat any forum as a place where people talk, not as an authority on the software.

### Someone on a forum offered to recover my wallet. Should I reply?

No. Nobody can recover a wallet without the phrase or the file, and anyone who offers to is attempting a theft.

### Why do people say the project stopped?

Because releases are infrequent compared with projects that ship weekly, and an observer without the repository in front of them reads quiet as inactivity. The release history is the answer.

<!-- answers: none -->
