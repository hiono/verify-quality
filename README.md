# verify-quality 🤖 [AI Agent Skill]

**Unified Quality Gate for CMake + C++ Projects.**

`verify-quality` combines `cmake-skill` and `cpp-lint` into a single quality gate, producing consolidated reports for autonomous AI agents.

## 🌟 Key Features

- **Unified Pipeline**: Runs cmake-skill (configure, build, test, lint, format) + cpp-lint (clang-format, clang-tidy)
- **Consolidated Reports**: All diagnostics merged into `quality_reports/quality_gate_report.md`
- **Simple Interface**: Single command replaces two separate skill invocations

## 🛠 Installation

Requires `cmake-skill` and `cpp-lint` to be installed.

```bash
git clone https://github.com/hiono/verify-quality ~/.agents/skills/verify-quality
```

## 📖 Usage

```bash
# Run full quality gate (default: linux-release preset, changed files only)
./scripts/verify-quality

# Custom preset and scope
./scripts/verify-quality . my-preset all
```

## 📁 Output

Reports are written to `quality_reports/`:
- `quality_gate_report.md` - Consolidated report
- `cmake_report.json` - CMake diagnostics
- `lint_report.json` - C++ lint diagnostics

---

Maintained by **hiono**.
