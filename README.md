# Safsata Bank — The Ledger of Arguments

A single-file, offline reasoning checker. It weighs an argument's **form** — telling a
valid argument (the conclusion is guaranteed by the premises) from one that only *looks*
valid — and records the verdict: **VALID** or **INVALID**.

**Live site:** https://edendia.github.io/safsata-bank/

---

## The lore

Before there were laws or scriptures, there were arguments. Within them, two kinds of
forms emerged: **Validators** — forms that hold — and **Sophists** — forms that only
seem to. A false form can wear the shape of a true one, and by the time you see the
difference, you may already have believed it. So the Bank was founded: every argument
enters the ledger, every form is weighed, and the Bank keeps the balance — of the
account, and perhaps of truth itself.

## What it actually does

Type an argument in plain English, one claim per line, ending with a "Therefore…"
conclusion. The Bank parses it and runs it through a fully deterministic logic engine —
no AI, no server, no guessing. If the form guarantees the conclusion, it's VALID;
otherwise it finds a counter-scenario and returns INVALID.

Under the hood it handles three tiers of logic:

- **Propositional** — if/then, and, or, not (truth tables).
- **Categorical** — All / No / Some, classic syllogisms.
- **Relational / first-order** — names, identities, and relations like "knows" or
  "admires", including quantifiers ("every", "some"), relative clauses, and passive
  voice, checked with a finite countermodel finder.

The engine is always the source of truth — it never bluffs a verdict. If it can't parse
a sentence into a form it can evaluate, it says so rather than guess.

## How it's built

Everything lives in one self-contained `index.html`: inline CSS and vanilla JavaScript,
no build step, no dependencies. Double-click it to run offline, or host it as a static
page (which is what GitHub Pages does here).

## Anonymous logging

The live site logs each submission — the argument text and its verdict, nothing
identifying — to a private Google Sheet, so I can see what arguments people try. This is
disclosed on the page itself ("Submissions are logged anonymously to improve the Bank").
The logging endpoint is set in `index.html` via the `LOG_ENDPOINT` constant; leaving it
empty turns logging off and keeps the app fully offline.

**Submissions sheet (private): https://docs.google.com/spreadsheets/d/1bTxhSfyUe9Gm3HG-FR8U1aF8hDsosT3N4-ldlPMR0PI/edit?usp=sharing** 

> This Sheet is set to **Restricted** — the link above grants no access on its own.
> It's here only as a reference for me.
