> **Business:** Module Kinetic (operating brand: Module Kinetic Ltd.)
> **Owner:** Digital Currensy Inc. (all rights reserved)
> **Document:** Product page: Bayline (check 1 of 7). Documentation only, no source code
> **Status:** DRAFT for founder review, not published
> **Date:** 2026-10-19

# Bayline

## The question

**Was this a real fault?**

Bayline is the front door. It decides whether a message from a charging station describes a real, open fault. If it does, Bayline locks the charger out and opens one repair job.

## Who it's for

- **Charging operators**, who need real faults separated from routine status noise.
- **Field teams**, who need a repair job only when there's a real fault, and never before the charger is safely locked out.

## What it refuses

- The older one-word status message from the previous protocol version.
- A stream of routine readings presented as a fault.
- A fault that has already cleared.
- A routine status update, or a charger reporting that it's available.
- The same fault sent a second time.
- A repair job opened before the charger is locked out.
- A lockout requested for a fault Bayline has never seen.
- A message with no repair-job number.

## How it decides

Chargers report to their management system using **OCPP** (Open Charge Point Protocol), the common language between chargers and the software that runs them. That system forwards faults to Bayline. Bayline never connects to a charger directly.

1. **Is the message current?** Only the current protocol versions are accepted.
2. **Is it a fault?** Only open alerts and changes to a "faulted" state count.
3. **Is it new?** A repeat is refused.
4. **Is the charger locked out?** The lockout always comes first, then the repair job.
5. **Save once.** The repair job is saved once, and only its number passes to Loadclear.

## Example outcome

These outcomes come from Module Kinetic's own test cases.

| Input, in words | Outcome |
|---|---|
| A current-protocol alert that a connector has faulted, with a repair-job number | **Accepted.** Fault kept, charger locked out, one repair job opened. |
| The same alert sent twice | **Refused** at *Was this a real fault?* (duplicate) |
| A stream of routine readings | **Refused** at *Was this a real fault?* (a stream isn't a fault) |
| The older protocol's status message | **Refused** at *Was this a real fault?* (old protocol) |
| A repair job requested before the lockout | **Refused** at *Was this a real fault?* (lockout required first) |

## What it isn't

- It doesn't connect to or control chargers.
- It doesn't switch a charger back on. That's Loadclear's job.
