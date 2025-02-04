# News

<div class="pagetoc" style="white-space:nowrap;">

<!-- toc -->
</div>

## This Week In Hledger 2023-11-10

It's time for This Week In Hledger!
Every Friday morning (or any time, tagged with "TWIH"), share your hledger/PTA user notes, 
dev news, achievements or experiences in the hledger matrix chat.

### sm
#### Dev

This week I completed the months-long yak shave that became Precisiongeddon, and it has landed in master;
see <https://github.com/simonmichael/hledger/pull/2111> for details.
Heads up: this can change default precisions shown especially by cost and value reports - 
all for the better hopefully, but any pre-release testing is welcome. 
There's a linux binary at <https://github.com/simonmichael/hledger/actions/runs/6804488282>.

CI (continuous integration) workflows on github have been optimised a bit:
- Scheduled weekly builds have been disabled, as they were propagating
  to forks and running wastefully there in some cases.
- Some repeated rebuilding of the hledger-lib and hledger packages
  that seems unnecessary has been stopped.
- hledger-ui no longer builds its modules twice.
- Haddock testing has been moved to the release workflows to save time.

Fixed:
- amounts in value reports can sometimes be shown unstyled / with zero decimal digits,
  <https://github.com/simonmichael/hledger/issues/2105>
- auto postings break redundant equity/cost detection and transaction balancing,
  <https://github.com/simonmichael/hledger/issues/2110>
  
My time log for the week shows 69% enhancement, 27% cleanup, 5% support.

#### Docs

As part of Precisiongeddon, I started expanding hledger's "code docs", in the Hledger module's haddock.
I spent time learning how to navigate Haddock and producing a fast-feedback authoring workflow (`make haddock-watch`).
And documented a bunch of "jargon" terms, and how we handle precision and display styles.

The "Regular expressions" manual section has been rewritten and now has examples:
<https://hledger.org/dev/hledger.html#regular-expressions>.

Unmentioned last week: I added a News page on hledger.org as a stable home
for This Week In Hledger and other news updates.

#### Misc

Some notable commits:
- feat: cli: Add tsv output (#869) (Peter Sagerson)
- feat: import: interpolate regex matches in field templates (#2009) (Jonathan Dowland)

There's new interest and design discussion for referencing the matched account name
in auto postings, and I have added to lukasbestle's $20 bounty to make it $100:
<https://github.com/simonmichael/hledger/issues/1975>

### Robert Nielsen

For more advanced hledger aficionados, here is a diagram showing just
about every possible part of an hledger transaction:
<https://hledgerfan.com/almost-everything-you-wanted-to-know-about-hledger-transactions>.

### Quotes of the week

*Overall very happy with hledger so far btw!*

*And thanks for the amazing tool. Migrating to hledger has been one of the most satisfying bits of digital homesteading I’ve done.*



## This Week In Hledger 2023-11-03

### sm
#### Dev
- tests: add outshine headings for folding/readability (in Emacs),
  readme updates, include .test files in TAGS, clean up ledger-compat tests
- tools: bake dbgstrs - print a bunch of hledger debug messages for review
- tools: ghci :rmain - like :main, but reloads first, useful eg when changing --debug level
- WIP: imp: prices: fixes, clarify/improve semantics
- WIP: precisiongeddon: precision/rounding cleanups/fixes/tests/docs, too intricate to describe

Continuing heavy work on consistent and optimal precision handling,
and all the related yaks which keep showing up.

#### Seen
- https://www.chvp.be/blog/nanoledger/ nice blog post introducing nanoledger android app

### Robert Nielsen

- Beginner's corner: What are the parts of a basic hledger transaction? Two resources for learners:
  https://hledgerfan.com/beginners-corner-a-basic-hledger-transaction


## This Week In Hledger 2023-10-27

### sm

#### Dev

- demo: avoid a bug in asciinema 2.3.0, and improve the error message when asciinema fails (#2094)
- web: fix broken "File format help" link in the edit form (#2103)
- web: access control UX cleanups: replace --capabilities and --capabilities-header with --allow, and validate it before starting the app (#834)
- web: refactor permission checking
- web: sandstorm web app cleanups; rename/reorder roles & permissions
- WIP: testing and improving amount style and precision handling in cost/value reports

#### Ops

- Set up a self-hosted Sandstorm server and learned how to configure it.
- Set up a public hledger-web instance in it: sandbox.hledger.org.
  Unlike <https://demo.hledger.org>, and until the spammers find it,
  sandbox is fully writable - use it as a pastebin for examples, eg.

#### Docs

- Contemplating: merging cookbook and examples/*; something more custom to replace mdbook

#### Examples

- hledger-report1: a custom compound report script, haskell and bash versions

#### Misc

- exploring latest Paisa, and how to use it with existing setups

#### Seen

- <https://www.reddit.com/r/plaintextaccounting/comments/17g0026/average_cost_capital_gains_with_hledger>
  very clear tutorial posts on (one way of) tracking investments

- *The primary reason Ledger was created was because it maintains the
  double-entry accounting equation for you: all accounts must
  balance. GUI tools never did this aggressively enough, all of them
  having some kind of feature like "check accounts" that would end up
  finding unaccountable pennies here or there.* --John Wiegley,
  <https://www.reddit.com/r/plaintextaccounting/comments/17fg4oi/why_plain_text_accounting_over_tools_like_excel/>


### chvp

- A new Android app, NanoLedger,  was added to F-droid to facilitate adding transactions on the fly. 
  Payees, notes and accounts can all be autocompleted. 
  Give it a try at <https://f-droid.org/en/packages/be.chvp.nanoledger/>


### Robert Nielsen

- Why I created the hledger fan YouTube channel:
  <https://hledgerfan.com/why-i-created-the-hledger-fan-youtube-channel>



## This Week In Hledger 2023-10-20

G'day @room. It's time for This Week In Hledger ! 
Every Friday morning, if you have any user or dev news or experiences you'd like to share, post them in the hledger matrix chat  (<https://matrix.to/#/#hledger:matrix.org>) as a message prefixed by "TWIH:". Markdown formatting and edits are welcome. On Saturday I'll publish on the hledger mail list and on mastodon.
  
### sm

Changes merged this week include:

#### Dev

- print: add --round option for more control of precisions (#2085)
- balance-assigned amounts affect commodity styles again (#2091, regression in 1.30)
- timedot: parse unitful quantities more accurately (#2096)
- Jacob Weisz has updated the hledger-web app on Sandstorm 
  (The amazing [https://sandstorm.io](https://sandstorm.io/) cloud app platform that lets you set up free private hledger-web instances with a few clicks, check it out!)

#### Ops

- renamed main CI workflow and branch to "ci"
- updated and committed hledger.org's caddy config and short urls (redirects)
- there's now an easy short url for trying out the hledger-web app on Sandstorm: <https://sandstorm.hledger.org>.

#### Docs

- moved regression bounty info to <https://hledger.org/REGRESSIONS.html>
- hledger manual > Journal > Commodity display style: rewritten
- hledger manual > aregister, hledger-ui manual > Register screen: note how separately-dated postings get combined

#### Examples
- justfile: forecast-import: show but don't consume future-dated forecast transactions

### Robert Nielsen

<https://hledgerfan.com/a-not-so-capital-idea-for-saving-time/> describes a timesaving tip for command line users. Specifically, when typing one of your account names, hledger "forgives" you if you don't match the capitalization of an account name.


## This Week In Hledger 2023-10-13

[hey there @room - I'd like to get a regular This Week In Hledger started, along the lines of This Week in Matrix (TWIM) ... Having a regular news heartbeat like this, even a small one, will help build our community and momentum.]

Welcome to This Week In Hledger ! Every Friday morning, if you have
any user or dev news or experiences you'd like to share, post them in
the hledger matrix chat room as a message prefixed by
"TWIH:". Markdown formatting welcome, edits welcome. On Saturday I'll
publish on the hledger mail list and on mastodon. (Inspired by This
Week In Matrix).

### sm

#### Merged

- [feat: balance: Add only-summary flag (#1012) #2086](https://github.com/simonmichael/hledger/pull/2086) (Stephen Morgan)
- [feat: CSV rule negation #2088](https://github.com/simonmichael/hledger/pull/2088) (bobobo1618)
- [imp: web: include account declaration info in accounts JSON #2097](https://github.com/simonmichael/hledger/pull/2097) (S. Zeid)

#### WIP

- more control of display precision with `print`
- more consistent precision handling in general
- displaying zeros with consistent commodity symbol, precision etc. when possible
- bug wrangling

#### Docs

- [How to record journal entries](https://hledger.org/how-to-record.html#how-to-record-journal-entries)
- [hledgermatic](https://hledger.org/hledgermatic.html#hledgermatic) , a simple up-to-date workflow
- Cleanups: Common workflows, Simon's old setup

### danielchappell

#### What I like about the data format
- Double Entry accounting in human readable files, the journal files.
- Balance assignments (to check in on my cash-wallet occasionally)
- Virtual transactions (to track funds)

#### What I like about HLedger specifically
- static analysis cf. [https://hledger.org/hledgermatic.html](https://hledger.org/hledgermatic.html)

#### What I need to do my homework on
- The limitations of balance assertions in HLedger
- study haskell

#### What makes me cry about HLedger
- A lack of amount expressions - github issue #183, [https://hledger.org/ledger.html?highlight=expression#amount-expressions](https://hledger.org/ledger.html?highlight=expression#amount-expressions)



<!--
Snippets

## TWIH

Schedule: Every Friday. Use each post  news as template for next.
Post to:
<https://hledger.org/news.html>
<https://mail.hledger.org>
<https://fosstodon.org/@simonmic> tags `#hledger #PlainTextAccounting`

Old template:

hledger news, posted most Fridays. Share content submissions in the #hledger chat.

### News
Recent developments.

### Tips
User tips, contributor tips.

### Jobs
Five ways you could help the project !
1. ...
2. ...
3. ...
4. ...
5. ...

### Quote of the week

-->
