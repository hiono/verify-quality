---
name: verify-quality
description: |
  統合品質ゲート。cmake-skillとcpp-lintを実行し、
  結果をquality_reports/に集約する。
  Use when user needs unified quality check across CMake build and C++ code.
---

## Quality Gate

Run `verify-quality` to execute cmake-skill pipeline + cpp-lint and generate a consolidated report:

```bash
verify-quality [project-root] [preset] [scope]
```

| Argument     | Default         | Description       |
| ------------ | --------------- | ----------------- |
| project-root | `.`             | Project directory |
| preset       | `linux-release` | CMake preset      |
| scope        | `changed`       | cpp-lint scope    |

### Output

Reports are written to `quality_reports/`:
- `quality_gate_report.md` - Consolidated report
- `cmake_report.json` - CMake diagnostics
- `lint_report.json` - C++ lint diagnostics
