![QRL article banner](assets/banner-article.png)

# Is the QRL Wallet Safe to Use?

**Short answer.** It is safe in the ways software can be. The wallet is open source under the MIT licence, its code has been reviewed by external firms in 2018 and 2026, and it keeps keys on your own machine with no account on a server. The risks that remain are the ones a user brings: a fake download, a phishing page, and anyone who asks for your seed phrase.

## What "safe" can mean

The word hides three different questions, and they have different answers.

First: who holds the keys? A wallet that keeps them on a server can lose them without your involvement. A wallet that keeps them on your machine cannot.

Second: can you check the code? Open source means you can read what the software does with a key, or pay someone to read it.

Third: what happens when you make a mistake? A wallet can be emptied by one wrong download or one leaked phrase, and no design removes that.

QRL answers the first two well. The third is the part that depends on you.

The three questions also explain why comparisons are hard. A wallet that holds keys locally but asks you to download it from an advertisement is not obviously better than one that does neither, and the answer changes depending on which question you weight.

## The code and the audits

The wallet is published under the MIT licence, which means the source is available to read, build and reuse. Nothing about the key handling is hidden behind a binary you have to trust.

Its cryptography has been reviewed externally: Red4Sec and x41 D-Sec in 2018, and Halborn in March 2026, with the current post-quantum library in scope. Each review covers a stated scope at a stated time, which is what any audit can offer.

That combination, public code plus outside review, is the strongest form of assurance software usually gets. It is evidence rather than a promise: code written after a review has not been reviewed.

A review also has a scope, and the scope is what makes the finding meaningful. A report on the signing code is not a report on the interface, and reading the scope takes less time than reading the whole document.

## Where your keys live

Keys are generated on your device and stored in a wallet file you control, encrypted with a password you choose. There is no account, no sign-up and no server that holds a copy.

That has a direct consequence for support: nobody can reset your password or restore your access, because nobody has anything to restore it from. The mnemonic is the recovery path, and it is the only one.

It also means the wallet file is worth protecting like the keys it holds. A copy on a shared machine is a shared wallet.

## The download risk

A common way a self-custody wallet is emptied is not a flaw in the wallet. It is a different program installed under the same name.

Lookalike pages copy the design, the screenshots and the version text, and change only the file the button points at. An advertisement above a search result is one common delivery route.

The defence is a hash check: compare the hash of the file you downloaded with the value the project publishes for that file. https://github.com/qrl-wallet/wallet-setup-and-repair/blob/main/verify-the-qrl-installer.md walks through the commands, and it takes a minute.

A bookmark to the release page is worth more than a search result, because the address you saved cannot be quietly replaced by an advertisement. Keep the bookmark, and type the address by hand if you ever doubt it.

## The seed phrase rule

The phrase is the wallet. Anyone who reads it can rebuild the keys and spend the balance, and no legitimate process needs it.

No support channel asks for it, no moderator needs it to check a balance, and no giveaway requires it. A message that asks is an attack, whether it arrives by email, direct message or a comment on a post.

Store it offline, on paper, in two places, and test the restore while the balance is small. https://github.com/qrl-wallet/wallet-setup-and-repair/blob/main/back-up-a-qrl-seed-phrase.md covers the method.

## What to do if you think you were phished

Assume the phrase is compromised and act as though the wallet is already watched.

Create a new wallet on a machine you trust, or on a clean install, and move the balance to the new address. Do not reuse the old phrase, and do not restore the old wallet anywhere new.

Then work out what happened, because the answer decides what else is exposed: a fake installer, a phishing site that asked for the phrase, or a copy of the file taken from the machine.

Do not pay anyone who offers to recover the funds. A wallet that has been emptied cannot be refilled by a third party, and the offer is a second attempt to take money from the same person.

https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/qrl-security-audit-history.md covers the reviews, https://github.com/qrl-wallet/signatures-and-comparisons/blob/main/qrl-wallet-source-code-licence.md covers the licence in detail, and https://github.com/qrl-wallet/token-facts-and-prices/blob/main/avoid-qrl-price-prediction-scams.md covers the messages that arrive when a balance is public.

## FAQ

### Can the wallet be hacked?

Any software can have flaws, and no review covers code written after it. What the design removes is the server that could lose your keys for you.

### Is it safer than a web wallet?

For a balance you intend to hold, yes: the keys sit in a file you control rather than in a tab you loaded. The trade is that you are responsible for the file and the backup.

### Does anyone at QRL have my keys?

No. The keys are generated and stored on your device, and there is no account on a server to hold them.

### What single habit matters most?

Never type the seed phrase into anything except a wallet you are restoring, and verify the download before you run it.

<!-- answers: Q043, Q156, Q252 -->
