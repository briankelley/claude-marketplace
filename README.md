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

### Paranoid E2E Architect

Adversarial E2E test layer that hunts for unguarded destructive paths in web applications. Builds a registry of every state-mutating operation, fuzzes every permutation of empty/default/boundary input against pre-existing data, and enforces that no write path exists without a corresponding guard. Does not verify happy paths — other tests handle those.

#### Install

```bash
claude /plugins install paranoid-e2e-architect
```

#### Usage

```bash
# Launch against a project
/paranoid /path/to/project

# Or invoke the agent directly via Task tool
```

#### The Five Approaches

1. **Destructive Action Inventory** — crawls every page, catalogs every write trigger, cross-references against the Write Registry
2. **State Snapshot Diffing** — hashes files before/after write actions, flags any mutation from no-op submissions
3. **Adversarial Prompt Templates** — optional LLM-driven threat analysis of each page's interactive elements
4. **Permutation Fuzzing** — systematically tests every registry entry × 10 input strategies (empty, boundary, type confusion, etc.)
5. **Loss Annotation Policy Tests** — enforces that irreversible/unbackupable operations require confirmation

#### What You Get

A complete paranoid test suite: `paranoid_helpers.py` (registry + utilities), `test_paranoid_inventory.py`, `test_paranoid_snapshots.py`, `test_paranoid_fuzzing.py`, `test_paranoid_loss_annotations.py`, `test_paranoid_adversarial.py`, plus conftest fixtures with pre-seeded state.

See `paranoid-e2e-architect/references/dispatch-template.md` for the structured dispatch format.

## License

MIT
