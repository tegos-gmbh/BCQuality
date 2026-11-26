---
bc-version: [all]
domain: data-modeling
keywords: [entry-no, primary-key, number-sequence, getnextseqno, sequence, autoincrement, findlast, insert]
technologies: [al]
countries: [w1]
application-area: [all]
---

# Use a number sequence for new technical Entry No. primary keys

## Description

A technical entry identifier needs uniqueness but normally does not require gapless numbering. A number sequence supports concurrent inserts without deriving the next value from the table's last row.

## Best Practice

For a new persisted table with a technical `Entry No.` primary key, use the application's existing number-sequence helper or a Business Central number sequence for allocation. Preserve supplied entry numbers when the established insertion contract requires them. This rule does not apply to temporary tables, business document numbers, or identifiers that must be legally gapless; retain the numbering mechanism appropriate to those requirements.

## Anti Pattern

A new technical entry table uses `AutoIncrement` or derives its next key via `FindLast()` and an increment instead of allocating it from a number sequence. Do not request a primary-key or numbering migration on an unchanged, already published table solely to enforce this rule.
