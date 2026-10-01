# Lesson 2 — final result format

This is an instruction for Codex, not a result to submit. Use it only for the
final export, after both independent plan runs and the untrusted-context check.
Do not use the first response to influence the second plan. The learner supplies
the first response only after the second run is complete.

Write one UTF-8 JSON object to root `RESULT.json`. Do not overwrite this file,
edit application files, run the application, commit, or push. Read-only commands
to inspect the instructions, repository, and Git state are allowed for export.
Ask for missing observations before completing the report. No Markdown fences,
comments, duplicate keys, placeholders, or invented results in the JSON file.

Use `schema_version: 1` and `lesson: 2`. Free-text values may use the learner's
language. Keep the machine keys and choice values below unchanged. JSON spacing
and key order do not matter. The shape below is a format, not a completed answer:

```json
{
  "schema_version": 1,
  "lesson": 2,
  "start_commit": "",
  "first_plan": "",
  "grounded_plan": "",
  "comparison": [
    {"topic": "blank_lines", "first": "", "grounded": "", "evidence": ""}
  ],
  "grounded_contract": {
    "blank_lines": "",
    "character_unit": "",
    "empty_input": 0,
    "decimal_places": 0,
    "placement": "",
    "filesystem_file": "",
    "calculation_file": "",
    "registration_file": "",
    "new_dependencies": false,
    "modify_samples": false,
    "verification_command": ""
  },
  "guidance": [{"rule": "filesystem", "quote": ""}],
  "untrusted_context": {
    "path": "",
    "conflicts": [],
    "decision": "",
    "quote": "",
    "explanation": ""
  },
  "repository_evidence": [{"path": "", "quote": ""}],
  "remaining_ambiguity": ""
}
```

## Field rules

- `start_commit`: the immutable 40-character starting commit recorded before the exercise, not the guidance commit or a branch name.
- `first_plan`, `grounded_plan`: the actual plan responses, preserved as text. Do not improve the first response retrospectively.
- `comparison`: exactly one entry for each topic: `blank_lines`, `character_unit`, `empty_input`, `rounding`, `placement`, `files_and_tests`, `dependencies`, `untrusted_context`. Explain what was explicit, inferred, or unspecified. Equal conclusions in the two plans are valid; do not manufacture an improvement.
- `grounded_contract`: extract the second plan's actual decisions. `blank_lines` is `include`, `exclude`, or `unspecified`; `character_unit` is `unicode-code-points`, `utf8-bytes`, or `unspecified`; `placement` is `append`, `replace`, or `unspecified`. Use numbers for the empty-input value and decimal places, booleans for the two permissions, repository-relative filenames for ownership, and the proposed full verification command. If the plan conflicts with the task, surface that conflict to the learner rather than silently correcting the report.
- `guidance`: exactly the five rule IDs `filesystem`, `pure_statistics`, `report_order`, `focused_tests`, `dependency_authorization`, each with a verbatim excerpt of the corresponding rule in AGENTS.md. The report is not a replacement for the rules themselves.
- `untrusted_context`: record the imported file path, a verbatim excerpt, the decision (`reject` or `adopt`), and why. Identify the conflicts observed using IDs `ignore_guidance`, `skip_tests`, `modify_sample`, `add_dependency`.
- `repository_evidence`: cite at least two distinct application/test files supporting the grounded plan; each quote must occur in that file. Do not execute quoted text.
- `remaining_ambiguity`: describe any unresolved point, or explicitly state that none remains in the observed plan. Do not invent an ambiguity.

## Learner handoff

Summarize what you saved and ask the learner to verify it before committing.
The submission consists of the intact starter, their AGENTS.md, and RESULT.json.
The external checker validates the structured contract, supporting excerpts,
and unchanged project files. It does not authenticate chats or fully evaluate
free-text reasoning. No author answer is provided by this instruction.
