# Nigeria OSINT stack — what exists, what still works, what is missing

Added 2026-10-04 alongside this fork. Recorded so the state of the ecosystem is
not guessed at later.

## This repo: whoget

`L4ser-Security-Labs/whoget` — the only genuine open-source **OSINT tool for
Nigerian phone numbers** found on GitHub.

| Property | Value |
|---|---|
| Stars / forks | 21 / 9 |
| License | **GPL-3.0** — a real license, so forking and redistribution are permitted |
| Created / last push | 2020-06-15 / **2020-07-07** — no maintenance in roughly six years |
| Language | Python |
| Input | Nigerian numbers only; it requires the `+234` prefix |

### What it actually does

- **Carrier, geocode and timezone for a Nigerian number.** This still works and
  needs no key, because it comes from the offline `phonenumbers` library
  (libphonenumber). Useful detail: libphonenumber's carrier data is blank only
  for US/CA/PR numbers, so **for Nigerian numbers it is populated.**
- Google and DuckDuckGo search on the number, plus Twitter and Facebook lookups.
- `Contact name` was never implemented — it remains an unchecked item in the
  README. So the tool never did phone-to-name resolution, which is the
  capability that would have made it unlawful to use casually.

### What is dead, and why

The social features require API keys that no longer function:

- **Facebook**: it uses a *user access token* against the Graph API. That model
  was removed years ago. `facebook-sdk` is abandoned.
- **Twitter**: it uses v1.1 credentials through `tweepy`, on an API that is now
  restricted and paid.
- **`mechanize`** is in the requirements and is effectively unmaintained, so the
  scraping paths are fragile or broken.

**Net position: one feature of this tool survives unmaintained — the phone
metadata lookup — and it survives because a different, well-maintained library
does the actual work.**

### Licence obligation to remember

GPL-3.0 is **copyleft**. Any project built on or incorporating this code must
itself be released under GPL-3.0. That is fine for a free tool; it matters a
great deal if the intention is ever to make the result closed-source or
proprietary.

## The maintained replacements

Also forked alongside this one:

- **`phoneng`** — MIT, last pushed 2026-04-15 — zero-dependency TypeScript for
  parsing, validating, normalising and formatting Nigerian phone numbers. The
  modern replacement for whoget's input handling.
- **`ng-locations`** — MIT, last pushed 2026-09-11 — zero-dependency TypeScript
  for Nigerian states, LGAs, universities and airports, with tests.

Nigerian bank-account (NUBAN) validation exists, but only in stale form:
`Zifah/Nigeria-Bank-Account-NUBAN-Algorithm` (41 stars, last pushed 2019) and
`mojoblanco/NUBAN` (36 stars, Go, 2021). Both implement the CBN specification;
neither is maintained.

## The gap

The pieces exist, and **nobody has assembled them**:

- phone parsing and NG-range intelligence — maintained
- NUBAN structure and bank codes — stale
- states, LGAs, wards and polling units — maintained
- .ng domain and company-registry lookups — not bundled by anyone
- a single CLI or API that ties them together — **does not exist**

The nearest thing to a Nigeria OSINT tool is the repo you are reading, and it is
six years old with one working feature. That is the honest state of the field.

## Scope and law

Nigerian identifiers are legally restricted and are deliberately out of scope
here: the NIN, the BVN, telco subscriber records, and bank account-name
enquiry. These are not publicly queryable, and a private individual may not
obtain them. Any tool claiming to resolve an account number or line to a
person's name is either unlawful or lying. This note is legal information, not
legal advice.
