# Contributing to Analysis OS

## Branch model
| Branch | Purpose |
|---|---|
| `main` | stable, always usable as a Claude Code skill |
| `feature/<name>` | new domain packs, new templates, framework changes |

## Commit convention (Conventional Commits)
```
feat:     new domain pack, new template, new phase capability
fix:      correction to existing skill/domain content
docs:      README/docs-only changes
chore:     repo maintenance
```

## Adding a new domain pack
1. Create `domains/<domain>/<topic>.md` (or `domains/<domain>/index.md` for a lighter pack).
2. Follow the existing structure: Key objects / Key metrics / Common failure modes / Diagnostic approach.
3. Keep it **thin** — a domain pack supplies domain knowledge, it does not reimplement the Define→Model→Observe→Explain→Predict→Optimize pipeline. See `docs/best-practices.md`.
4. Add a one-line pointer to the new pack in `.claude/skills/analysis-os/SKILL.md`'s domain-detection table.
5. Optionally add a worked example to `examples/`.

## Adding a new template
Add to `templates/`, and reference it from the relevant phase file in `.claude/skills/analysis-os/` if it's meant to be used mid-pipeline rather than only at report time.

## Style
- Markdown only, no build step.
- Prefer concrete, checkable statements over generic advice ("check X via Y trace field" beats "investigate performance issues").
- Keep the Fact/Inference/Hypothesis/Unknown discipline visible in all example content, not just described abstractly.
