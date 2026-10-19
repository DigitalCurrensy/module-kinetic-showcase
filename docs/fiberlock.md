> **Business:** Module Kinetic (operating brand: Module Kinetic Ltd.)
> **Owner:** Digital Currensy Inc. (all rights reserved)
> **Document:** Product page: Fiberlock (check 6 of 7). Documentation only, no source code
> **Status:** DRAFT for founder review, not published
> **Date:** 2026-10-19

# Fiberlock

## The question

**Is the line clean enough?**

Control messages travel over a fibre link. Fiberlock checks that the link was clean and secure while it was used. Only then does it approve the path.

## Who it's for

- **Network and security teams**, who must show that control traffic wasn't interfered with.
- **Auditors**, who need evidence that the path behind each record was sound.

## What it refuses

- A line with too many errors. The session is stopped.
- A line with too much background noise, even when errors are low. The session is stopped.
- A security key that's too short.
- A GPS-only clock, or a clock graded too wide by Phasepin.
- A missing error reading.
- Saving a path it didn't approve.

## How it decides

The link is a **quantum-secured fibre link**. It uses quantum key distribution, a way of sharing a security key using light, where any eavesdropping shows up as errors on the line.

1. **Read the line's log.** Each entry records the error level, background noise and key size.
2. **Stop on noise.** Too many errors or too much noise stops the session at once, and the reason is recorded.
3. **Check the key and the clock.** The key must be long enough, and the clock must pass Phasepin.
4. **Approve and save once.** Photonseal won't seal a path Fiberlock didn't approve.

## Example outcome

These outcomes come from Module Kinetic's own test cases.

| Input, in words | Outcome |
|---|---|
| A quiet line, a full-length key and a trusted clock | **Accepted.** The path is approved and saved once. |
| A noisy line | **Refused** at *Is the line clean enough?* (session stopped) |
| Low errors but high background noise | **Refused** at *Is the line clean enough?* (excess noise) |
| A clean line with a GPS-only clock | **Refused** at *Is the line clean enough?* (untrusted clock) |
| A clean line with a clock graded too wide | **Refused** at *Is the line clean enough?* (clock too wide) |
| No error reading | **Refused** at *Is the line clean enough?* (missing) |

## What it isn't

- It isn't the clock. Phasepin is.
- It doesn't measure the cabinet or seal the record.
