# AI Agent Autonomous Problem-Solving Methodology

> Author: MO | License: CC BY 4.0

A reusable autonomous problem-solving workflow for AI Agents, fusing the best practices from 7 mainstream frameworks.

## Core Loop

**Observe → Think → Act → Observe Result → Reflect** — forming a closed loop.

## Methodology (9 Steps)

### 0. Define Success Criteria
Before starting, clarify: what conditions mean "done"? List verifiable criteria. Prevents infinite loops.

### 1. Search Past Experience
Before tackling a problem, search for related experience documents. Reuse known solutions, skip known failures.

### 2. Evaluate Approach
- Is the method correct? Does it fit the current environment?
- **Risk Assessment**: What side effects could this cause? (file overwrite, port conflicts, permission issues)
- Don't retry previously failed approaches

### 3. Write Process Document
Record: background, success criteria, environment, methods used, test results, next steps, iteration count (max 10 rounds).

### 4. Read-Write Loop
Read the document before each action to confirm direction. Update immediately after each step. **Use the document to correct yourself**, not short-term memory.

### 5. Failure Reflection
After each failure, analyze: why did it fail? Wrong method, wrong environment, or wrong execution? Distinguish "try a different method" from "same method, different parameters".

### 6. Never Repeat Mistakes
Failed methods recorded in the document must never be attempted again.

### 7. Quality Verification
After solving, self-check: Does it meet the success criteria? Any edge cases missed? Is the code/files clean?

### 8. Summarize and Crystallize
Document: what worked, what didn't, key pitfalls, reusable code snippets. For future reuse.

## Framework Sources

This methodology fuses the best from:
- **Chain of Thought** — Step-by-step reasoning
- **ReAct** — Observe → Think → Act loop
- **Reflexion** — Structured failure reflection and root cause analysis
- **Self-Refine** — Post-completion quality checking and iterative improvement
- **Plan-and-Solve** — Plan first, execute second, assess risks
- **AutoGPT** — Define success criteria, prevent infinite loops
- **Claude Computer Use** — File-driven autonomous operation patterns

## Use Cases

- AI Agent autonomous debugging and bug fixing
- Complex multi-step task automation
- Cross-session experience accumulation and knowledge reuse
- Any AI workflow that needs to "solve problems independently"

## License

[CC BY 4.0](https://creativecommons.org/licenses/by/4.0/legalcode) — Use freely with attribution.

---
*Author: MO | 2026*
