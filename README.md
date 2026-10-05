# Minimal reproduction: vulnerability fixes for dependencies a manager disables

## Current behavior

The gomod manager extracts `// indirect` modules with `enabled: false`.
`golang.org/x/text v0.3.0` has known vulnerabilities (for example GO-2020-0015), but Renovate skips it as `disabled`, so no vulnerability-fix PR is raised.

## Expected behavior

A dependency disabled by its manager still gets a vulnerability-fix PR.
A dependency disabled by the user with a package rule stays skipped.

Vulnerabilities come from OSV (`osvVulnerabilityAlerts: true`), so no GitHub Dependabot alerts are needed.

## Verified

Run with Renovate from source.

| Renovate | `golang.org/x/text` |
| --- | --- |
| `main` (e58cc8fa19) | `Dependency: golang.org/x/text, is disabled`, 0 updates |
| with the fix (0d0073f878) | `is disabled by default, but has a vulnerability alert`, [#1](../../pull/1) [SECURITY] |
