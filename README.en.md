# Claude Code Harness & Plugin Guide

A curated, hands-on catalog of **harnesses, plugins, and extensions** for Claude Code (and compatible coding agents). Each entry follows one consistent template: *what it is → how to install → how to trigger it (commands + concrete prompt examples) → caveats*.

> Primary docs are written in Korean. This is an English summary. See [README.md](README.md).

## Why this repo

Most lists of these tools are just link dumps. But in practice **they are not the same kind of thing.** Some ship a whole config pack, some enforce a development methodology, some are features already built into the agent. This repo first classifies tools by **layer (category)**, then documents each one down to copy-pasteable install and trigger steps.

## Categories (layers)

| Layer | What it is | Examples |
|---|---|---|
| **A. Harness pack** | Drops a full set of agents/skills/hooks/commands into `.claude/` | gstack, ECC, revfactory/harness |
| **B. Methodology** | Enforces one development process (spec → plan → implement) | spec-kit |
| **C. Discipline** | A layer that forces the agent to use skills/procedures first | **superpowers** |
| **D. Native** | Built into the agent, no install required | ultracode |

## Catalog

| Harness | Category | Install | Status | One-liner |
|---|---|---|---|---|
| [superpowers](harnesses/superpowers.md) | C. Discipline | Easy (plugin) | ✅ used | Forces skill-first workflow + 14 dev skills |

> 📌 **Planned**: gstack · spec-kit · ECC · revfactory/harness · ultracode.

## Contributing

Copy [TEMPLATE.md](TEMPLATE.md) to `harnesses/<name>.md` and fill it in. See [CONTRIBUTING.md](CONTRIBUTING.md).

## License

[MIT](LICENSE) © 2026 Kim Yoohyun (uuuhyun)
