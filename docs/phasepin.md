> **Business:** Module Kinetic (operating brand: Module Kinetic Ltd.)
> **Owner:** Digital Currensy Inc. (all rights reserved)
> **Document:** Product page: Phasepin (check 5 of 7). Documentation only, no source code
> **Status:** Published (documentation showcase)
> **Date:** 2026-10-19

# Phasepin

![Phasepin — illustration, with yes and no cards that are real product output](../assets/phasepin.svg)

*Illustration: product art, not a photo of real equipment. Yes and no cards: real product output, same words as the run.*

## The question

**Is the clock good enough?**

Every energy record needs a time you can trust. Phasepin chooses which clock to believe and grades how good it is.

## Who it's for

- **Utility settlement teams**, who pay by time interval.
- **Auditors**, who need to prove when the energy was delivered.

## What it refuses

- GPS as the only time source. GPS can be jammed or faked, so it's only ever a second opinion.
- A clock whose error is too large.
- A missing or negative error figure from the operator.

## How it decides

Phasepin trusts time sources in a fixed order:

1. **A local atomic clock**, a small, very stable clock on site.
2. **Network time**, set by **PTP** (Precision Time Protocol), a standard for accurate time over a network, if its error is small enough.
3. **A short holdover**, when the atomic clock keeps time on its own for a limited period after losing its reference.
4. **GPS alone**, which isn't good enough to save.

It then grades the error that the network switch announces, measured against the **utility timing standards** that power substations use. A grade never changes which clock was chosen.

| Grade | Meaning |
|---|---|
| In profile spec | Meets the utility timing standard |
| Phasepin OK | Good enough for Module Kinetic, though not the full utility standard |
| Too wide | Refused by the later checks |
| Missing | No announced error supplied |

## Example outcome

These outcomes come from Module Kinetic's own test cases.

| Input, in words | Outcome |
|---|---|
| A healthy atomic clock, with a small announced error | **Accepted.** Source is the atomic clock, graded in profile spec. |
| No atomic clock, no network time and an expired holdover | **Refused** at *Is the clock good enough?* (GPS only) |
| An announced error far outside the standard | Graded too wide, then **refused** at the later checks |
| No error figure supplied by the operator | **Refused** at *Is the clock good enough?* (missing) |
| A negative error figure | **Refused** at *Is the clock good enough?* (invalid) |

## What it isn't

- It doesn't run the network time protocol itself. It reads the error the network has already measured.
- It doesn't check the data link. That's Fiberlock's job.
