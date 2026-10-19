> **Business:** Module Kinetic (operating brand: Module Kinetic Ltd.)
> **Owner:** Digital Currensy Inc. (all rights reserved)
> **Document:** Product page: Cabinetfield (check 3 of 7). Documentation only, no source code
> **Status:** DRAFT for founder review, not published
> **Date:** 2026-10-19

# Cabinetfield

## The question

**Was the cabinet measured?**

The electrical cabinet feeds a group of chargers. Cabinetfield checks that the cabinet was actually measured, not just assumed from its rating plate, and sets how much power it can safely carry right now.

## Who it's for

- **Asset and field engineering teams**, who need cabinet health based on evidence.
- **Utilities**, who need power limits that reflect the equipment's real condition.

## What it refuses

- A serious fault with no calibration for that cabinet.
- A calibration that had expired when the reading was taken.
- A calibration that belongs to a different cabinet.
- A reading with missing details.
- A rating-plate figure in place of a measurement.

## How it decides

The cabinet is read by a **quantum magnetic sensor**, a device that detects tiny changes in magnetic field. Each reading is compared with that cabinet's calibration.

1. **Is the reading complete?** Every required detail must be present.
2. **How serious is the fault?** A warning can go ahead without a calibration. A serious fault can't.
3. **Is the calibration valid?** It must be for the same cabinet and still in date.
4. **Set the power factor.** The result is a factor that shrinks the power the next check may use. The worse the reading, the lower the factor.

## Example outcome

These outcomes come from Module Kinetic's own test cases.

| Input, in words | Outcome |
|---|---|
| A warning-level reading on a cabinet, with no calibration | **Accepted.** A power factor is issued and saved once. |
| A serious reading on the same cabinet, with no calibration | **Refused** at *Was the cabinet measured?* (calibration required) |
| The serious reading, with a valid calibration for that cabinet | **Accepted.** A power factor is issued and linked to that calibration. |
| The serious reading, taken after the calibration expired | **Refused** at *Was the cabinet measured?* (calibration expired) |
| The serious reading, with a calibration from a different cabinet | **Refused** at *Was the cabinet measured?* (wrong cabinet) |

## What it isn't

- It doesn't decide which chargers are on. That's Unitcommit's job.
- It doesn't seal the record. That's Photonseal's job.
