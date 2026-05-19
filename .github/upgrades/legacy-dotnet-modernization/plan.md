# Modernization Plan (Automatic Mode)

## Goal
Create a safe, incremental path from legacy .NET Framework solution to modern .NET with repeatable builds and reduced technical risk.

## Phases
1. **Baseline & Build Stabilization**
   - Restore legacy packages reliably.
   - Enable build environment support for WebApplication targets.
   - Produce warning-free baseline in modified projects.

2. **Project System Modernization**
   - Convert non-SDK projects to SDK-style where feasible.
   - Move dependencies from `packages.config` to `PackageReference`.
   - Introduce central package management (optional phase if desired).

3. **Service & Client Modernization**
   - Replace/modernize WCF service hosting strategy.
   - Update WinForms service client integration (generated proxies/contracts).

4. **Validation Hardening**
   - Build in CI with deterministic restore.
   - Add/upgrade tests and run end-to-end validation.

## Success Criteria
- Solution builds in CLI/CI environment.
- No warnings in modified projects.
- Legacy dependency/hosting blockers removed or replaced.
