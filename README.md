# nextjs-bff-rules

**Open constitution for Next.js BFF portals** — shared Cursor agent rules (`.mdc`) for App Router backends-for-frontend: server auth, route handlers, layout, i18n, and spec-driven delivery.

Rules describe **how to code** the portal layer. They do **not** contain upstream service catalogs, product route trees, or INIT requirements — those belong in each consumer repo under `docs/specification/`.

| | |
|---|---|
| **License** | [MIT](LICENSE) |
| **Version** | see [`VERSION`](VERSION) (currently **0.1.1**) · [CHANGELOG](CHANGELOG.md) |
| **Harness profile** | `frontend` |
| **Mount path** | `.cursor/rules/` (git submodule) |
| **Pairs with** | [launchpad](https://github.com/drivestream-lab/launchpad) · [prayog-skills](https://github.com/drivestream-lab/prayog-skills) |

---

## Role in the harness stack

```text
.harness-pin.yaml  (profile: frontend)
        │
        ├── rules  ──►  nextjs-bff-rules  →  .cursor/rules/*.mdc
        └── agent_skills  ──►  prayog-skills  →  .agents/skills/ (seeded)
```

[Launchpad](https://github.com/drivestream-lab/launchpad) `sync-harness-app` writes the pin, syncs this submodule, and seeds the frontend skill bundle. See [harness pins](https://github.com/drivestream-lab/launchpad/blob/main/playbook/harness-pins.md).

---

## Layout

This repository root **is** the contents of a consumer's `.cursor/rules/` directory:

```text
nextjs-bff-rules/
  VERSION
  README.md
  CHANGELOG.md
  code-guidelines-index.mdc
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
```

Full module table: [`code-guidelines-index.mdc`](code-guidelines-index.mdc).

---

## Adoption

### With Launchpad (recommended)

From your tenant meta workspace:

```bash
launchpad sync-harness-app --repo <portal-repo> --apply
launchpad verify-harness-app --repo <portal-repo>
```

Tenant harness config (`config/harness-<org>.yaml`) documents approved `rules.ref` + `agent_skills.ref` pairs.

### Manual submodule

From the **consumer portal repo root**:

```bash
rm -rf .cursor/rules

git submodule add https://github.com/drivestream-lab/nextjs-bff-rules.git .cursor/rules
cd .cursor/rules && git checkout v0.1.1 && cd ../..

git add .gitmodules .cursor/rules
git commit -m "Add Next.js BFF Cursor rules at .cursor/rules (v0.1.1)"
```

Add **`AGENTS.md`** at the consumer root — copy from your tenant `templates/AGENTS.frontend.md` or run harness sync.

---

## Bump rules version

```bash
cd .cursor/rules
git fetch --tags
git checkout v0.1.1    # target version
cd ../..
git add .cursor/rules .harness-pin.yaml
git commit -m "Bump Next.js BFF rules to v0.1.1"
```

Read [CHANGELOG](CHANGELOG.md) before every bump. Update `.harness-pin.yaml` `rules.ref` when using the harness pin record.

---

## Governance

| Principle | Detail |
|-----------|--------|
| **Ownership** | Platform team owns this repo |
| **Consumers** | Pin a release tag — never edit `.cursor/rules/` in product repos |
| **Changes** | Propose via PR here; consumers update the submodule pointer only |
| **Product truth** | Route maps, upstream contracts, branding → `docs/specification/` and `docs/project-guidance/` |

---

## What stays in each portal repo

| Path | Purpose |
|------|---------|
| `docs/specification/product/` | Capabilities, route maps, INIT slices |
| `docs/specification/adr/` | Architecture decisions |
| `docs/specification/as-built/` | Live vs deferred; verification matrix |
| `docs/project-guidance/` | Portal UX, CRUD patterns, branding |
| `AGENTS.md` | Agent router; playbook and verify commands |
| `tests/README.md` | Vitest vs live verify feature map |

---

## Release process (maintainers)

1. Branch `rules/<short-description>` — edit `*.mdc` at repo root
2. Bump **`VERSION`** (semver) and **`CHANGELOG.md`** (Breaking vs Additive + migration)
3. Update version in this README header
4. PR → `develop` → `main`; tag and push:

```bash
git tag v0.1.1
git push origin v0.1.1
```

5. Bump harness config in tenant `config/harness-<org>.yaml`; notify portal teams

---

## Reference profile

Typical consumer: a **management or operations portal** BFF (`profile: frontend`) that proxies authenticated calls to internal APIs. Your org's meta repo documents onboarding runbooks and approved harness pairs.

---

## Related repositories

| Repo | Role |
|------|------|
| [python-services-rules](https://github.com/drivestream-lab/python-services-rules) | Constitution for Python APIs your BFF calls |
| [prayog-skills](https://github.com/drivestream-lab/prayog-skills) | SDD agent workflows (`profiles/frontend.yaml`) |
| [launchpad](https://github.com/drivestream-lab/launchpad) | Factory CLI and harness sync |

> **Note:** `nextjs-bff-foundation` (cookiecutter scaffold for new portals) is planned; use harness sync + your portal skeleton until it ships.

---

## License

MIT — see [LICENSE](LICENSE).
