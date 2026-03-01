---
description: Launch the paranoid E2E architect against a web application to build adversarial test layers
argument-hint: [project-path]
---

Use the paranoid-e2e-architect agent (via Task tool) to analyze the web application at `$1` and build adversarial E2E tests.

The agent should:

1. **Discover** the application — read routes, handlers, forms, frontend submission logic, and existing tests
2. **Build the Write Registry** — catalog every state-mutating endpoint with empty/valid payloads and loss annotations
3. **Produce test files** — inventory, snapshot diffing, permutation fuzzing, loss annotation policy, and adversarial analysis tests
4. **Verify** the tests run without import errors

If `$1` is not provided, ask which project to target.

Dispatch template for context: @${CLAUDE_PLUGIN_ROOT}/references/dispatch-template.md
