---
name: "aidlc"
displayName: "AI-DLC Workflow V1"
description: "AI-Driven Development Life Cycle - an adaptive three-phase workflow (Inception, Construction, Operations) that guides structured software development with requirements analysis, design, implementation, and quality assurance."
keywords: ["aidlc", "ai-dlc", "development lifecycle", "software development", "requirements", "design", "construction", "inception", "workflow", "sdlc"]
author: "Amit-Verma-AWS"
---

# AI-DLC (AI-Driven Development Life Cycle)

## Overview

AI-DLC is an intelligent software development workflow that adapts to your needs, maintains quality standards, and keeps you in control. It follows a structured three-phase approach:

- **Inception Phase** — Determines WHAT to build and WHY (requirements, user stories, design, risk assessment)
- **Construction Phase** — Determines HOW to build it (component design, code generation, testing, QA)
- **Operations Phase** — Deployment and monitoring (future expansion)

The workflow adapts to project complexity: simple changes stay efficient, complex changes get comprehensive treatment. For more about the AI-DLC methodology, see the [AWS Blog](https://aws.amazon.com/blogs/devops/ai-driven-development-life-cycle/) and the [Method Definition Paper](https://prod.d13rzhkk8cj2z0.amplifyapp.com/).

## Available Steering Files

- **core-workflow** — The complete AI-DLC adaptive workflow rules including all phases, stages, and decision logic. Installed into your project's `.kiro/steering/` from the [aidlc-workflows v1 branch](https://github.com/awslabs/aidlc-workflows/tree/v1) (see Onboarding below). Once installed, Kiro auto-loads it as a steering file.

## Onboarding

### Prerequisites

- Kiro IDE or Kiro CLI installed

> **Version scope:** This power packages the **v1** AI-DLC workflow (steering-file based).
> Upstream `main` and releases from v2.0.0 onward are a rewrite that installs via the native
> `aidlc` CLI (`aidlc config --harness kiro-ide`) and are **not** compatible with these
> instructions. Always use the v1 link below.

### Installation

1. Download the v1 branch archive: [v1.zip](https://github.com/awslabs/aidlc-workflows/archive/refs/heads/v1.zip)
2. Extract the zip — it creates an `aidlc-workflows-1/` folder containing `aidlc-rules/` with:
   - `aws-aidlc-rules/` — core workflow rules
   - `aws-aidlc-rule-details/` — detailed rules referenced by the core workflow
3. Copy the rule details and the latest core workflow into your project. Run these commands from your project root:

**macOS / Linux (bash, zsh)**
```bash
mkdir -p .kiro/steering .kiro/aws-aidlc-rule-details
cp -R ~/Downloads/aidlc-workflows-1/aidlc-rules/aws-aidlc-rule-details/. .kiro/aws-aidlc-rule-details/
cp -R ~/Downloads/aidlc-workflows-1/aidlc-rules/aws-aidlc-rules/* .kiro/steering
```

**Windows (PowerShell)**
```powershell
New-Item -ItemType Directory -Force .kiro\steering, .kiro\aws-aidlc-rule-details | Out-Null
Copy-Item -Recurse $HOME\Downloads\aidlc-workflows-1\aidlc-rules\aws-aidlc-rule-details\* .kiro\aws-aidlc-rule-details\
Copy-Item -Recurse $HOME\Downloads\aidlc-workflows-1\aidlc-rules\aws-aidlc-rules\* .kiro\steering
```

**Windows (Command Prompt)**
```cmd
mkdir .kiro\steering 2>nul
mkdir .kiro\aws-aidlc-rule-details 2>nul
xcopy /E /I /Y "%USERPROFILE%\Downloads\aidlc-workflows-1\aidlc-rules\aws-aidlc-rule-details" ".kiro\aws-aidlc-rule-details"
xcopy /E /I /Y "%USERPROFILE%\Downloads\aidlc-workflows-1\aidlc-rules\aws-aidlc-rules" ".kiro\steering"
```

Your project should look like:
```
<project-root>/
├── .kiro/
│   ├── aws-aidlc-rule-details/
│   │   ├── common/
│   │   ├── inception/
│   │   ├── construction/
│   │   ├── operations/
│   │   └── extensions/
│   └── steering/
│       └── core-workflow.md   
```

### Verification

Confirm the copy actually landed — the failure mode is empty directories, not an error message:

```bash
test -s .kiro/steering/core-workflow.md && echo "steering OK"
ls -d .kiro/aws-aidlc-rule-details/*/ | wc -l              # expect 5
find .kiro/aws-aidlc-rule-details -name '*.md' | wc -l     # expect 31
```

Expected: `core-workflow.md` non-empty, five subdirectories (`common`, `construction`,
`extensions`, `inception`, `operations`), and 31 rule files. Once confirmed, `core-workflow` is
auto-loaded as a steering file in the Kiro chat context and you can start the AI-DLC workflow.

## Usage

The workflow activates automatically and displays the entire welcome message VERBATIM to the user. Do not summarize, trim, paraphrase, or modify the ASCII diagram and guides you through:

1. Structured questions (written to files, not chat)
2. Execution plans showing which stages will run
3. Phased approvals — review and approve each stage
4. All artifacts generated in the `aidlc-docs/` directory

## Three-Phase Adaptive Workflow

### Inception Phase
Determines WHAT to build and WHY:
- Workspace Detection (always)
- Reverse Engineering (brownfield projects)
- Requirements Analysis (adaptive depth)
- User Stories (conditional)
- Workflow Planning (always)
- Application Design (conditional)
- Units Generation (conditional)

### Construction Phase
Determines HOW to build it:
- Per-Unit Loop: Functional Design → NFR Requirements → NFR Design → Infrastructure Design → Code Generation
- Build and Test (after all units complete)

### Operations Phase
Deployment and monitoring (placeholder for future expansion).

## Key Features

| Feature | Description |
|---------|-------------|
| Adaptive Intelligence | Only executes stages that add value to your specific request |
| Context-Aware | Analyzes existing codebase and complexity requirements |
| Risk-Based | Complex changes get comprehensive treatment, simple changes stay efficient |
| Question-Driven | Structured multiple-choice questions in files, not chat |
| Human in the Loop | Review execution plans and approve each phase |
| Extensible | Layer custom rules (security, compliance) on top of the core workflow |

## Extensions

AI-DLC v1 ships three extensions under `aws-aidlc-rule-details/extensions/`:

- `security/baseline/` — security baseline
- `resiliency/baseline/` — resiliency baseline
- `testing/property-based/` — property-based testing

Compliance packs (HIPAA, PCI-DSS, SOC2) and organization-specific policies are not included —
add them as custom extensions (below).

Extensions are automatically loaded and enforced when enabled during the Requirements Analysis phase. Each extension includes an applicability question so users can opt in or out per project.

### Adding Custom Extensions

1. Create a directory under `extensions/` (e.g., `extensions/compliance/hipaa/`)
2. Add two files, using `extensions/security/baseline/` as the reference:
   - `<name>.opt-in.md` — the opt-in prompt shown during Requirements Analysis
   - `<name>.md` — the rules themselves, loaded only after the user opts in

   Pairing is by naming convention: `<name>.opt-in.md` → `<name>.md`. Omitting the `.opt-in.md`
   file makes the extension unconditionally enforced with no way to decline.
3. Include an Applicability Question, Rule section, and Verification section
4. Rules are blocking by default — non-compliance prevents stage progression

## Troubleshooting

### Rules Not Loading
- Verify `.kiro/aws-aidlc-rule-details/` exists with subdirectories (common, inception, construction, operations, extensions)
- Use `/context show` in Kiro CLI to verify rules are loaded
- Start a new chat session after file changes

### File Encoding Issues
- Ensure all files are UTF-8 encoded

### Workflow Not Activating
- Start your message with "Using AI-DLC, ..." to trigger the workflow
- Verify the power is installed and the core-workflow steering file is active

## Best Practices

- Always review execution plans before approving
- Use the question files for structured input rather than free-form chat
- Commit AI-DLC artifacts (`aidlc-docs/`) to version control for traceability
- Layer security and compliance extensions for regulated projects
- For brownfield projects, let reverse engineering complete before requirements analysis



## License and support

This power is distributed under MIT-0 (MIT No Attribution).

- Repository: https://github.com/aws-samples/sample-ai-dlc-kiro-power

- Support / Issues: https://github.com/aws-samples/sample-ai-dlc-kiro-power/issues
