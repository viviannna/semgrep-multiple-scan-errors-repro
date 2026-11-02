# Multiple scan errors

Two Gradle projects for testing errors in one Semgrep Supply Chain scan:

- `missing-requirement/`: missing Gradle wrapper.
- `resolution-command-failed/`: Gradle wrapper intentionally exits with an error.

Scan the repository root with dynamic dependency resolution enabled.
