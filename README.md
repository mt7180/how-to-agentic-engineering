# Agentic Engineering

**Agentic engineering** is the shift from unstructured prompt-based coding (vibe coding) to disciplined, system-driven software development, where developers orchestrate autonomous AI agents using strict pipelines, context files, and automated quality gates.

This summary condenses the **emerging state of the art** workflow for production-grade software development.

## The Agentic Workflow

| # | Phase | Action | Goal |
|---|-------|--------|------|
| 1 | **Alignment** ("Grill-Me") | Interview the agent relentlessly before any code is written. | Expose blind spots and reach shared understanding (Matt Pocock's "grill-me" approach). |
| 2 | **PRD & Task Decomposition** | Turn the alignment chat into a PRD (problem, user stories, acceptance criteria) and split it into vertical implementation tickets. | Establish a source of truth and protect the agent from context overload. |
| 3 | **Implementation & TDD** | For each ticket: write a failing test from the acceptance criteria, confirm it fails, then implement until it's green + run linters, formatters, and type checkers automatically (hooks)| Prevent hallucination and drive correctness with tests. Catch mechanical issues before a human ever looks at it. |
| 4 | **Review & Merge** | Human-in-the-Loop | Retain full control over architecture and the final code review. |


## Agentic Engineering Resources

### General Concept & Learning Resources:
- https://github.com/EthicalML/awesome-agentic-engineering-resources
- https://agentfactory.panaversity.org/docs/agentic-engineering-crash-course
- https://github.com/fatihkc/awesome-agentic-engineering
- https://walkinglabs.github.io/learn-harness-engineering/

### Skills 
- (Matt Pokock): https://github.com/mattpocock/skills → (grill-me, to-prd, tdd, ...)
- (Kaparthy) https://github.com/karpathy/autoresearch → (autoresearch loop)

### Advanced Skills
- (Ken Chun Guid) https://github.com/kunchenguid/no-mistakes
- (Ken Chun Guid) https://github.com/kunchenguid/firstmate


### Top Strategies of the Experts

#### A. Spec-Driven Development & Context Engineering
Agents rarely fail on syntax — they fail from missing context.
- **AGENTS.md / CLAUDE.md as a Standard:** Every repository contains machine-readable markdown instructions that precisely explain to the agent which commands (build, test, lint) it is allowed to run, which directories are off-limits, and which coding style it must enforce.
- **[CONTEXT.md](https://github.com/mattpocock/skills/blob/6654f6b60cd9d5be8b54c6fafe44346dabeb3b76/README.md?plain=1#L94) as a Living Glossary:** A dedicated `CONTEXT.md` file acts as the single source of truth for domain concepts and terminology, preventing context drift across sessions without cluttering technical specs.
- **Micro-Specs before Code:** Instead of throwing a vague task at the agent in the chat, a 3-step process is enforced: Idea $\rightarrow$ Grill (challenging edge cases) $\rightarrow$ PRD (Product Requirements Document) / Ticket, and only then does implementation begin.

#### B. The Principle: "Treat AI as a Junior Engineer"
- Isolated Work: Never push directly to main. Agents operate strictly within isolated branches, opening draft PRs for human review.
- Automated Gates: Enforce automated CI/CD, linters, and test suites to catch subtle bugs or security blind spots before human inspection.
- Durable Artifacts: Avoid endless chat sessions that degrade into the "dumb zone." Use small, modular handoffs and clean diffs instead.

#### C. Day Shift / Night Shift Workflow
- **Day Shift (human-in-the-loop):** architecture, design, review, direction.
- **Night Shift (autonomous/sandbox):** well-defined refactors, test coverage, and bugfixes run overnight in an isolated container — diffs ready for review in the morning.
