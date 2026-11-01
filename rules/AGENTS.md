# Rule: Automatic README Synchronization & Release Hygiene

## Directive
Whenever you modify, add, or refactor code, package dependencies, environment configurations, or project directory structures:
You **MUST** evaluate and update the relevant `README.md` file(s) using the bundled `readme-r` skill before concluding your task or presenting your final response.

When preparing to commit changes or bump releases, use the bundled `commiter` skill to enforce atomic staging, Conventional Commits, Semantic Versioning, and authenticated remote push validation.

---

## When to Trigger README Updates
Automatically invoke the `readme-r` workflow when any of the following occur during the conversation:
1. **New or Modified Functionality**: New features, updated API routes, CLI arguments, or changed component behaviors.
2. **Dependency & Environment Updates**: Added or removed packages in manifests (`package.json`, `pyproject.toml`, `Cargo.toml`, `go.mod`, etc.) or new configuration keys in `.env` / `.env.example`.
3. **Structural Changes**: New submodules, packages, or services created under directories such as `packages/`, `services/`, `apps/`, `skills/`, or `plugins/`.
4. **Bugfixes or Refactors with Behavioral Impact**: Any architectural change altering how developers run, test, build, or deploy the application.

---

## Execution Protocol
1. **Detect Changes**: Run `python3 skills/readme-r/scripts/detect_changes.py` (or the project/global resolved path) to identify modified files, dependencies, and target READMEs.
2. **Contextual Merge**:
   - For existing `README.md` files: Preserve all existing user branding, badges, tone, and untouched sections. Surgically update or insert sections for features, setup, configuration, and usage.
   - For new modules or projects without a README: Generate a comprehensive README using the standard template in `skills/readme-r/resources/standard_template.md`.
3. **Hierarchical Scope**: Update the root `README.md`. If a submodule or package was added or altered, update or create that submodule's local `README.md`.
4. **Pre-Commit Verification**: Ensure documentation changes are reviewed and staged either alongside the feature commit or as an atomic `docs:` commit.

