# claude-marketplace

Plugin marketplace for Claude Code.

## Plugins

### Spector

High-density functional spec generation from code. Three-layer pipeline:

1. **Scope discovery** — identifies modules, groups files, estimates scale
2. **Parallel capture** (Sonnet 4.5) — structured behavioral inventories per module
3. **Sequential compression** (Opus 4.6) — dense functional specs at 20:1–50:1 compression

#### Install

```bash
claude /plugins add-marketplace briankelley/claude-marketplace
claude /plugins install spector
```

#### Usage

```bash
# Spec a single file
/spector path/to/module.py

# Spec an entire directory
/spector src/

# Spec current working directory
/spector

# Custom output path
/spector src/ docs/my-spec.md
```

#### What You Get

Dense functional specifications where every token carries semantic load. Behavior-first, state-machine-oriented, zero filler. A 1000-line module compresses to 20–50 lines of spec.

See `spector/examples/config-page-iconography.md` for the gold-standard reference output.

#### Architecture

| Component | Model | Role |
|---|---|---|
| `/spector` skill | — | Orchestrator: scope discovery, dispatch, assembly |
| `spec-scanner` agent | Sonnet 4.5 | Broad capture: reads code, emits structured inventory |
| `spec-compressor` agent | Opus 4.6 | Precision compression: inventory → dense spec |

## License

MIT
