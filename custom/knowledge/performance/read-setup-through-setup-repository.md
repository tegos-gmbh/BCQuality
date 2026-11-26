---
bc-version: [all]
domain: performance
keywords: [setup, setup-repository, readfromcache, singleinstance, get, findfirst, findset, cache-invalidation]
technologies: [al]
countries: [w1]
application-area: [all]
---

# Read application setup through its setup repository

## Description

Tegos routes ordinary reads of application setup through the setup repository so callers share the same caching and invalidation behavior.

## Best Practice

Identify the setup table by its purpose and existing access pattern, not by its name alone. Use its established cached accessor from business code. If a changed setup repository introduces or changes cached data, check that modifications to the setup invalidate the affected cached values. Keep loading and invalidation inside the repository.

Do not require the cache when loading or refreshing it, editing setup, reading temporary settings, or when the read intentionally needs current transactional data. Do not prescribe a nonexistent cache API for a table outside the application's setup repository.

## Anti Pattern

A new call site bypasses an existing cached accessor by directly reading the same setup table with `Get` or `Find*`. Report the bypass at the new read. Also report a changed cache path that demonstrably retains stale setup after a supported modification.
