---
bc-version: [16..]
domain: interfaces
keywords: [interface, implements, enum, enumextension, setup, setup-id, guid, systemid, tablerelation, primary-key]
technologies: [al]
countries: [w1]
application-area: [all]
---

# Store the GUID of persisted interface setup on its owner

## Description

This rule applies when an enum-backed interface implementation persists per-record setup in a table whose primary key is a single `Guid` field, and a record in another table owns that setup. It checks how the setup identity is assigned and referenced; it does not require the setup table to have a GUID primary key.

## Best Practice

Store the setup primary-key value in a dedicated `Guid` field on the owning table, such as `"<Provider> Setup Guid"`. Reuse an existing field with the same purpose; the field name is not the deciding factor. Use a GUID assigned for the setup, not the owning record's `SystemId` or another owner identity. It is valid to generate the setup GUID in the owner field first and then assign it to the setup primary key, or to assign it to the setup first and then store it on the owner. Use the same stored value for lookup, editing, and deletion of that setup.

Do not apply this rule to setup with a non-GUID primary key, setups without an owner in another table, global singleton setup, or implementations without persisted setup. A `Guid` field on the owner or a `GetBySystemId` call does not establish that the setup itself has a GUID primary key. Do not require a particular interface name or add a new interface just to enforce this rule. If a fix affects an already published setup contract, preserve compatibility and call out any needed migration.

## Anti Pattern

The setup table has a GUID primary key, but creation assigns `Owner.SystemId` to that key or lookup uses `Setup.Get(Owner.SystemId)` instead of reading the dedicated owner field. Copying `Owner.SystemId` into a field named `"Provider Setup Guid"` still reuses the owner identity. Also report when an owner lacks a dedicated persisted setup reference or the code resolves a different identifier instead of the stored setup primary key. Base the finding on the setup key, the owning table, and the relevant assignment or lookup shown in the diff or surrounding code.
