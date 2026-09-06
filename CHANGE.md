# CHANGE.md

## 2026-09-05 (Planned Before Edits)

We plan to update our project guidance to reflect the team decisions below before any additional implementation topics:

- We follow the 12 Factor Application principles.
- We apply Gang of Four design patterns where they improve clarity and maintainability.
- We use BDD (Gherkin) from unit testing through end-to-end testing.
- We follow Git Flow branching and avoid direct commits to main and develop.
- We prioritize elegant changes that are simple, easy to change, and DRY.
- We capture decisions and direction in LESSONS.md.
- We document all code and files in first person plural, as a journey junior contributors can follow, with an informal tone and light humor.

## 2026-09-05 (Completed)

- Added this file and recorded planned guidance updates before editing other project guidance files.
- Updated `.github/INSTRUCTIONS.md` with explicit rules for Git Flow, no direct commits to main/develop, 12 Factor alignment, GoF pattern usage, BDD expectations, and documentation style.
- Updated `.github/README.md` to match the same operating model for contributors and maintainers.
- Added `LESSONS.md` and seeded it with the current team baseline decisions.

## 2026-09-05 (Planned Before Edits - Wave 2)

We plan to add focused implementation guidance for the next topics:

- Create `.github/CODE_STYLE.md` with language-specific standards for Java, Python, Groovy, XML/YAML, and shell scripts.
- Create `.github/ARCHITECTURE.md` with 12 Factor alignment, GoF usage guidance, resilience patterns, and BDD traceability from behavior to tests.
- Update `.github/README.md` to include quick links to the new guidance files.

## 2026-09-05 (Completed - Wave 2)

- Added `.github/CODE_STYLE.md` with coding conventions, formatting rules, logging/error handling guidance, and BDD test style.
- Added `.github/ARCHITECTURE.md` with 12 Factor alignment, preferred GoF patterns, reliability/concurrency guidance, and BDD traceability expectations.
- Updated `.github/README.md` so contributors can quickly find and apply the new guidance.

## 2026-09-05 (Planned Before Edits - Wave 3)

We plan to add the next instruction topics:

- Create `.github/TESTING.md` covering BDD with Gherkin across unit, integration, and end-to-end testing.
- Create `.github/TOOLING_RECOMMENDATIONS.md` with lightweight linting, testing, and CI tooling that matches our stack.
- Update `.github/README.md` with quick links to these new guides.

## 2026-09-05 (Completed - Wave 3)

- Added `.github/TESTING.md` with BDD-first testing guidance from unit to end-to-end and reliability-focused validation expectations.
- Added `.github/TOOLING_RECOMMENDATIONS.md` with practical tooling recommendations for Java, Groovy, Python, shell, config, and CI quality gates.
- Updated `.github/README.md` to include discovery links and contributor usage guidance for the new files.

## 2026-09-05 (Planned Before Edits - Wave 4)

We plan to add deployment and security guidance:

- Create `.github/DEPLOYMENT.md` with Git Flow-aware release, promotion, and rollback guidance.
- Create `.github/SECURITY_GUIDELINES.md` with baseline security controls, review checkpoints, and dependency hygiene rules.
- Update `.github/README.md` with links to these new guides.

## 2026-09-05 (Completed - Wave 4)

- Added `.github/DEPLOYMENT.md` with branch-to-environment flow, release checks, validation gates, and rollback guidance.
- Added `.github/SECURITY_GUIDELINES.md` with secret handling, dependency hygiene, secure review checks, and security BDD scenario guidance.
- Updated `.github/README.md` to include quick access to deployment and security guidance.

## 2026-09-05 (Planned Before Edits - Wave 5)

We plan to add AI guidance and enforcement scaffolding:

- Create `.github/COPILOT_GUIDANCE.md` with tracked team guidance for AI-assisted development.
- Create local `.vscode/copilot-instructions.md` with repository-specific assistant instructions.
- Create `.github/ENFORCEMENT.md` and a lightweight workflow scaffold to verify policy files are present.
- Update `.github/README.md` to reference the new guidance.

## 2026-09-05 (Completed - Wave 5)

- Added `.github/COPILOT_GUIDANCE.md` with team-level guidance for AI-assisted coding and review.
- Updated local `.vscode/copilot-instructions.md` to align with 12 Factor, GoF, BDD, Git Flow, and junior-friendly documentation style.
- Added `.github/ENFORCEMENT.md` plus `.github/workflows/policy-checks.yml` for lightweight policy presence checks in CI.
- Updated `.github/README.md` to include the new Copilot and enforcement guidance links.

## 2026-09-05 (Planned Before Edits - Wave 6)

We plan to add a Vagrant + VirtualBox build path so we can build without WSL:

- Add a repository `Vagrantfile` with a Linux VM profile suitable for SyncWeave builds.
- Add provisioning and build helper scripts to install Java 21, Ant 1.10.17, and runtime dependencies.
- Add contributor documentation with Windows + VirtualBox setup steps and build commands.
- Ignore local `.vagrant/` runtime artifacts from version control.

## 2026-09-05 (Completed - Wave 6)

- Added `Vagrantfile` for a VirtualBox-backed Ubuntu build VM.
- Added `build/scripts/provision-vagrant.sh` to install Java 21, Ant 1.10.17, and required Linux packages.
- Added `build/scripts/build-in-vagrant.sh` to run `ant resolve rename_jars package` with repo-local environment.
- Added `docs/syncweave_vagrant_build_steps.md` with end-to-end setup and troubleshooting guidance.
- Updated `.gitignore` to exclude `.vagrant/` runtime files.

## 2026-09-05 (Planned Before Edits - Wave 7)

We plan to reduce build cycle time by adding segmented Ant entry points and usage guidance:

- Add aggregate build targets for connectors, functions, and parsers.
- Document a connectors-first iterative workflow for Vagrant builds.
- Document promotion steps from segmented builds to broader `JARS` and `package` verification.

## 2026-09-05 (Completed - Wave 7)

- Added `connectors-all`, `functions-all`, and `parsers-all` targets to `build.xml` for segmented build execution.
- Updated `docs/syncweave_vagrant_build_steps.md` with segmented build commands and recommended escalation flow (`component -> JARS -> package`).

## 2026-09-05 (Planned Before Edits - Wave 8)

We plan to harden OSGi dependency preparation so stale or partial jar artifacts do not poison later builds:

- Update OSGi dependency copy behavior to overwrite existing plugin `lib/*.jar` entries during each build.
- Validate that copied dependency jars are readable in the OSGi builder workspace.

## 2026-09-05 (Completed - Wave 8)

- Updated `osgi/build.xml` macro `copyPluginDeps` to use `overwrite="true"` so dependency jars are refreshed every run.
- This prevents stale or corrupted copies (for example `miserver.jar`) from being reused by PDE plugin compilation.

## 2026-09-05 (Planned Before Edits - Wave 9)

We plan to improve WebUI Dojo build stability in Linux VM package runs:

- Disable CSS optimization in the Dojo profile used by OSGi `setupWebUI`.
- Avoid path-resolution failures during CSS rewrite (`error(357)`) for legacy OneUI relative URLs.

## 2026-09-05 (Completed - Wave 9)

- Updated `osgi/plugins/com.ibm.di.ui.webui/tdi.profile.js` from `cssOptimize: "comments"` to `cssOptimize: "none"`.
- This avoids repeated CSS optimizer path errors in VM builds while preserving JS packaging and release output generation.
