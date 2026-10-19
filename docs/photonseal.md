> **Business:** Module Kinetic (operating brand: Module Kinetic Ltd.)
> **Owner:** Digital Currensy Inc. (all rights reserved)
> **Document:** Product page: Photonseal (check 7 of 7). Documentation only, no source code
> **Status:** DRAFT for founder review, not published
> **Date:** 2026-10-19

# Photonseal

## The question

**Is the record sealed?**

Photonseal is the last step. It seals the final energy record so that any later change shows, and it only does so once every earlier check has passed.

## Who it's for

- **Billing and settlement teams**, who rely on the energy figure.
- **Utilities and auditors**, who need to check a record without trusting whoever sent it.

## What it refuses

- Sealing without a security key, or with a placeholder test key.
- Sealing a run that failed the power check.
- Sealing a path that Fiberlock didn't approve.
- Sealing with a clock graded too wide, or with GPS alone.

## How it decides

The record is protected by a **cryptographic seal**, a tamper-evident mark made with a secret key.

1. **Confirm every earlier check passed:** the power, the line and the clock.
2. **Seal the record.** The seal covers the meter, the repair job, the start time, the length, the energy and the clock source.
3. **Keep the key out of the record.** The key stays with the host system. It's never stored in the data.
4. **Save once.**

Anyone holding the key can check a seal. The right key confirms it. A wrong or empty key is rejected cleanly and never crashes the check.

## Example outcome

These outcomes come from Module Kinetic's own test cases.

| Input, in words | Outcome |
|---|---|
| A cleared run on an approved path, with a trusted clock and a configured key | **Accepted.** The record is sealed and saved once. |
| Checking that seal with the right key | Valid |
| Checking that seal with a wrong or empty key | Not valid |
| A cleared run whose clock was graded too wide | **Refused** at *Is the record sealed?* (clock too wide) |
| No key configured | **Refused** at *Is the record sealed?* (missing key) |
| A placeholder test key | **Refused** at *Is the record sealed?* (missing key) |

## What it isn't

- It isn't a coin, a token or a ledger entry.
- It doesn't check power, time or the line itself. It relies on the checks before it.
