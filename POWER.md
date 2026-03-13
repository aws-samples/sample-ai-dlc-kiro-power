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

- **core-workflow** (auto-included) — The complete AI-DLC adaptive workflow rules including all phases, stages, and decision logic. Automatically active when this power is installed.

## Onboarding

### Prerequisites

- Kiro IDE or Kiro CLI installed

### Installation

The core workflow steering file is included with this power and activates automatically — no manual setup needed for the workflow itself.

You only need to install the rule details files that the workflow references:

1. Download the latest release from the [aidlc-workflows releases page](https://github.com/awslabs/aidlc-workflows/releases/latest)
2. Extract the zip — it contains an `aidlc-rules/` folder with:
   - `aws-aidlc-rules/` — core workflow rules (already included in this power)
   - `aws-aidlc-rule-details/` — detailed rules referenced by the core workflow
3. Copy the rule details and the latest core workflow into your project:

```bash
# From your project root
cp -R ~/Downloads/aidlc-rules/aws-aidlc-rule-details .kiro/aws-aidlc-rule-details
cp -R ~/Downloads/aidlc-rules/aws-aidlc-rules/steering/* .kiro/steering/
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
│       └── core-workflow.md    ← updated from the latest release
```

### Verification

Open the steering files panel in Kiro IDE and confirm you see an entry for `core-workflow` under the AI-DLC power. It should show as auto-included.

## Usage

Start any development task by saying **"Using AI-DLC, ..."** followed by your intent. The workflow activates automatically and guides you through:

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

## Additional Resources

- [AI-DLC Method Definition Paper](https://prod.d13rzhkk8cj2z0.amplifyapp.com/)
- [AI-DLC Methodology Blog](https://aws.amazon.com/blogs/devops/ai-driven-development-life-cycle/)
- [AI-DLC Open-source Launch Blog](https://aws.amazon.com/blogs/devops/open-sourcing-adaptive-workflows-for-ai-driven-development-life-cycle-ai-dlc/)
- [AI-DLC Example Walkthrough Blog](https://aws.amazon.com/blogs/devops/building-with-ai-dlc-using-amazon-q-developer/)
- [GitHub Repository](https://github.com/awslabs/aidlc-workflows)
