# verify-quality 🤖 [AI Agent Skill]

**Unified Quality Gate for CMake + C++ Projects.**

`verify-quality` aggregates reports from `cmake-skill` and `cpp-lint` into a consolidated quality report. It does **not** execute other skills—run them first, then use this to consolidate results.

## 🌟 Key Features

- **Report Aggregation**: Reads outputs from cmake-skill and cpp-lint
- **Manifest Discovery**: Uses `.cmake-skill-manifest.json` and `.cpp-lint-manifest.json` to locate reports
- **Consolidated Output**: All diagnostics merged into `quality_reports/quality_gate_report.md`

## 🔗 Dependency Diagram

```mermaid
graph TD
    subgraph Required Skills
        A[cmake-skill]
        B[cpp-lint]
    end

    A -->|manifest| A1[.cmake-skill-manifest.json]
    A -->|reports| A2[build/preset/cmake_reports/]

    B -->|manifest| B1[.cpp-lint-manifest.json]
    B -->|reports| B2[cpp_lint_reports/]

    C{verify-quality}

    A1 -.->|read| C
    A2 -.->|read| C
    B1 -.->|read| C
    B2 -.->|read| C

    C -->|writes| D[quality_reports/]

    style A fill:#4a90d9,stroke:#333,color:#fff
    style B fill:#d94a4a,stroke:#333,color:#fff
    style C fill:#50b85f,stroke:#333,color:#fff
    style D fill:#f5a623,stroke:#333,color:#fff

    E["⚠️ ALL 3 SKILLS REQUIRED"]
    style E fill:#ff6b6b,stroke:#333,color:#fff
```

**If cmake-skill or cpp-lint is missing:**
- verify-quality will report "No Report Data Found"
- quality_reports/ will be empty or incomplete

## 🛠 Installation

**All three skills must be installed to `~/.agents/skills/`:**

```bash
# Install all three skills (REQUIRED)
git clone https://github.com/hiono/cmake-skill ~/.agents/skills/cmake-skill
git clone https://github.com/hiono/cpp-lint ~/.agents/skills/cpp-lint
git clone https://github.com/hiono/verify-quality ~/.agents/skills/verify-quality
```

Installing only `verify-quality` without the other two skills will not work.

## 📖 Usage

```bash
# 1. Run cmake-skill first
cmake-skill pipeline --preset linux-release

# 2. Run cpp-lint next
cpp-lint changed

# 3. Aggregate results
./scripts/verify-quality .
```

## 📁 Output

Reports are written to `quality_reports/`:
- `quality_gate_report.md` - Consolidated report
- `cmake_report.json` - CMake diagnostics (copied)
- `lint_report.json` - C++ lint diagnostics (copied)

---

Maintained by **hiono**. Version **v0.1.2**.
