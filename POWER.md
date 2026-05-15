---
name: "aidlc"
displayName: "AI-DLC Workflow"
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

- **core-workflow** — The complete AI-DLC adaptive workflow rules including all phases, stages, and decision logic. Installed into your project's `.kiro/steering/` from the [aidlc-workflows release](https://github.com/awslabs/aidlc-workflows/releases/latest) (see Onboarding below). Once installed, Kiro auto-loads it as a steering file.

## Onboarding

### Prerequisites

- Kiro IDE or Kiro CLI installed

### Installation

1. Download the latest release from the [aidlc-workflows releases page](https://github.com/awslabs/aidlc-workflows/releases/latest)
2. Extract the zip — it contains an `aidlc-rules/` folder with:
   - `aws-aidlc-rules/` — core workflow rules
   - `aws-aidlc-rule-details/` — detailed rules referenced by the core workflow
3. Copy the rule details and the latest core workflow into your project. Run these commands from your project root:

**macOS / Linux (bash, zsh)**
```bash
mkdir -p .kiro/steering .kiro/aws-aidlc-rule-details
cp -R ~/Downloads/aidlc-rules/aws-aidlc-rule-details/. .kiro/aws-aidlc-rule-details/
cp -R ~/Downloads/aidlc-rules/aws-aidlc-rules/* .kiro/steering
```

**Windows (PowerShell)**
```powershell
New-Item -ItemType Directory -Force .kiro\steering, .kiro\aws-aidlc-rule-details | Out-Null
Copy-Item -Recurse $HOME\Downloads\aidlc-rules\aws-aidlc-rule-details\* .kiro\aws-aidlc-rule-details\
Copy-Item -Recurse $HOME\Downloads\aidlc-rules\aws-aidlc-rules\* .kiro\steering
```

**Windows (Command Prompt)**
```cmd
mkdir .kiro\steering 2>nul
mkdir .kiro\aws-aidlc-rule-details 2>nul
xcopy /E /I /Y "%USERPROFILE%\Downloads\aidlc-rules\aws-aidlc-rule-details" ".kiro\aws-aidlc-rule-details"
xcopy /E /I /Y "%USERPROFILE%\Downloads\aidlc-rules\aws-aidlc-rules" ".kiro\steering"
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

Confirm the files exists in .kiro folder. Once confirmed the core-workflow should be auto loaded /injected as a steering file in the KIRO chat context, validate it and start the AIDLC workflow.

## Usage

The workflow activates automatically and displays the welcome message and guides you through:

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

AI-DLC supports extensions under `aws-aidlc-rule-details/extensions/` for additional rules like:
- Security baselines
- Compliance (HIPAA, PCI-DSS, SOC2)
- Organization-specific policies

Extensions are automatically loaded and enforced when enabled during the Requirements Analysis phase. Each extension includes an applicability question so users can opt in or out per project.

### Adding Custom Extensions

1. Create a directory under `extensions/` (e.g., `extensions/compliance/hipaa/`)
2. Add markdown files with rules following the same structure as `security-baseline.md`
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


