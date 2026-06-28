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

## Today

- review debt:
- new study lock:
- priority subjects:

## Tomorrow

1.
2.
3.

## This Week

- milestone:
- risk:
- next recalibration:
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
- decision: keep_dual_track | warn | switch_to_first_exam_only
- next_two_week_adjustment:
```
