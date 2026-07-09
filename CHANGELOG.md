# Changelog

All notable changes to `nextjs-bff-rules` are documented here.

Format: **Breaking** changes require code changes in consumer repos before or alongside the version bump. **Additive** changes are safe to adopt incrementally.

---

## v0.1.5

### Summary

Spec-tree parity with python-services-rules — folder-level as-built, no numbered product filenames in constitution, CI as requirements not scripts.

### Changes

- **`spec-driven-development.mdc`** — as-built row is `docs/specification/as-built/`; BFF pointers use `product/` folder not fixed filenames
- **`testing-verify-flows.mdc`** — feature map aligns with `as-built/`; CI states required gates, not `npm run` script block
- **`code-guidelines-index.mdc`**, **`nextjs-repository-layout.mdc`**, **`nextjs-bff-route-handlers.mdc`**, **`workspace-page-layout.mdc`**, **`no-hardcoded-strings.mdc`** — upstream/route/i18n pointers use `docs/specification/product/` not `00-` / `02-` filenames
- **`client-forms-patterns.mdc`** — add missing `description` frontmatter

### Migration guide

- Bump consumer submodule: `cd .cursor/rules && git fetch --tags && git checkout v0.1.5`
- No application code changes required

---

## v0.1.3

### Summary

Point harness sync documentation at the public launchpad CLI instead of a tenant-specific wrapper script.

### Changes

- **`code-guidelines-index.mdc`** — `launchpad sync-harness-app` + harness-pins link (replaces `drivestream-meta ./scripts/meta sync-harness`)

### Migration guide

- Bump consumer submodule: `cd .cursor/rules && git fetch --tags && git checkout v0.1.3`
- Update `.harness-pin.yaml` rules ref if pinned explicitly
- No application code changes required

---

## v0.1.2

### Summary

Remove prayog skill catalog from `spec-driven-development.mdc` — skills belong in `AGENTS.md` and prayog-skills, not constitution MDC. Add CI boundary check.

### Changes

- **`spec-driven-development.mdc`** — replace skill list with agent-workflows boundary pointer
- **`scripts/check_mdc_boundary.sh`** + **`.github/workflows/ci.yml`** — fail CI if MDC files enumerate slash-command skills

### Migration guide

- Bump consumer submodule: `cd .cursor/rules && git fetch --tags && git checkout v0.1.2`
- Update `.harness-pin.yaml` rules ref if pinned explicitly
- No application code changes required

---

## v0.1.1

### Summary

Packaging parity with `python-services-rules` and `data-platform-rules`: `VERSION`, `CHANGELOG`, consumer `README`, `.gitignore`, and `code-guidelines-index.mdc`. No MDC behaviour changes.

### Changes

#### Additive (new files)

- **`VERSION`** — semver SSOT (`0.1.1`)
- **`CHANGELOG.md`** — release history (this file)
- **`README.md`** — consumer-facing submodule guide (replaces bootstrap stub)
- **`.gitignore`** — repo housekeeping
- **`code-guidelines-index.mdc`** — index of all rule modules + product boundary

### Migration guide

- Bump consumer submodule: `cd .cursor/rules && git fetch --tags && git checkout v0.1.1`
- Update `.harness-pin.yaml` rules ref if pinned explicitly
- No application code changes required

---

## v0.1.0

### Summary

Initial release — DriveStream Next.js BFF portal constitution (13 MDC modules). Platform/stack patterns only; no upstream service names in rules.

### Changes

#### Additive (initial rules)

- **`spec-driven-development.mdc`** — truth hierarchy, same-PR discipline
- **`testing-verify-flows.mdc`** — Vitest vs live verify; no-overlap policy
- **`nextjs-app-router-stack.mdc`** — Next.js 15, React, TS, Tailwind, TanStack Query
- **`nextjs-bff-server-auth.mdc`** — httpOnly cookie, `authFetch`, no browser upstream
- **`nextjs-bff-route-handlers.mdc`** — BFF logging, error shaping, upstream fetch
- **`nextjs-repository-layout.mdc`** — BFF by `<upstream-service>`, UI by workflow
- **`typescript-react-style.mdc`** — strict TS, FC + hooks
- **`client-forms-patterns.mdc`** — forms + TanStack Query
- **`tailwind-design-tokens.mdc`** — CSS variables, design tokens
- **`shared-limits-pagination.mdc`** — `@/lib/constants` for limits
- **`no-hardcoded-strings.mdc`** — i18n via `@/lib/i18n`
- **`workspace-page-layout.mdc`** — `WorkspacePage` shell pattern
- **`documentation-project-guidance.mdc`** — `docs/project-guidance/` vs spec split

### Consumers

- [drivestream-ops](https://github.com/autrio10x/drivestream-ops) (`profile: frontend`)
