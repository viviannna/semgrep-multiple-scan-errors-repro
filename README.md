# Multiple Semgrep scan errors

Two independent Gradle subprojects intended to produce different Supply Chain
resolution errors in a single scan of this repository.

- `missing-requirement/`: has `build.gradle` but no `gradlew`, intended to trigger `MissingRequirement`.
- `resolution-command-failed/`: has an executable `gradlew` that prints an intentional failure and exits with status 1, intended to trigger `ResolutionCmdFailed`.

Neither subproject has a lockfile. There is deliberately no root Gradle build,
settings file, or wrapper, so the subprojects can be discovered independently.

## Run the reproduction

1. Add this repository to a Semgrep organization with Supply Chain enabled.
2. Enable dynamic dependency resolution.
3. Scan the repository root, including both subfolders.
4. Inspect the scan errors and subproject dependency-resolution details.

Expected: both error types in the same scan. Actual results depend on scanner
version and runner configuration; a hosted scan has not yet verified this fixture.
A runner that substitutes Gradle tooling may change the missing-requirement result.

## Fixture sources

- https://github.com/viviannna/missing-requirement-gradlew
- https://github.com/viviannna/semgrep-resolution-command-failed-repro

The Java source and build files are copied from these reproductions. The failing
wrapper is intentional and does not download or run Gradle.
