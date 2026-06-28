# Recalibration

## Weekly Review

Every Sunday, create or update `weekly_review.md`.

Include:

- total study minutes
- review debt trend
- due/overdue/rebuild counts
- repeated wrong-answer patterns
- subject risk ranking
- micro-skills to merge, split, or rebuild
- next week's lock risks

## Biweekly Mock Review

Every two weeks, or after a timed past-exam set, update `mock_results.md`.

User input:

- scores by subject
- wrong-answer photos or numbers

Codex output:

- chapter-level wrong-answer clusters
- time shortage signal
- guessed-question signal if available
- predicted recall vs actual result
- selector promotion, demotion, or rollback
- next two-week time allocation
- dual-track risk decision

## Hard Gates

| Time | Gate | Decision |
|---|---|---|
| Week 4 | 민법 below 40 | dual-track risk warning |
| Week 6 | first exam average below 55 | consider prioritizing first exam |
| End of August | first exam average below 70 | switch to first exam only |
| Week 10 | 공법 below 40 | second exam failure-risk warning |
| Week 11 | 중개사법 below 70 | second exam average-risk warning |

## Recalibration Workflow

```text
collect last two weeks of logs
-> compare estimated recall with actual correctness
-> find high repeated-wrong micro-skills
-> inspect lapse_count >= 3 items
-> compare selector performance
-> run held-out past-question check when possible
-> promote better parameters
-> roll back worse parameters
```

## Decision Language

Use direct labels:

- `keep_dual_track`
- `warn_dual_track`
- `switch_to_first_exam_only`
- `lock_new_study`
- `reduce_second_exam_scope`
- `rebuild_selector`

Do not soften a hard gate. If the data says the plan is failing, say so.
