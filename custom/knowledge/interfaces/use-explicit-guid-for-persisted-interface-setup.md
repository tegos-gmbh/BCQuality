---
bc-version: [16..]
domain: interfaces
keywords: [interface, implements, enum, enumextension, setup, setup-id, guid, systemid, tablerelation, primary-key]
technologies: [al]
countries: [w1]
application-area: [all]
---

# Use an explicit GUID for persisted interface setup

## Description

An interface implementation that stores configuration per owning record needs a stable link between that record and the implementation's setup. A dedicated setup identifier can be included explicitly when records are imported or copied.

## Best Practice

When a changed enum-backed interface implementation introduces persisted per-record setup, use an explicit `Guid` primary key on its setup table and a separate `Guid` setup reference on the owning record. Reuse an existing compatible setup identity instead of adding a duplicate. Review that setup reads resolve the same identifier stored by the owner.

Do not apply this rule to implementations without persisted setup, global singleton setup, or unrelated tables. Do not require a particular interface name or add a new interface just to enforce this rule. If the change extends an already published setup contract, preserve compatibility and call out any needed migration.

## Anti Pattern

New per-record interface setup relies solely on the implicit `SystemId`, uses a non-GUID primary key, or lacks a persisted owner-to-setup reference. Report only if the diff or surrounding code establishes that the setup is per record and durable.
