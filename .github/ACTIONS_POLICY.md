# GitHub Actions Cost & Storage Policy

Use these defaults for every workflow added to this repository.

## Minutes
- Keep normal push CI lightweight: analyze, lint, unit tests, schema/syntax checks.
- Run heavy APK/AAB builds, Shorebird validation/publish, full release packaging, and similar expensive jobs only when they are actually required, preferably by manual dispatch or release-specific triggers.
- Scope push workflows with `paths` / `paths-ignore` when practical so docs or request-marker-only commits do not start full CI.
- Use `concurrency` with `cancel-in-progress: true` for superseded same-branch CI runs.
- Do not remove safety-critical tests just to save minutes.

## Artifact storage
- Do not upload whole build directories when a single APK/AAB/log/file is sufficient.
- Debug/diagnostic artifacts: normally 1 day.
- Temporary handoff artifacts: normally 1-3 days.
- Production AAB/APK handoff: normally up to 7 days.
- Obfuscation symbols and R8 mapping: normally up to 30 days when required for production diagnostics.
- Patch logs may be retained longer when they are tiny and operationally useful.
- Every new `actions/upload-artifact` step should set an explicit `retention-days`.

## Safety
Optimization must not change application behavior, signing, release identity, security checks, or production validation.
