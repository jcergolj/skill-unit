# skill-test — Short Plan

## Goal

Build an open-source framework to test AI skills.

A skill is treated like software:
- `SKILL.md` = behavior definition
- `tests/` = acceptance tests
- `skill-test` = test runner

The goal is to answer:

> "Does this skill make the AI agent behave as expected?"

---

## 1. Skill structure

Each skill contains its own tests:


my-skill/
├── SKILL.md
├── tools/
└── tests/
├── scenarios.json
└── fixtures/


Example:

```json
{
  "id": "fix_bug",
  "prompt": "Fix the failing authentication test.",
  "assertions": [
    {
      "type": "command_executed",
      "contains": "test"
    },
    {
      "type": "tests_passed"
    }
  ]
}
2. Build CLI runner

Command:

skill-test ./skills/my-skill

Responsibilities:

Load skill
Load scenarios
Run agent
Capture execution trace
Execute assertions
Generate report
3. Keep agent-independent

Architecture:

skill-test
|
├── Core
|   ├── scenarios
|   ├── assertions
|   └── reports
|
└── Adapters
    ├── OpenCode
    ├── Codex
    ├── Claude
    └── Gemini
4. Capture agent behavior

Record:

commands executed
files changed
tools used
final response
test results

Example:

Agent trace:

✓ php artisan test
✓ changed User.php
✓ changed LoginTest.php
✓ tests passing
5. First assertions

Start simple:

command_executed
file_changed
file_not_changed
tests_passed
response_contains

Avoid complex AI judging initially.

6. First milestone

Support:

skill-test ./skills/laravel-debugging

Output:

Laravel Debugging Skill

✓ fixes failing tests
✓ does not delete tests
✓ verifies solution

3/3 scenarios passed
7. Future improvements
LLM-based quality evaluation
benchmark repository
CI integration
compare different AI agents
skill version regression testing

Use this file as reference: https://developers.openai.com/blog/eval-skills
