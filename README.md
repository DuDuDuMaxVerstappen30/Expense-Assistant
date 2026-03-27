# Expense Assistant

**English** | [中文](./README.zh-CN.md)

Expense Assistant is a local-first, chat-oriented reimbursement preparation tool designed to reduce the manual overhead of expense reporting.

> Status: `Planning`

## Overview

Expense reimbursement is often more painful than the expense itself. The real cost is not just paying for a ride, meal, or hotel. It is the repeated effort of collecting screenshots, renaming receipts, remembering context, classifying each item, and manually copying the final data into a corporate reimbursement system.

Expense Assistant is being designed to solve that preparation problem first.

In v1, the project focuses on turning chat-style inputs such as:

- short text notes
- voice messages
- screenshots
- receipt photos
- PDF invoices

into a structured reimbursement package that is easy to review and easy to copy into SAP or Concur manually.

The product goal is not "fully automated submission." The goal is to eliminate as much repetitive preparation work as possible while keeping the last step safe, transparent, and under the user's control.

## Why v1 Focuses on Preparation Instead of SAP Automation

Many enterprise expense systems, especially SAP-hosted or customized environments, are difficult to automate reliably. Even when browser automation is technically possible, it may still be the wrong default due to:

- unclear or unavailable APIs
- fragile UI workflows
- login and MFA complexity
- compliance and policy risk
- maintenance cost when internal screens change

For that reason, v1 intentionally stops one step earlier.

Instead of attempting brittle submission automation, Expense Assistant prepares a clean export bundle that the user can review and copy into SAP quickly. This keeps the workflow practical from day one without overpromising direct system integration.

## Core Workflow

The intended v1 workflow is:

1. Send a message to the assistant through a local web chat interface.
2. Upload or paste text, voice, screenshots, photos, or PDF receipts.
3. Let the assistant extract key reimbursement fields.
4. If any item is unclear, the assistant asks targeted follow-up questions in chat.
5. Review the resulting expense entries.
6. Export a reimbursement bundle for manual SAP submission.

The assistant is meant to feel like a lightweight personal reimbursement robot rather than a traditional form-based data entry tool.

## Product Principles

### Low Friction

The input experience should be as natural as sending a message. The user should not need to pre-sort files or fill complex forms before the assistant can help.

### Local First

The system should be useful on a personal machine before any cloud or enterprise integration exists. This reduces setup overhead and gives the user more control over sensitive receipts and reimbursement data.

### Chat First

The assistant should work through a conversation model instead of forcing users into rigid workflows. Missing information can be collected through short clarifying questions.

### Human in the Loop

The final reimbursement package should be transparent and reviewable. The system should organize, extract, and suggest, but not silently submit expenses into a corporate system.

## v1 Scope

Version 1 is planned to include:

- a local web chat UI for expense intake
- support for text, voice, image, screenshot, and PDF inputs
- speech-to-text for short voice notes
- OCR and receipt understanding for screenshots and invoices
- structured extraction of reimbursement fields, including:
  - date
  - merchant or vendor
  - amount
  - currency
  - category
  - payment method
  - trip or project context
  - free-form notes
- clarification prompts when confidence is low or key fields are missing
- session-level context, so the assistant can remember the current trip, project, or default assumptions during a conversation
- export generation in Markdown and CSV
- attachment indexing and normalized file naming

## Out of Scope for v1

The following are explicitly not part of the first release:

- direct SAP or Concur submission
- browser automation as a default workflow
- enterprise approval flows
- multi-user access control
- accounting system integration
- policy enforcement beyond basic structuring and flagging
- guaranteed support for unofficial personal WeChat automation

WeChat-like interaction is part of the product direction, but v1 is designed around a general chat interface so that future adapters can target WeChat, WeCom, Feishu, or other channels without changing the core reimbursement pipeline.

## Proposed Architecture

The initial architecture is planned around four layers:

### 1. Chat Intake Layer

A local web-based chat interface receives messages and attachments in a unified format.

### 2. Understanding Pipeline

This layer handles:

- speech transcription
- OCR
- receipt parsing
- field normalization
- confidence scoring
- duplicate detection

### 3. Session and Clarification Layer

This layer keeps short-lived context for an active reimbursement conversation and asks follow-up questions when the extracted data is incomplete or ambiguous.

### 4. Export and Archive Layer

This layer generates structured outputs and stores renamed attachments for downstream manual submission.

## Export Outputs

The planned v1 export bundle includes:

- `expenses.md`: a human-readable reimbursement summary
- `expenses.csv`: a structured table for copy, filtering, or future import workflows
- `attachments/index.csv`: an index of renamed attachments and their mapped expense items

The export is intentionally designed to make SAP entry easier, even if SAP remains a manual step.

## Planned Repository Direction

The repository does not contain implementation code yet. A likely future structure is:

```text
app/
  web/
  api/
core/
  ingestion/
  extraction/
  session/
  export/
data/
  attachments/
  exports/
docs/
```

This is a planning placeholder, not a committed implementation layout.

## Roadmap

### Milestone 1

Define product scope, interaction model, README, and implementation requirements.

### Milestone 2

Build the local chat intake flow and support basic file uploads.

### Milestone 3

Add transcription, OCR, and structured expense extraction.

### Milestone 4

Add clarification loops, attachment indexing, and export generation.

### Milestone 5

Evaluate channel adapters such as WeCom, Feishu, or other supported messaging platforms.

### Milestone 6

Only after v1 proves useful, evaluate whether SAP-facing automation is justified and compliant.

## Privacy and Compliance Notes

Expense data often contains personal, financial, and employer-related information. The project therefore starts with a local-first posture and avoids promising system automation that may conflict with company policy.

Any future integration with enterprise messaging tools or reimbursement systems should be evaluated against:

- company security requirements
- data retention expectations
- acceptable use policy
- authentication constraints
- auditability requirements

## Current Project Status

This repository is currently in the planning stage.

The next major step is to refine implementation requirements before code is written, including AI model choices, local storage design, attachment processing behavior, and channel adapter boundaries.

## License

This project is licensed under the terms of the [MIT License](./LICENSE).
