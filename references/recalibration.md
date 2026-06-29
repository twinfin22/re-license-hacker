# Recalibration

## Weekly Review

Every Sunday, create or update `weekly_review.md`.

Include:

- total study minutes
- review debt trend
- due/overdue/rebuild counts
- repeated wrong-answer patterns
- subject risk ranking
- subject role status: first-exam defense, second-exam average, floor defense, maintenance
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

## Time Reallocation Rules

Every two weeks, change the next two-week subject allocation from timed past-exam or mock scores. Do not rebalance from mood, effort, or vague confidence.

Default 300-hour role weights and guardrails:

| Subject | Strategic role | Target | Default | Min | Max |
|---|---|---:|---:|---:|---:|
| 민법 | first-exam defense | 60+ | 25% | 20% | 35% |
| 부동산학개론 | first-exam score source | 70+ | 15% | 10% | 25% |
| 중개사법 | second-exam high-score source | 75+ | 15% | 10% | 25% |
| 공법 | second-exam floor defense | 45-55 | 15% | 10% | 25% |
| 공시법 | second-exam maintenance | 55-65 combined | 12% | 5% | 18% |
| 세법 | second-exam maintenance | 55-65 combined | 8% | 5% | 12% |
| 실전모의/오답 | score stabilization | average 65 buffer | 10% | 8% | 20% |

Adjustment rules:

- If 1차 average is below 60, shift 10-20% of the next two weeks into 민법/부동산학개론 and reduce second-exam expansion.
- If 민법 is below 50, move 민법 toward the top of its weekly max range until the risk is contained.
- If 부동산학개론 is below 65, prioritize calculation, economics, finance, and high-frequency concept selectors.
- If 중개사법 is below 70 after Week 8, add repetition but do not push 민법 below its weekly minimum.
- If 공법 is below 45 or any core 공법 micro-skill is lapsed, add floor-defense blocks before 공시법/세법 expansion.
- If 공시법+세법 combined is below 55, add maintenance blocks; if above 65, keep only due review and high-yield misses.
- If review debt is over 60 minutes, pay debt first and postpone new expansion.

## Hard Gates

| Time | Gate | Decision |
|---|---|---|
| Week 4 | 민법 below 40 | dual-track risk warning |
| Week 6 | first exam average below 55 | consider prioritizing first exam |
| Week 8 | first exam average below 60 | strongly recommend switching to first exam only |
| Week 8 | first exam average 60-64 | keep dual-track only with reduced second-exam scope |
| Week 8 | first exam average 65+ | keep dual-track |
| Week 10 | 공법 below 40 | second exam failure-risk warning |
| Week 11 | 중개사법 below 70 | second exam average-risk warning |

## Recalibration Workflow

```text
collect last two weeks of logs
-> compare estimated recall with actual correctness
-> compare mock scores with target scores and subject roles
-> find high repeated-wrong micro-skills
-> inspect lapse_count >= 3 items
-> compare selector performance
-> run held-out past-question check when possible
-> reallocate the next two-week subject weights with min/max guardrails
-> promote better parameters
-> roll back worse parameters
```

## Decision Language

Use direct labels:

- `keep_dual_track`
- `warn_dual_track`
- `keep_dual_track_reduced_scope`
- `switch_to_first_exam_only`
- `lock_new_study`
- `reduce_second_exam_scope`
- `rebalance_subject_time`
- `rebuild_selector`

Do not hide a failing gate. If the data says the dual-track plan is likely failing, say so directly while treating Week 8 first-exam-only switching as a strong recommendation.
