# nextjs-bff-rules

Shared **Cursor agent rules** (`.mdc`) for DriveStream **Next.js BFF portals**. Rules describe **how to code** (App Router, BFF auth, layout, i18n, SDD) — not product requirements or upstream service catalogs.

**Version:** see [`VERSION`](VERSION) (currently **0.1.1**) · [CHANGELOG](CHANGELOG.md)

---

## Layout

This repository root **is** the contents of a consumer's **`.cursor/rules/`** directory. Every `.mdc` file at the root is loaded by Cursor when the repo is mounted as a submodule:

```
nextjs-bff-rules/          # mounted as .cursor/rules/ in portal repos
  VERSION
  README.md
  CHANGELOG.md
  code-guidelines-index.mdc
  spec-driven-development.mdc
  testing-verify-flows.mdc
  nextjs-app-router-stack.mdc
  nextjs-bff-server-auth.mdc
  nextjs-bff-route-handlers.mdc
  nextjs-repository-layout.mdc
  typescript-react-style.mdc
  client-forms-patterns.mdc
  tailwind-design-tokens.mdc
  shared-limits-pagination.mdc
  no-hardcoded-strings.mdc
  workspace-page-layout.mdc
  documentation-project-guidance.mdc
```

---

## Consumer: first-time setup

Prefer the DriveStream factory when available:

```bash
# From drivestream-meta (consumer cloned adjacent to meta)
./scripts/meta sync-harness --repo drivestream-ops --apply
./scripts/meta verify-harness --repo drivestream-ops
```

### Manual submodule (without factory)

Run from the **consumer portal repo root** (e.g. `drivestream-ops/`):

```bash
rm -rf .cursor/rules

git submodule add https://github.com/autrio10x/nextjs-bff-rules.git .cursor/rules
cd .cursor/rules && git checkout v0.1.1 && cd ../..

git add .gitmodules .cursor/rules
git commit -m "Add shared Next.js BFF Cursor rules at .cursor/rules (v0.1.1)"
```

Add **`AGENTS.md`** at the consumer root — use drivestream-meta `templates/AGENTS.frontend.md` or run `sync-harness`.

---

## Consumer: bump rules version

```bash
cd .cursor/rules
git fetch --tags
git checkout v0.1.1    # replace with target version
cd ../..
git add .cursor/rules
git commit -m "Bump shared Cursor rules to v0.1.1"
```

**Before bumping**, read the [CHANGELOG](CHANGELOG.md). Breaking releases require consumer changes before or alongside the bump.

Update **`.harness-pin.yaml`** `rules.ref` when using the harness pin record.

---

## Release process (platform team)

1. Branch `rules/short-description` — edit `*.mdc` at repo root
2. Bump **`VERSION`** (semver) and add **`CHANGELOG.md`** section (Breaking vs Additive + migration)
3. Update version in this **README** header
4. Commit, tag, push:

```bash
git tag v0.1.1
git push origin main
git push origin v0.1.1
```

5. Bump harness config in [drivestream-meta](https://github.com/autrio10x/drivestream-meta) `scripts/config/harness-autrio10x.yaml` and notify consumer teams

---

## Governance

- **Platform team** owns this repo. Portal teams **do not** edit `.cursor/rules/` in product repos.
- Propose rule changes via PR here. Consumers only update the submodule pointer.
- **Product-specific** upstream maps, route trees, and INIT specs belong in **`docs/specification/product/`** — not here.

---

## What stays in each portal repo

| Location | Purpose |
|----------|---------|
| `docs/specification/product/` | Capabilities, `02-route-map.md`, INIT slices |
| `docs/specification/adr/` | Architecture decision records |
| `docs/specification/as-built/` | Live vs deferred; verification matrix |
| `docs/project-guidance/` | Portal UX, CRUD, branding |
| `AGENTS.md` | Agent router; playbook and verify commands |
| `tests/README.md` | Vitest vs live verify feature map |

---

## Rule index

See [`code-guidelines-index.mdc`](code-guidelines-index.mdc) for the full module table.

---

## Reference consumer

| Portal | Profile |
|--------|---------|
| [drivestream-ops](https://github.com/autrio10x/drivestream-ops) | `frontend` — management portal BFF |

Onboarding runbook: [drivestream-meta/playbook/frontend-harness-onboarding.md](https://github.com/autrio10x/drivestream-meta/blob/develop/playbook/frontend-harness-onboarding.md)
