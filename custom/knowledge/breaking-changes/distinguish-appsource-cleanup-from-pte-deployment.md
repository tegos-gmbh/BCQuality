---
bc-version: [all]
domain: breaking-changes
keywords: [appsource, pte, obsolete, obsoletestate, obsoletetag, clean, preprocessorsymbols, migration, upgrade, breaking-change]
technologies: [al]
countries: [w1]
application-area: [all]
---

# Distinguish AppSource cleanup from PTE deployment

## Description

An incompatible change can break dependent apps or lose existing data regardless of how the app is distributed. Tegos uses a scheduled cleanup window for AppSource and assesses deployment and migration separately for per-tenant extensions (PTEs).

## Best Practice

Identify the distribution type from explicit repository or review context; do not infer PTE from an object ID range or the lack of an AppSource setting. If the type is unknown, describe the concrete compatibility or migration risk without imposing a distribution-specific procedure.

For AppSource, preserve the published contract during deprecation. For cleanup governed by a versioned `CLEAN<BC-major>` symbol, review both branches of the directive and ensure the removal path cannot activate before two BC major releases have elapsed. Apply the appropriate obsolete property or attribute for the AL element. When a persisted schema replacement requires moving data, verify that an upgrade path preserves that data.

For a confirmed PTE, do not report the lack of an AppSource-only `CLEAN` directive or deprecation window as a defect by itself. Still identify incompatible changes and missing data migration or dependent-app verification. Ask for deployment coordination when the change requires it; do not recommend force synchronization as a default remedy.

## Anti Pattern

An AppSource change activates versioned cleanup too early or removes a published contract without the applicable transition. A PTE change that risks losing data or breaking a dependent app is waved through because its deployment is tenant-specific. Report the concrete impact once rather than repeating a generic breaking-change finding.
