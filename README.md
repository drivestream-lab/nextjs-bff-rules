# nextjs-bff-rules

**Open constitution for Next.js BFF portals** — shared Cursor agent rules (`.mdc`)
for App Router backends-for-frontend: server auth, route handlers, layout,
i18n, and spec-driven delivery.

Rules describe **how to code** the portal layer. They do **not** contain upstream
service catalogs, product route trees, or INIT requirements — those belong in
each consumer repo under `docs/specification/`.

| | |
|---|---|
| **License** | [MIT](LICENSE) |
| **Version** | see [`VERSION`](VERSION) (currently **0.1.6**) · [CHANGELOG](CHANGELOG.md) |
| **Mount path** | `.cursor/rules/` (git submodule) |
| **Scaffold** | `nextjs-bff-foundation` — optional cookiecutter in your org |

---

## Layout

This repository root **is** the contents of a consumer's `.cursor/rules/` directory:

```text
nextjs-bff-rules/
  VERSION
  README.md
  CHANGELOG.md
  code-guidelines-index.mdc    ← module index (start here)
  nextjs-app-router-stack.mdc
  nextjs-bff-server-auth.mdc
  nextjs-bff-route-handlers.mdc
  nextjs-repository-layout.mdc
  typescript-react-style.mdc
  tailwind-design-tokens.mdc
  client-forms-patterns.mdc
  workspace-page-layout.mdc
  no-hardcoded-strings.mdc
  shared-limits-pagination.mdc
  spec-driven-development.mdc
  testing-verify-flows.mdc
  documentation-project-guidance.mdc
  …
```

Full module table: [`code-guidelines-index.mdc`](code-guidelines-index.mdc).

---

## Adoption

From the **consumer portal repo root**:

```bash
rm -rf .cursor/rules

git submodule add https://github.com/<org>/nextjs-bff-rules.git .cursor/rules
cd .cursor/rules && git checkout v0.1.6 && cd ../..

git add .gitmodules .cursor/rules
git commit -m "Add Next.js BFF Cursor rules at .cursor/rules (v0.1.6)"
```

Cursor loads **`.cursor/rules/*.mdc`** automatically — no copy step.

Greenfield portals may start from `nextjs-bff-foundation` in your org
(`cookiecutter … --checkout v0.1.0`), then add the rules submodule as above.

---

## Tooling expected by the rules

`testing-verify-flows.mdc` and related modules define required quality gates:
**ESLint**, **Prettier**, **TypeScript**, **Vitest**, and Makefile targets
(`setup`, `check`, `test`). Exact config files live in the consumer repo or
scaffold — not in this constitution.

---

## Bump rules version

```bash
cd .cursor/rules
git fetch --tags
git checkout v0.1.6    # target version
cd ../..
git add .cursor/rules
git commit -m "Bump Next.js BFF rules to v0.1.6"
```

Read [CHANGELOG](CHANGELOG.md) before every bump. **Breaking** releases require
consumer code changes before or alongside the submodule pointer update.

---

## Governance

| Principle | Detail |
|-----------|--------|
| **Ownership** | Platform / architecture team owns this repo |
| **Consumers** | Pin a release tag — never fork or edit rules in product repos |
| **Changes** | Propose via PR here; consumers update the submodule pointer only |
| **Product truth** | Route maps, upstream contracts, branding → `docs/specification/` and `docs/project-guidance/` |
| **Do not** | `gitignore` `.cursor/rules` in consumers — breaks the pinned submodule |

---

## What stays in each portal repo

| Path | Purpose |
|------|---------|
| `docs/specification/product/` | Capabilities, route maps, INIT slices |
| `docs/specification/adr/` | Architecture decisions |
| `docs/specification/as-built/` | Live vs deferred; verification matrix |
| `docs/project-guidance/` | Portal UX, CRUD patterns, branding |
| `README.md`, `tests/README.md` | Setup, env vars, verify commands |

---

## Release process (maintainers)

1. Branch `rules/<short-description>` — edit `*.mdc` at repo root; peer review required
2. Bump **`VERSION`** (semver) and **`CHANGELOG.md`**
3. Update version in this README header
4. PR → `develop` → `main`; tag and push:

```bash
git tag v0.1.6
git push origin v0.1.6
```

---

## Related repositories

| Repo | Role |
|------|------|
| `nextjs-bff-foundation` | Cookiecutter scaffold for new BFF portals |
| `python-services-rules` | Constitution for Python APIs your BFF calls |

---

## License

MIT — see [LICENSE](LICENSE).
