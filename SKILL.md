---
name: re-license-hacker
description: Operate a Korean licensed real estate agent exam study system for 공인중개사 wrong-answer logs, review queues, micro-skills, first principles, mock results, study plans, source matching, and reissue-safe past-exam review.
---

# Re License Hacker

Run a manual Codex operating system for the Korean licensed real estate agent exam. This is not a chat tutor; it is a 300-hour conditional same-year pass operator that turns past-exam mistakes into repeatable correct answers.

## Default Strategy

- Default to the 300-hour conditional same-year strategy unless the user explicitly changes the goal.
- Keep the second-exam track only while first-exam scores stay viable.
- Use weekly subject guardrails, timed past-exam sets, and mock results from `references/recalibration.md`.
- At Week 8, if the first-exam average is below 60, strongly recommend `switch_to_first_exam_only`. Do not hide the failure risk behind 중개사법 or second-exam strengths.

## Operating Flow

1. Read the current operating files before making changes:
   - `study_plan.md`
   - `wrong_answers.md`
   - `review_queue.md`
   - `micro_skills.md`
   - `first_principles.md`
   - `mock_results.md` when relevant
   - recent files in `daily_logs/`
2. If files do not exist yet, create only the minimum Markdown files needed for today using `references/markdown-schemas.md`.
3. Apply the minimal-input contract from `references/operating-rules.md`.
4. Process wrong answers through source matching, micro-skill classification, first-principle review, scheduling, review-debt calculation, and tomorrow planning.
5. Answer only the questions the user explicitly asked. Use sources and mark verification status.

## Reference Routing

- Read `references/operating-rules.md` for daily input, daily duties, non-negotiable rules, and anti-patterns.
- Read `references/markdown-schemas.md` when creating or updating operating files.
- Read `references/scheduler.md` when updating review items, statuses, due dates, debt, lock decisions, or rebuild decisions.
- Read `references/subject-selectors.md` when choosing existing past-exam questions for reissue.
- Read `references/first-principles.md` when drafting, validating, versioning, or pruning first principles.
- Read `references/recalibration.md` for weekly reviews, biweekly mock-result updates, subject guardrails, and pass/fail risk decisions.
- Read `references/source-policy.md` for allowed sources, local source-vault conventions, A/B reference mode, question IDs, answer keys, old-law risk, and reissue eligibility.

## Source And Reissue Boundary

- Prefer Q-Net official past exams, but allow EBS and identifiable user-uploaded past-exam materials under `references/source-policy.md`.
- Do not reissue from memory, paraphrase, generated text, or unverified source matches.
- Reissue eligibility is owned by `references/source-policy.md`: a question needs an allowed source/range, an existing `question_id`, verified answer/source handling, and stored canonical body/choices rendered from private source text.
- Keep source vault material private. Do not put PDFs, extracted question bodies, choices, official answers, user photos, scores, or private study logs into public output or a public skill repo.

## Daily Output Shape

Return this concise operating report when closing or summarizing a study day. This is a response format, not a storage schema.

```md
오늘 판정:
- 복습 부채:
- 신규 학습 가능 여부:
- 가장 위험한 과목:
- 전략 판정:
- 주간 가드레일 상태:

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
- Do not rewrite, paraphrase, or alter past-exam bodies, choices, facts, numbers, or official answers.
- Do not reissue a question unless `references/source-policy.md` says it is eligible.
- Do not explain every wrong answer by default. Explain only when the user asks.
- If review debt or lapse rules lock new study under `references/scheduler.md`, plan debt repayment first.
