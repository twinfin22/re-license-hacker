# Markdown Schemas

Use these schemas for manual operation. Keep them boring and stable.

## Directory Shape

```text
study_plan.md
daily_logs/
  YYYY-MM-DD.md
wrong_answers.md
review_queue.md
micro_skills.md
first_principles.md
mock_results.md
sources.md
weekly_review.md
```

## Daily Log

```md
# Daily Study Log

날짜:
공부 시작:
공부 종료:
순공부시간:

오늘 푼 것:
- 과목/단원:
- 자료: 단원별 기출 / 연도별 기출 / 복습 / 모의고사 / 기타

오답:
- W1:
- W2:
- W3:

오늘 질문:
- Q1:

Codex 처리:
- 생성/갱신한 파일:
- 신규 학습 잠금:
- 내일 최우선:
- 전략 판정:
```

## Wrong Answers

```md
## W{id} - {date}

- source_question_id:
- subject:
- chapter:
- source_type: official_past_exam | user_uploaded_past_exam | unknown
- user_input:
- wrong_reason:
- trap:
- linked_micro_skill_ids:
- linked_first_principle_id:
- status: needs_source | queued | reviewing | mastered | rebuild
- notes:
```

## Review Queue

```md
## R{id}

- source_question_id:
- reissue_question_id:
- wrong_answer_id:
- micro_skill_id:
- status: learning | fragile | mastered | lapsed | rebuild
- due_at:
- overdue_days:
- estimated_minutes:
- estimated_recall:
- stability:
- difficulty:
- lapse_count:
- last_result:
- response_time:
- confidence:
- parameter_version:
- selector_version:
```

## Micro Skills

```md
## MS{id}

- subject:
- chapter:
- description:
- trap:
- linked_first_principle_id:
- evidence_question_ids:
- priority: high | medium | low
- mastery_status: unknown | learning | fragile | mastered
- notes:
```

## First Principles

```md
## FP{id}

- subject:
- chapter:
- principle:
- plain_example:
- rule:
- exception:
- trap:
- test_question:
- evidence_question_ids:
- linked_micro_skill_ids:
- validation_status: draft | verified | needs_review
- version:
- supersedes_id:
```

## Study Plan

```md
# Study Plan

## Strategy

- mode: 300h_conditional_same_year
- target_scores:
  - 부동산학개론:
  - 민법:
  - 중개사법:
  - 공법:
  - 공시법+세법:
- current_track: keep_dual_track | keep_dual_track_reduced_scope | switch_to_first_exam_only
- week8_cutoff_decision:
- weekly_min_max_guardrails:
  - 민법:
  - 부동산학개론:
  - 중개사법:
  - 공법:
  - 공시법+세법:
  - 실전모의/오답:

## Today

- review debt:
- new study lock:
- priority subjects:
- weekly_guardrail_status:

## Tomorrow

1.
2.
3.

## This Week

- milestone:
- risk:
- next recalibration:
- next_two_week_allocation:
  - 민법:
  - 부동산학개론:
  - 중개사법:
  - 공법:
  - 공시법+세법:
  - 실전모의/오답:
```

## Mock Results

```md
## {date}

- exam_year:
- timed: yes | no
- scores:
  - 부동산학개론:
  - 민법:
  - 중개사법:
  - 공법:
  - 공시법:
  - 세법:
- wrong_answer_ids:
- time_shortage:
- decision: keep_dual_track | warn_dual_track | keep_dual_track_reduced_scope | switch_to_first_exam_only | rebalance_subject_time
- next_two_week_adjustment:
- next_two_week_allocation:
  - 민법:
  - 부동산학개론:
  - 중개사법:
  - 공법:
  - 공시법:
  - 세법:
  - 실전모의/오답:
- next_two_week_guardrails:
  - 민법:
  - 부동산학개론:
  - 중개사법:
  - 공법:
  - 공시법+세법:
  - 실전모의/오답:
- week8_cutoff_decision:
```

## Weekly Review

```md
## {week_start} - {week_end}

- total_study_minutes:
- review_debt_trend:
- repeated_wrong_patterns:
- subject_role_status:
  - 민법 first-exam defense:
  - 부동산학개론 score-source:
  - 중개사법 high-score:
  - 공법 floor-defense:
  - 공시법/세법 maintenance:
- hard_gate_status:
  - Week 4 민법 40:
  - Week 6 1차 평균 55:
  - Week 8 1차 평균 60:
  - Week 10 공법 40:
  - Week 11 중개사법 70:
- next_week_lock_risks:
- decision:
```
