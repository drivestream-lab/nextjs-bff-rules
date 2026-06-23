# nextjs-bff-rules — bootstrap

Platform constitution for **DriveStream Next.js BFF portals**. Copy this tree into `autrio10x/nextjs-bff-rules`, tag **`v0.1.0`**, then register in `scripts/config/harness-autrio10x.yaml`.

**Consumers:** `drivestream-ops` (pilot), future Next.js BFF repos (`profile: frontend`).

**Boundary:** No upstream service names (Abhilekh, Parichay, …). Product-specific routes and trackers live in each app's `docs/specification/product/` and `AGENTS.md` appendix.

**Onboard:** [playbook/frontend-harness-onboarding.md](../../playbook/frontend-harness-onboarding.md)

## Files

| File | alwaysApply / globs |
|------|---------------------|
| `spec-driven-development.mdc` | always |
| `testing-verify-flows.mdc` | always |
| `nextjs-app-router-stack.mdc` | always |
| `nextjs-bff-server-auth.mdc` | always |
| `nextjs-repository-layout.mdc` | always |
| `nextjs-bff-route-handlers.mdc` | `app/api/**/*.ts` |
| `typescript-react-style.mdc` | always |
| `client-forms-patterns.mdc` | `components/**/*.tsx` |
| `tailwind-design-tokens.mdc` | `**/*.tsx` |
| `shared-limits-pagination.mdc` | always |
| `no-hardcoded-strings.mdc` | always |
| `workspace-page-layout.mdc` | always |
| `documentation-project-guidance.mdc` | always |

Mount at `.cursor/rules/` via harness `sync-harness`.
