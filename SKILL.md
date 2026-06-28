---
name: re-license-hacker
description: Operate a Korean licensed real estate agent exam study system based on past-exam wrong answers, W-labeling, micro-skill tagging, review queues, review-debt locking, no-new-question rules, daily plans, weekly reviews, and biweekly recalibration. Use when managing 공인중개사 study logs, wrong_answers, review_queue, micro_skills, first_principles, mock_results, study_plan, or any Codex-run workflow for turning past-exam mistakes into repeatable correct answers.
---

# Re License Hacker

Run a manual Codex operating system for the Korean licensed real estate agent exam. This is not a chat tutor; it is a wrong-answer reissue operator that keeps the learner from repeating the same past-exam mistakes.

## Core Workflow

1. Read the current operating files before making changes:
   - `study_plan.md`
   - `wrong_answers.md`
   - `review_queue.md`
   - `micro_skills.md`
   - `first_principles.md`
   - `mock_results.md` when relevant
   - recent files in `daily_logs/`
2. If files do not exist yet, create only the minimum Markdown files needed for today. Use `references/markdown-schemas.md`.
3. Parse the user's daily input: date, start time, end time, units studied, wrong-answer photos or numbers, and any explicit questions.
4. Label each wrong answer as `W1`, `W2`, `W3`, etc. Preserve the user's wording and uncertainty.
5. Match each wrong answer to an existing `question_id` when possible. If source matching fails, mark it `needs_source` and do not add it to reissue.
6. Classify the mistake into one or more micro-skills. Keep the tag practical enough to select existing past questions.
7. Draft a first principle only when the same trap is likely to recur. Link at most one first principle per wrong answer.
8. Update the review queue using `references/scheduler.md`.
9. Calculate review debt and decide whether new study is locked.
10. Generate tomorrow's plan: review first, then new study only if unlocked.
11. Answer only the questions the user explicitly asked. Use sources and mark verification status.

## Reference Routing

- Read `references/operating-rules.md` for non-negotiable rules, especially no-new-question policy.
- Read `references/markdown-schemas.md` when creating or updating operating files.
- Read `references/scheduler.md` when updating review items, statuses, due dates, or lock decisions.
- Read `references/subject-selectors.md` when choosing which existing past questions to reissue.
- Read `references/first-principles.md` when drafting, validating, versioning, or pruning first principles.
- Read `references/recalibration.md` for weekly reviews, biweekly mock-result updates, and pass/fail gates.
- Read `references/source-policy.md` when handling Q-Net, EBS, question IDs, source versions, hashes, or old-law risk.

## Daily Output Shape

Return a concise operating report:

```md
오늘 판정:
- 복습 부채:
- 신규 학습 가능 여부:
- 가장 위험한 과목:

내일 계획:
1.
2.
3.

복습 큐:
- due today:
- overdue:
- rebuild:

오답 재출제:
- W1:
- W2:

질문 답변:
- Q1:
```

## Hard Stops

- Do not generate new exam questions.
- Do not rewrite, paraphrase, or alter past-exam bodies, choices, or official answers.
- Do not reissue a question without a verified existing `question_id`.
- Do not explain every wrong answer by default. Explain only when the user asks.
- If review debt exceeds 60 minutes, lock new study and plan debt repayment first.
- If an item lapses three times, mark it `rebuild` and review the micro-skill or selector rule.
