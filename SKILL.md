     1|---
     2|name: autonomous-problem-solving
     3|description: "Resource-aware autonomous execution engine — text-driven memory loop + dynamic resource discovery + active research. Search before act when uncertain."
     4|version: "2.0"
     5|tags: [agent, autonomous, memory-loop, resource-aware, research-driven]
     6|author: "Hermes Agent / Nous Research"
     7|---
     8|
     9|## Core: Text-driven memory loop
    10|
    11|All tasks revolve around **documents**. Documents are memory, not decoration.
    12|
    13|```
    14|Search experience → Write PLAN → Execute → Update docs → Reflect → Sink
    15|  ↑                                                              ↓
    16|  └──────────── Auto-retrieve next time ←───────────────────────┘
    17|```
    18|
    19|## Step 0: Judge complexity
    20|
    21|Decide search depth before acting:
    22|
    23|- **Simple** (single file/command, clear direction) → Skip to Step 3
    24|- **Medium** (multi-file, clear but has dependencies) → Step 1 local + Step 2 skills
    25|- **Complex** (uncertain/multi-component/unseen) → Full flow: search → research → execute
    26|
    27|## Step 1: Search experience (local)
    28|
    29|```
    30|1. search_files("keywords", path="workspace/")   ← Experience base
    31|2. search_files("keywords", path="project_root")  ← Project source
    32|```
    33|
    34|Found experience → Read it, skip known failures, reuse success paths.
    35|
    36|## Step 2: Search resources (extended)
    37|
    38|For medium+ tasks, continue searching available resources:
    39|
    40|```
    41|3. skills_list() → match relevant skills → skill_view() to load
    42|4. Web search("problem keywords")                ← Web solutions
    43|5. GitHub API search related repos/code/issues   ← Open source reference
    44|```
    45|
    46|**Resource evaluation**: Not all useful. Rank by relevance, quality, cost. Pick Top N.
    47|
    48|**Not enough?** Change keywords, change channels. Don't guess, search.
    49|
    50|## Step 3: Write PLAN.md
    51|
    52|Required for every non-simple task. Five mandatory fields:
    53|
    54|```markdown
    55|# PLAN: [Task name]
    56|
    57|## Background
    58|What user wants, one sentence.
    59|
    60|## Success criteria
    61|What counts as "done". Verifiable conditions, list clearly.
    62|
    63|## Available resources
    64|- Experience: [from Step 1]
    65|- Skills: [from Step 2]
    66|- References: [from web/GitHub]
    67|
    68|## Method
    69|What technical approach, why this one.
    70|
    71|## Steps (with time tracking)
    72|1. [ ] Step 1 — Est: Xmin — Actual: __min
    73|2. [ ] Step 2 — Est: Xmin — Actual: __min
    74|3. [ ] Step 3 — Est: Xmin — Actual: __min
    75|   Total: __min est — __min actual
    76|
    77|## Iteration count
    78|Current round __ (max 10 rounds, then change direction)
    79|
    80|## Progress/feedback
    81|(Updated during execution)
    82|```
    83|
    84|## Step 4: Execute
    85|
    86|Default: execute immediately after PLAN. Only wait for user confirmation if user explicitly asks to review the plan first.
    87|
    88|Core: Use docs to correct yourself, not short-term memory.
    89|
    90|Each step follows:
    91|```
    92|Read PLAN for direction → ACT → VERIFY → Update PLAN progress
    93|```
    94|
    95|- Update PLAN.md progress immediately after each step
    96|- Long operations: report every minute — current step, what was done, result, next step
    97|- Verify failed → Record failure, go to Step 5
    98|
    99|## Step 5: Failure handling
   100|
   101|**Reflection (Reflexion)**: After failure, write clearly:
   102|
   103|- **Symptom**: Exact error message/output
   104|- **Root cause**: Wrong method? Wrong environment? Wrong execution?
   105|- **Distinguish**: Change method vs. same method, different params
   106|
   107|**Escalation (10-round grading)**:
   108|```
   109|Rounds 1-3:  Same method, tune params
   110|Rounds 4-6:  Completely different method
   111|Rounds 7-9:  Different stack/framework/tool
   112|Round 10:    Stop. Write experience doc. Report to user.
   113|```
   114|
   115|**Iron rule**: Failed methods recorded in docs must NEVER be retried. Catch yourself reusing one → stop immediately.
   116|
   117|## Step 6: Verification gate
   118|
   119|**Iron rule: No evidence, no claim of completion.**
   120|
   121|Self-check before claiming done:
   122|1. What command/operation proves success?
   123|2. Did I run it? See full output?
   124|3. Does output actually prove success? (Not "should work")
   125|
   126|Verification types:
   127|- Code: Run command + check output + exit code
   128|- File: stat + read back content
   129|- Network: fetch URL + check status code
   130|- Process: Check alive + must kill after test
   131|- External: Must verify side effects (HTTP status, file exists)
   132|
   133|Report with evidence (command output/file content/status code). Never say "it should work".
   134|
   135|Banned words: probably, should work, might work, maybe
   136|
   137|## Step 7: Experience sink
   138|
   139|After task ends, write to `notes/YYYY-MM-DD-keywords.md`:
   140|
   141|```markdown
   142|## Summary
   143|- What worked
   144|- What didn't (+ root cause)
   145|- Key pitfalls
   146|- Reusable code/command templates
   147|- New resources discovered
   148|```
   149|
   150|For complex tasks that succeeded, consider saving as skill.
   151|
   152|## Tool mapping
   153|
   154|| Step | Tool | Purpose |
   155||------|------|---------|
   156|| Search experience | `search_files` | Search local experience base and project source |
   157|| Search skills | `skills_list` / `skill_view` | Discover and load skills |
   158|| Search web | `web_search` | Search web solutions |
   159|| Search code | GitHub API | Search open source references |
   160|| Write PLAN | `write_file` | Create process document |
   161|| Update PLAN | `patch` | Incremental doc updates |
   162|| Execute | `terminal` / `execute_code` | Run commands and scripts |
   163|| Task tracking | `todo` | Checklist tracking |
   164|| Parallel | `delegate_task` | Multiple independent subtasks |
   165|| Sink | `write_file` / `skill_manage` | Save experience / create skill |
   166|