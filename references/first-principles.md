# First Principles

## Purpose

A first principle is not a summary. It is a reusable judgment structure that helps the learner answer existing past-exam choices correctly.

Use this shape:

```text
condition -> judgment -> exception -> common trap -> existing past-exam verification
```

## When To Create

Create or update a first principle when:

- the same trap appears across multiple wrong answers
- the learner knows the keyword but fails the judgment
- similar existing past questions are being missed
- the item has high ROI for 민법, 중개사법, or a score-risk chapter

Do not create one just because a question was wrong.

## Object Shape

```yaml
id:
subject:
chapter:
principle:
plain_example:
rule:
exception:
trap:
test_question:
evidence_question_ids:
linked_micro_skill_ids:
validation_status: draft | verified | needs_review
version:
supersedes_id:
```

## Validation

- `needs_review`: source or rule is uncertain.
- `draft`: seen in one question or not yet tested.
- `verified`: repeated across at least three question/choice examples and useful in held-out past questions.

Promote only when the principle helps answer existing past questions, not when it sounds elegant.

## Failure Patterns

- Grouping by keyword instead of judgment structure.
- Absorbing a wrong choice as if it were true.
- Creating generic statements that do not help under exam pressure.
- Over-generalizing from one question.
- Mixing law before and after amendment without a source note.
- Treating a trap as the rule.

## Versioning

When a new insight changes the principle:

1. Create a new version.
2. Preserve the old version through `supersedes_id`.
3. Update linked micro-skills only if the new version changes reissue selection.
4. Mark stale or misleading principles as `needs_review` before relying on them.
