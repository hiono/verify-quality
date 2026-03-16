---
name: verify-quality
description: |
  Unified quality gate combining cmake-skill and cpp-lint.
  Executes build pipeline and C++ linting, consolidates results into quality_reports/.
  Use when Claude needs a single command to run full quality checks on CMake + C++ projects.
metadata:
  version: "0.1.0"
  agent: build
  models:
    - copilot/gpt-4.1
    - copilot/gpt-4o
    - opencode/big-picle
---

# Verify Quality

Run `verify-quality` to execute cmake-skill pipeline + cpp-lint and generate a consolidated report:

```bash
verify-quality [project-root] [preset] [scope]
```

| Argument     | Default         | Description       |
| ------------ | --------------- | ----------------- |
| project-root | `.`             | Project directory |
| preset       | `linux-release` | CMake preset      |
| scope        | `changed`       | cpp-lint scope    |

## Output

Reports are written to `quality_reports/`:
- `quality_gate_report.md` - Consolidated report
- `cmake_report.json` - CMake diagnostics
- `lint_report.json` - C++ lint diagnostics
