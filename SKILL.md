---
name: verify-quality
description: |
  Aggregates existing reports from cmake-skill and cpp-lint into quality_reports/.
  Does NOT execute other skills. Uses .cmake-skill-manifest.json to discover report locations.
  Use when Claude needs to consolidate quality reports after running build and lint checks.
---

## Quality Gate Report

`verify-quality` discovers and aggregates reports from:
- cmake-skill: via `.cmake-skill-manifest.json` (written by cmake-skill)
- cpp-lint: from `cpp_lint_reports/`

```bash
verify-quality [project-root]
```

| Argument     | Default | Description       |
| ------------ | ------- | ----------------- |
| project-root | `.`     | Project directory |

## Workflow

1. Run cmake-skill: `cmake-skill pipeline --preset <preset>`
2. Run cpp-lint: `cpp-lint changed`
3. Aggregate: `verify-quality`

## Report Discovery

- **cmake-skill**: via `build/.agents/cmake-skill-manifest.json` (relative paths)
- **cpp-lint**: via `build/.agents/cpp-lint-manifest.json` (relative paths)
- **Fallback**: If manifest missing, searches `build/*/cmake_reports/` and `build/.agents/cpp_lint_reports/`

## Output

Reports are written to `build/.agents/quality_reports/`:
- `quality_gate_report.md` - Consolidated report
- `cmake_report.json` - CMake diagnostics (copied)
- `lint_report.json` - C++ lint diagnostics (copied)
