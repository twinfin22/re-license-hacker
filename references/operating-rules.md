# Operating Rules

## Purpose

The system exists to convert repeated wrong answers from Korean licensed real estate agent past exams into reliable correct answers. It should reduce repeated mistakes, not maximize study time, chat volume, or note production.

## Non-Negotiable Rules

- Use only existing past-exam questions for reissue.
- Never generate new question bodies, choices, cases, OX items, fill-in-the-blank items, or variant questions.
- Never alter official past-exam text, choices, numbers, periods, parties, facts, or answers.
- Select similar questions only by existing `question_id`.
- If a wrong answer cannot be matched to a source, mark it `needs_source` and exclude it from reissue.
- Write explanations only for questions the user explicitly asked about.
- Link at most one first principle to each wrong answer.
- Increase a first principle version when a new insight changes it.
- Create `weekly_review.md` every Sunday.
- Update `mock_results.md` every two weeks or after a timed past-exam set.

## Daily Input Contract

The user should provide only:

- study start time
- study end time
- units studied
- wrong-answer photos or wrong-answer numbers
- explicit questions, if any

Do not demand a perfect data entry workflow. If fields are missing, proceed with `unknown` or ask only the minimum follow-up needed to avoid a bad operational decision.

## Daily Duties

1. Save the daily log.
2. Label wrong answers as `W1`, `W2`, `W3`, etc.
3. Match each wrong answer to a source question when possible.
4. Classify the reason for the mistake into micro-skills.
5. Draft or update first principles only when useful.
6. Update the review queue.
7. Calculate review debt.
8. Decide whether new study is locked.
9. Generate tomorrow's plan.
10. Answer only explicit questions.

## Lock Rules

- Lock new study when estimated review debt exceeds 60 minutes.
- Lock new study when more than 10 core micro-skills are overdue.
- Prioritize 민법 and 중개사법 core lapses the next day.
- Mark any item with `lapse_count >= 3` as `rebuild`.

## Fragile Rules

Mark a correct answer as `fragile` when:

- confidence is 3/5 or lower
- response time exceeds 90 seconds
- the user guessed
- the user changed the answer after seeing a hint

## Anti-Patterns

- Turning the system into a note generator.
- Writing full explanations for every wrong answer.
- Creating new practice questions because matching is hard.
- Over-splitting micro-skills before enough logs exist.
- Treating old-law questions as current without source notes.
- Letting review debt grow while adding new chapters.
