# PRD: 공인중개사 AI 튜터

작성일: 2026-06-28  
목표 시험일: 2026-10-31  
가동 시작일: 2026-06-29 월요일  
상태: Draft v2  
운영 방식: 당분간 Codex 수동 운영. 웹앱 전환 시점은 미정.  

## 1. 한 줄 정의

이 제품은 AI 선생님이 아니다.

최근 10개년 기출 오답을 다시 틀리지 않게 만드는 오답 재출제 운영체제다.

## 2. 목표

Objective function:

```text
minimize(time_spent_on_studying)
minimize(rewrong_rate)
maximize(past_exam_question_to_real_answer_conversion)
```

현실 목표:

- 300-400시간 안에 최근 10개년 공인중개사 기출 오답을 실전 정답으로 전환한다.
- 2026-06-29부터 전 과목 단원별 기출 회전을 시작한다.
- 단원별 기출로 전 범위를 한 번 훑은 뒤, 연도별 기출 회전을 반복한다.
- 8월 말 1차 평균 70점 미만이면 동차를 포기하고 1차 합격으로 전환한다.
- 공부량을 늘리는 앱이 아니라, 이미 틀린 문제를 다시 틀리는 낭비를 차단하는 앱을 만든다.

냉정한 판단:

- 300-400시간 동차는 빡세다.
- 이 PRD는 "잘 공부하기"가 아니라 "합격선 통과 확률이 낮은 행동을 버리기" 위한 문서다.
- 강의 완강, 예쁜 노트, 전 범위 완벽 이해는 목표가 아니다.

## 3. 핵심 전제

- 초기 데이터는 공개 기출 PDF, 공식 정답, 법령만 사용한다.
- 기출 정답은 당시 공식 정답 기준을 따른다.
- 문제 해설은 사용자가 질문하기 전까지 작성하지 않는다.
- 저장소는 당분간 Markdown이다.
- 사용자는 매일 아침 3-4시간 deep focus로 공부한다.
- 사용자가 매일 입력하는 것은 공부 시작 시간, 종료 시간, 오답뿐이다.
- 격주 recalibration에서 사용자가 입력하는 것은 과목별 점수와 오답뿐이다.
- 복습 부채가 60분을 넘으면 신규 학습은 잠근다.
- 새 문제 생성은 금지한다. 모든 재출제는 기존 기출 `question_id` 선택이다.

## 4. Benchmark 결론

AI 교육 제품의 핵심은 채팅이 아니다.

- Alpha / 2 Hour Learning: 짧은 집중 학습, adaptive software, guide 운영. 검증은 약하지만 루틴 강제는 참고.
- Khanmigo: 답을 바로 주지 않고 힌트와 질문으로 유도. 공인중개사도 보기 제거 이유를 훈련해야 한다.
- Synthesis Tutor: 자유 채팅보다 전문가가 만든 lesson + micro-assessment가 핵심.
- Squirrel AI: 지식 포인트를 잘게 쪼개고 약점만 학습.
- Riiid / Santa: 시험 대비형에 가장 가까움. 풀이 로그로 다음 문제를 추천.
- ALEKS / MATHia: 지금 배울 준비가 된 항목만 추천.
- Anki / SuperMemo / FSRS: 정답 여부보다 interval, review debt, lapse 관리가 중요.
- Intelligent Tutoring / Knowledge Tracing: 문항-지식요소 매핑은 필요하지만, 처음부터 과분해하면 쓰레기 데이터가 된다.

PRD 적용:

- canonical 기출 DB
- micro-skill 태그
- first principle은 단순 객체로 시작
- 오답 재출제
- 복습 부채
- 재오답률 감소
- `question_id` 기반 No New Questions
- kill-switch
- 근거 기반 Q&A

## 5. 성공 지표

일반 앱 지표는 버린다. DAU, 체류시간은 보조 지표다.

핵심 지표:

- 재오답률
- 같은 함정 재발률
- due item 처리율
- 복습 부채 총량
- overdue 복습 수
- micro-skill별 mastery 비율
- first principle transfer 성공률
- 격주 기출 오답 수 감소
- 8월 말 1차 평균 70점 달성 여부

목표 점수:

| 과목 | 목표 | 실전 목표 |
|---|---:|---:|
| 부동산학개론 | 70 | 75 |
| 민법 | 60 | 65 |
| 중개사법 | 75 | 80 |
| 공법 | 50 | 55 |
| 공시법+세법 | 60 | 65 |

## 6. MVP 범위

MVP는 하나다.

Codex 운영 MVP와 웹앱 MVP는 같은 입력, 같은 판단 규칙, 같은 출력물을 써야 한다.  
웹앱은 Codex 운영을 자동화한 인터페이스일 뿐, 별도 제품 범위를 갖지 않는다.

### 6.1 공통 MVP 기능

1. Daily Study Log 수집
2. 오답 사진 라벨링
3. 오답을 micro-skill로 분해
4. 기존 기출 `question_id`와 연결
5. 오답 재출제 큐 생성
6. 복습 부채 계산
7. 신규 학습 잠금 판단
8. 과목별 self-evolving selector
9. 격주 기출 결과 기반 재보정
10. 질문한 문제만 해설 작성
11. first principle 초안 작성과 검증 상태 관리

### 6.2 Codex 운영과 웹앱의 1:1 대응

| Codex 산출물 | 웹앱 대응 |
|---|---|
| `daily_logs/` | study_logs |
| `wrong_answers.md` | wrong_answers |
| `review_queue.md` | review_items |
| `micro_skills.md` | micro_skills |
| `first_principles.md` | first_principles |
| `mock_results.md` | mock_results |
| `study_plan.md` | study_plans |
| `sources.md` | sources |

### 6.3 Non-goals

- 예쁜 노트 생성
- 모든 문제 자동 해설 작성
- 전 과목 완벽 이해
- 상업 해설집/강의자료 사용
- 2015년 이전 기출 학습
- 점수 예측 제품화
- OCR 파이프라인 먼저 만들기
- 새 문제 생성
- 기존 기출 보기/숫자/사례를 바꾼 변형 문제 생성
- Codex 운영과 다른 웹앱 전용 MVP 만들기

## 7. 데이터 소스

초기 DB:

- Q-Net 기출문제: https://www.q-net.or.kr/cst003.do?id=cst00309&gSite=L&gId=08
- EBS 기출/답안: https://www.ebs.co.kr/land/examData/previous/30004650703?p=Yy5wYWdlPTEmYy5wYWdlU2l6ZT0yMCZzZWFyY2hLZXl3b3JkPSZzZWFyY2hDb25kaXRpb249

기출 범위:

- DB 구축: 2016-2025, 최근 10개년
- Phase 1 실제 학습: 전 과목 단원별 기출
- 단원별 1회독 후: 2021-2025 연도별 기출 반복
- 2018-2020: 약점 단원 보강
- 2016-2017: 반복 micro-skill만
- 2015 이전: 버림

이유:

- 시중 표준은 최근 10개년이다.
- 300-400시간 전략에서 10년 초과 기출은 ROI가 낮다.
- 공법/세법/중개사법은 법령 개정 리스크가 크다.

## 8. 핵심 개념

### 8.1 문항 쪼개기

문제 1개를 그대로 저장하지 않는다. 다음 단위로 쪼갠다.

- 보기별 함정
- 필요한 개념
- 틀린 이유
- micro-skill
- 재출제할 기존 `question_id`

예:

```text
민법 1문제
→ 대항요건 발생시점
→ 무효/취소 구별
→ 제3자에게 주장 가능 여부
→ 유사 기출 question_id 선택
```

### 8.2 First Principle 추출 엔진

목표는 기출 요약이 아니다.  
여러 보기의 차이에서 반복되는 판단 구조를 뽑고, 그 원리로 기존 유사 기출을 맞히게 하는 것이다.

브루탈한 원칙:

- 처음부터 객체를 많이 쪼개면 지식그래프 쓰레기장이 된다.
- 첫 버전은 단순해야 한다.
- 한 오답에는 first principle을 최대 1개만 연결한다.
- 세분화는 학습 로그가 쌓인 뒤 병합/분리가 필요할 때만 한다.

First principle 객체:

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

핵심 단위:

```text
조건 -> 판단 -> 예외 -> 자주 틀리는 착각 -> 기존 기출로 검증
```

좋은 예시 1: 민법

```yaml
principle: 부동산 물권변동은 원인행위만으로 끝나지 않고, 등기 같은 공시요건이 맞아야 완성된다.
plain_example: 매매계약을 했다고 바로 소유권자가 되는 것이 아니다. 소유권 이전등기까지 해야 원칙적으로 물권변동이 완성된다.
rule: 법률행위로 인한 부동산 물권변동은 등기해야 효력이 생긴다.
exception: 상속처럼 법률규정에 의한 물권취득은 등기 없이도 취득하지만, 처분하려면 등기가 필요하다.
trap: "계약 체결 = 소유권 이전"으로 착각한다.
test_question: 이 지문이 계약의 효력만 묻는지, 물권변동 완성을 묻는지 먼저 나눈다.
```

좋은 예시 2: 민법

```yaml
principle: 취소할 수 있는 행위는 취소 전까지 일단 유효하고, 무효는 처음부터 효력이 없다.
plain_example: 미성년자가 단독으로 한 계약은 바로 없는 계약이 아니라, 취소되기 전까지는 유효한 계약으로 다뤄진다.
rule: 취소는 취소권자가 행사해야 소급하여 무효가 된다.
exception: 처음부터 강행규정 위반 등으로 무효인 행위는 취소를 기다릴 필요가 없다.
trap: "취소 가능 = 당연 무효"로 착각한다.
test_question: 지문이 무효 사유를 묻는지, 취소권 행사 전후 효과를 묻는지 먼저 본다.
```

좋은 예시 3: 중개사법

```yaml
principle: 중개대상물 확인설명의무는 거래 전에 위험 정보를 드러내기 위한 의무다.
plain_example: 등기부에 권리관계가 적혀 있어도, 중개업자는 중요한 권리관계와 제한사항을 확인하고 설명해야 한다.
rule: 권리관계, 공법상 제한, 거래상 중요사항은 확인설명 대상이다.
exception: 법령상 확인설명 대상이 아닌 사소한 정보까지 무한정 설명하는 의무는 아니다.
trap: "공부상 공개된 정보면 설명 안 해도 됨"으로 착각한다.
test_question: 이 정보가 거래 결정에 중요한 위험인지 먼저 본다.
```

추출 파이프라인:

```text
기출 문항/보기/정답 수집
→ 이 문항이 맞히게 하려는 claim 1개 정의
→ 정답 보기와 오답 보기의 최소 차이 추출
→ 조건/판단/예외/착각으로 압축
→ 같은 구조의 기존 question_id 2개 이상 연결
→ 법령/공식 정답/검증된 해설 근거 연결
→ first principle 초안 작성
→ held-out 기출에 적용해 맞히는지 검증
→ 성능 낮으면 병합/분리/versioning
```

검증 기준:

- 근거 없는 principle은 `needs_review`.
- 한 문제에서만 나온 principle은 `draft`.
- 최소 3개 이상 기출/보기에서 반복되면 `verified` 후보.
- held-out 보기 20개 중 16개 이상 판단 성공해야 승격.
- 조건 하나를 바꿨을 때 답이 바뀌는 counterfactual test를 통과해야 한다.
- 실전 오답 감소에 기여하지 못하면 병합 또는 삭제 후보로 둔다.

실패 패턴:

- 키워드가 같다는 이유로 묶기.
- 오답 보기를 사실로 흡수하기.
- "권리변동은 원인과 요건이 맞아야 발생한다"처럼 당연하지만 시험장에서 쓸 수 없는 문장 만들기.
- 한 문제에서 과잉 일반화하기.
- 법 개정 전후를 섞기.
- 함정을 규칙으로 착각하기.

### 8.3 사진 입력: Vision-first, OCR-later

OCR은 `Optical Character Recognition`이다.  
사진 속 글자를 텍스트로 바꾸는 기술이다.

MVP 판단:

- 지금은 OCR 제품이 필요 없다.
- 입력은 책/프린트 기출 오답 사진이다.
- 사진을 vision 모델이 읽고, 사용자가 추출 텍스트를 확인/수정하면 충분하다.
- 손글씨 인식, 낙서 정리, 전자책 자동 추출은 MVP 범위가 아니다.
- OCR은 검색, 대량 파싱, 정확한 원문 저장, 하이라이트, 장기 DB 품질이 중요해질 때 붙인다.

사진 입력 흐름:

```text
사진 업로드
→ vision으로 문제/보기/필기/밑줄 읽기
→ 추출 텍스트와 문제번호 후보 표시
→ 사용자가 확인/수정
→ canonical 기출 DB와 매칭
→ 기존 기출 question_id 선택
```

주의:

- 작은 글씨, 흐린 사진, 회전, 표, 한국어 조문은 vision도 틀릴 수 있다.
- OCR을 붙여도 최종 확인은 필요하다.
- MVP의 병목은 글자 인식이 아니라, 인식된 오답을 좋은 재출제 항목으로 바꾸는 것이다.

### 8.4 No New Questions 정책

새 문제 생성은 절대 금지한다.  
재출제는 기존 기출 `question_id` 검색과 선택만 허용한다.

허용:

- 기존 기출 문제 원문 표시.
- 기존 기출 보기 원문 표시.
- 기존 기출 중 유사 문제 검색.
- 기존 기출의 문제번호, 과목, 단원, micro-skill 태깅.
- 해설, first principle, 틀린 이유, 검색 쿼리 작성/갱신.

금지:

- 새 지문 생성.
- 새 보기 생성.
- 기존 보기의 숫자, 기간, 주체, 사례를 바꾼 변형 생성.
- `OX`, 빈칸, 사례형 문제를 새로 만드는 것.
- LLM이 만든 문장을 문제처럼 보여주는 것.
- first principle을 이유로 기출 원문을 수정하는 것.

단순 강제 규칙:

```yaml
allowed_question_id_range:
  min_year: 2016
  max_year: 2025
  allowed_source_type:
    - official_past_exam
    - user_uploaded_past_exam
  allowed_status:
    - verified

reissue_rule:
  - selected question_id must exist
  - selected question_id must be inside allowed_question_id_range
  - selected question_id must have official_text_hash
  - selected question_id body and choices must be rendered from DB only
  - LLM output cannot contain generated body or generated choices
```

문항 ID 예시:

```text
REA-2025-1-LAW-001
REA-2024-2-BROKER-018
REA-2023-2-TAX-033
```

저장 조건:

- 모든 문항은 `source_exam_id`, `question_id`, `year`, `official_text_hash`, `license_scope`가 있어야 한다.
- 출처와 해시 없는 문항은 저장할 수 없다.
- 한번 저장된 `body`, `choices`, `official_answer`, `official_text_hash`는 immutable이다.
- 원문 정정이 필요하면 기존 row 수정이 아니라 새 source version을 만들고 이전 version을 archived로 둔다.

## 9. 공통 오답 재출제 스케줄러

핵심 문장:

> 이 앱은 오답을 보관하지 않는다. 까먹기 직전에 다시 시험 보고, 같은 함정을 실전에서 맞힐 때까지 복습 부채로 남긴다.

9번은 공통 스케줄러다.  
12번은 과목별 재출제 item selector다.

오답 처리 흐름:

```text
오답 입력
→ 문제 식별
→ 틀린 이유 분류
→ micro-skill 연결
→ 기존 기출에서 유사 question_id 검색
→ 재출제 항목 선택
→ due_at 설정
→ 복습 큐 반영
→ 실전 정답 전환율 추적
```

오답 1개에서 선택 가능한 항목:

- 같은 기출 재출제
- 같은 micro-skill의 기존 기출 재출제
- 같은 trap pattern의 기존 기출 재출제
- 같은 숫자/기간/주체가 나온 기존 기출 재출제
- 같은 계산 패턴의 기존 기출 재출제
- first principle이 같은 기존 기출 재출제

Self-improving 원칙:

- 정답률을 예측하는 앱이 아니라, 기억 회상확률 `R`을 내부 추정한다.
- 각 review item은 안정도 `S`, 난이도 `D`, 현재 회상확률 `R`을 가진다.
- 재출제 우선순위는 `R 55-85%` 구간을 우선한다.
- 너무 쉬운 항목은 낭비다.
- 너무 어려운 항목은 학습이 아니라 해설 읽기가 된다.
- 매 격주 recalibration 때 실제 정답률과 예측 `R`의 차이를 줄인다.
- self-improving은 문제 생성 품질 개선이 아니라, 기존 기출 선택 품질 개선이다.

## 10. 복습 부채 엔진

복습 부채는 사용자가 아직 갚지 않은 기억 부채다.

필드:

```yaml
review_item_id:
source_question_id:
reissue_question_id:
micro_skill_id:
status: learning | fragile | mastered | lapsed | rebuild
due_at:
overdue_days:
estimated_recall:
stability:
difficulty:
lapse_count:
last_result:
response_time:
confidence:
parameter_version:
```

기본 스케줄:

```text
당일 재시험 -> D+1 -> D+3 -> D+7 -> D+14 -> D+30
```

틀리면:

```text
당일 재시험 -> D+1부터 reset
```

잠금 규칙:

- 복습 부채 > 60분: 신규 학습 잠금
- overdue 핵심 micro-skill > 10개: 신규 학습 잠금
- 민법/중개사법 핵심 lapse 발생: 다음날 최우선 복습
- lapse_count >= 3: micro-skill 태그와 기출 선택 규칙 재검토

## 11. Mastery 기준

Mastery는 복습 종료가 아니다.  
고빈도 복습 큐에서 빠지는 것이다.  
모든 mastered item은 시험 전까지 저빈도 감시 큐에 남는다.

상태:

- learning: 새 항목
- fragile: 맞았지만 느림, 자신감 낮음
- mastered: spaced review 3회 연속 성공
- lapsed: 오답, 힌트 필요, 정답 보고 "아 맞다"
- rebuild: 3회 이상 lapse

Mastered 기준:

- D+1, D+3, D+7 3연속 정답
- 객관식 판단 60-90초 안
- 자신감 4/5 이상
- 최근 14일 lapse 없음
- 예상 recall 90% 이상

Micro-skill mastery:

- 유사 기출 5개 중 4개 이상 정답
- 최소 2회차 이상 떨어져서 성공
- 같은 실수 유형 재발 없음

Retention 목표:

- 기본: 90%
- 민법/중개사법 핵심, 과락 위험 단원: 93-95%
- 97% 이상 금지. workload가 폭증한다.

## 12. 과목별 재출제 Item Selector

과목별 selector는 공부법이 아니다.  
같은 오답 다음에 어떤 기존 기출을 다시 풀게 할지 정한다.

공통 스케줄은 9번이 담당한다.  
과목별 selector는 기존 기출 검색/선택만 담당한다.

### 12.1 Self-evolving selector 규칙

Selector는 고정 규칙이 아니다.  
매주 재오답률, response_time, confidence, overdue 증가 여부를 기준으로 자동 승격, 강등, 롤백된다.

입력:

- 오답의 `source_question_id`
- 과목
- 단원
- micro-skill
- trap
- first principle
- 직전 재출제 결과
- response_time
- confidence
- lapse_count
- overdue 상태

출력:

- 재출제할 기존 `question_id` 1-5개
- 선택 이유
- selector_version
- rollback 가능 로그

승격:

- 같은 trap 재오답률 감소
- response_time 감소
- confidence 상승
- overdue 증가 없음
- 같은 과목에서 2주 연속 성과 유지

강등:

- 재오답률 감소 없음
- 너무 쉬운 문제만 골라 mastery 착시 발생
- 너무 어려운 문제만 골라 해설 읽기만 늘어남
- overdue 폭증
- 같은 오답이 3회 이상 반복

롤백:

```text
새 selector_version 적용
→ 1주 shadow test
→ 성과가 기존 version보다 나쁘면 rollback
→ 좋아지면 active version 승격
```

### 12.2 과목별 selector

| 과목 | selector | 핵심 | self-evolving 기준 |
|---|---|---|---|
| 부동산학개론 | 계산/빈출개념 selector | 같은 계산 유형 기출 | 계산 실수 재발률, 풀이시간 |
| 민법 | 요건판단/유사사례 selector | 같은 요건/함정의 기존 기출 | 유사사례 정답률, 보기 제거 속도 |
| 중개사법 | 숫자-주체-벌칙 selector | 같은 숫자, 기간, 주체, 처분, 벌칙 기출 | 숫자/기간 lapse 감소 |
| 공법 | 구조/과락방어 selector | 같은 법 구조, 허가권자, 절차, 예외 기출 | 과락 단원 오답 감소 |
| 공시법 | 절차/효력비교 selector | 같은 절차, 주체, 효력 비교 기출 | 절차 순서 오답 감소 |
| 세법 | 세목/기한/계산 selector | 같은 세목, 세율, 기한, 과세대상 기출 | 기한/세율/과세대상 오답 감소 |

예시:

```text
민법 W7 오답: 취소와 무효 효과 혼동
→ selector_v1: 같은 연도 다른 문제 재출제
→ 결과: 또 틀림
→ selector_v2: 취소/무효가 섞인 다른 연도 question_id 3개 선택
→ 결과: 2/3 정답, response_time 감소
→ selector_v2 유지
```

## 13. 학습계획 엔진

사용자 입력은 최소화한다.

사용자가 매일 입력하는 것:

- 공부 시작 시간
- 공부 종료 시간
- 오늘 푼 단원
- 오답 사진 또는 오답 번호

Codex가 자동 생성하는 것:

- 순공부시간
- 과목별 시간 배분 추정
- 최근 실전 결과 반영
- 과목별 오답 밀도
- 복습 부채
- micro-skill mastery
- 최근 기출 오답 유형
- 시간당 재오답률 감소
- 오늘 신규 학습 가능 여부
- 내일 공부 순서
- 내일 복습 우선순위

출력:

- 오늘 판정
- 내일 공부 순서
- 신규 학습 가능 여부
- 복습 우선순위
- 과목별 시간 배분
- 이번 주 milestone
- 다음 격주 기출에서 제거할 오답 유형

일일 계획 규칙:

1. 복습 부채 먼저 본다.
2. 부채가 60분 초과면 신규 학습 잠금.
3. 민법은 매일 본다.
4. 공법은 짧게라도 자주 본다.
5. 중개사법은 누적 암기 점수원으로 만든다.
6. 학개론은 계산/빈출 개념으로 점수 유지.
7. 전 과목을 매주 끊기지 않게 돌린다.

## 14. 격주 Recalibration

격주말마다 기출 1회분을 시간 재고 푼다.  
목표는 점수 예측이 아니다.  
지난 2주 스케줄러와 item selector가 오답을 줄였는지 검증하는 것이다.

사용자가 입력하는 것:

- 과목별 점수
- 오답 사진 또는 오답 번호

Codex가 자동 생성하는 것:

- 단원별 오답
- 시간 부족 여부 추정
- 찍은 문제 수 추정
- confidence 추정 또는 누락 표시
- 과목별 순공부시간 추정
- review item별 예측 R
- 실제 정오답 매칭
- 해설 조회 여부
- 재시도 결과
- parameter_version 비교

출력:

- 다음 2주 시간 배분
- 과목별 risk status
- 동차 유지/경고/포기 권고
- 새로 잠글 신규 학습 범위
- 복습 부채 처리 계획
- 스케줄러 파라미터 유지/수정/롤백
- selector별 승격/강등

Self-improving 절차:

```text
최근 2주 로그 수집
→ 예측 R과 실제 정답률 비교
→ 재오답률이 높은 micro-skill 찾기
→ lapse_count >= 3 항목은 태그/선택 규칙 재검토
→ 과목별 selector 성과 비교
→ holdout 기출에서 shadow test
→ 개선되면 parameter_version 승격
→ 나빠지면 롤백
```

승격 기준:

- 같은 함정 재발률 감소.
- overdue가 늘지 않음.
- held-out 오답 재출제 정답률 개선.
- 사용 시간 증가 없이 mastery 비율 개선.

MVP에서 하지 않을 것:

- DKT/RNN/Transformer 지식추적.
- 개인별 고급 IRT.
- 강화학습 bandit.
- 자동 태깅 전면 자동화.

데이터가 없을 때는 FSRS-lite + 오답률 + 베이지안 보정만 쓴다.

Hard gates:

| 시점 | 기준 | 결정 |
|---|---|---|
| 4주차 | 민법 40 미만 | 동차 위험 경고 |
| 6주차 | 1차 평균 55 미만 | 1차 우선 전환 검토 |
| 8월 말 | 1차 평균 70 미만 | 동차 포기, 1차만 |
| 10주차 | 공법 40 미만 | 2차 과락 위험 |
| 11주차 | 중개사법 70 미만 | 2차 평균 위험 |

## 15. 학습 시간 배분

합격후기에는 과목별 시간이 깔끔하게 남아 있지 않은 경우가 많다.  
그래도 반복 패턴은 분명하다.

- 민법 먼저.
- 중개사법은 점수원.
- 공법은 과락 방어.
- 공시법/세법은 깊게 파면 손해.
- 막판 4-8주는 오답/100선/동형/암기장.

300시간 기준:

| 과목 | 시간 | 역할 |
|---|---:|---|
| 민법 | 75h | 1차 생존 |
| 부동산학개론 | 45h | 1차 점수원 |
| 중개사법 | 45h | 2차 평균 견인 |
| 공법 | 45h | 과락 방어 |
| 공시법 | 35h | 공시세법 방어 |
| 세법 | 25h | 버릴 세목과 맞힐 세목 구분 |
| 실전모의/100선/오답 | 30h | 점수 안정화 |

400시간으로 늘어날 경우:

| 과목 | 시간 |
|---|---:|
| 민법 | 100h |
| 부동산학개론 | 60h |
| 중개사법 | 60h |
| 공법 | 60h |
| 공시법 | 47h |
| 세법 | 33h |
| 실전모의/100선/오답 | 40h |

운영 원칙:

- 300시간 플랜으로 시작한다.
- 8월 말까지 1차 평균 70이 안 나오면 2차 시간을 줄이고 1차로 전환한다.
- 점수 상승이 안 나는 과목은 시간 추가보다 selector와 오답 분류부터 고친다.

## 16. Timeline

### Phase 1: 2026-06-29부터, 전 과목 단원별 기출 회전

목표:

- 당장 내일부터 전 과목 기출을 시작한다.
- 처음은 연도별 기출이 아니라 단원별 기출이다.
- 전 범위를 빠르게 훑으며 오답과 micro-skill을 만든다.
- first principle map은 많이 만들지 말고, 자주 틀리는 함정만 만든다.

방식:

```text
단원별 기출
→ 오답 라벨링
→ micro-skill 연결
→ 기존 question_id 재출제
→ 복습 부채 처리
→ 전 범위 1회 스캔 완료
→ 연도별 기출 반복
```

초기 2주 시간 배분:

| 과목 | 비중 | 이유 |
|---|---:|---|
| 민법 | 25% | 1차 병목 |
| 학개론 | 15% | 1차 점수원 |
| 중개사법 | 18% | 2차 평균 견인 |
| 공법 | 17% | 과락 방어는 초반부터 |
| 공시법 | 13% | 절차/효력 반복 필요 |
| 세법 | 7% | 최소 방어선 |
| 복습/오답 | 5% | 부채 폭발 방지 |

첫날 2026-06-29 운영:

1. 공부 시작 시간 기록.
2. 단원별 기출로 전 과목을 짧게라도 시작.
3. 오답 사진 또는 오답 번호를 남김.
4. 공부 종료 시간 기록.
5. Codex가 `daily_logs/2026-06-29.md`, `wrong_answers.md`, `review_queue.md`, `study_plan.md` 갱신.

### Phase 2: 단원별 1회독 완료 후

목표:

- 2021-2025 연도별 기출 회전 시작
- 단원별 오답을 연도별 실전 판단으로 전환
- subject selector 성과 비교

### Phase 3: 8월

목표:

- 전 과목 기출 회전 지속
- 공법/공시/세법 방어선 확보
- 복습 부채 폭발 방지

판정:

- 8월 말 1차 평균 70 미만이면 동차 포기

### Phase 4: 9월

목표:

- 오답/유사문항/100선 중심
- 신규 이론 최소화
- 과목별 실전 점수 안정화

### Phase 5: 10월

목표:

- 신규 학습 금지
- 오답 재출제
- 모의고사
- 숫자/기간/벌칙/세율 최종 회전

## 17. Q&A 기능

Q&A는 보조 기능이다.

원칙:

- 사용자가 질문한 문제만 해설한다.
- 답변은 기출 원문, 공식 정답, 법령, 기존 DB 근거를 먼저 찾는다.
- 근거가 없으면 `확인 필요`로 표시한다.
- 시험장에서 어떻게 판단할지 짧게 말한다.

답변 형식:

```md
정답:
왜:
시험장 판단법:
관련 first principle:
관련 micro-skill:
다시 나올 함정:
출처:
검증 상태: verified | AI draft | needs review
```

## 18. 시간관리

Clock in/out은 기록용이 아니다.  
과목별 ROI 계산용이다.

사용자 입력:

```yaml
date:
start_time:
end_time:
wrong_answers:
```

Codex 생성:

```yaml
net_study_minutes:
subject_time_estimate:
activity_type: review | new | mock | wrong_answer | qna
questions_solved:
correct_count:
wrong_again_count:
mastery_delta:
focus_risk:
```

핵심 계산:

- 복습 시간 대비 재오답률 감소
- 신규 학습 시간 대비 mastery 증가
- 과목별 시간 투입 대비 점수 변화
- 멍때린 시간 감지

## 19. Markdown 저장 구조

```text
real-estate-ai-tutor/
  prd.md
  study_plan.md
  daily_logs/
    2026-06-29.md
  wrong_answers.md
  review_queue.md
  micro_skills.md
  first_principles.md
  mock_results.md
  sources.md
```

## 20. Codex 운영 매뉴얼

### 20.1 매일 사용법

사용자는 하루 공부 후 Codex에 아래만 준다.

- 공부 시작 시간
- 공부 종료 시간
- 오늘 푼 단원
- 오답 사진 또는 오답 번호
- 질문이 있으면 질문

Codex는 다음을 한다.

1. 로그를 Markdown으로 저장
2. 오답을 W1, W2, W3 라벨로 정리
3. 문제 식별 가능하면 기출 DB와 연결
4. 틀린 이유를 micro-skill로 분류
5. 필요한 경우 first principle 초안 작성
6. 복습 큐 업데이트
7. 복습 부채 계산
8. 내일 신규 학습 가능 여부 판단
9. 내일 계획 생성
10. 질문한 문제만 해설

### 20.2 Daily Study Log 템플릿

```md
# Daily Study Log

날짜:
공부 시작:
공부 종료:

오늘 푼 것:
- 과목/단원:
- 자료: 단원별 기출 / 연도별 기출 / 복습 / 모의고사 / 기타

오답:
- W1:
- W2:
- W3:

오늘 질문:
- Q1:

내일 요청:
- 복습 큐 만들어줘
- 신규 학습 가능 여부 판단해줘
- 오답 재출제 만들어줘
```

### 20.3 Codex 응답 형식

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

### 20.4 운영 규칙

- 사진은 하루 5-10장까지.
- 사진마다 W번호를 붙인다.
- 해설은 질문한 문제만 작성한다.
- 새 문제 생성은 금지한다.
- 유사 문제는 기존 기출 `question_id`에서만 고른다.
- 문제 본문/보기는 기출 원문만 보여준다.
- 기출 원문/보기/정답은 절대 바꾸지 않는다.
- first principle은 한 오답당 최대 1개만 연결한다.
- first principle은 새 insight가 있으면 version을 올려 갱신한다.
- 출처를 못 찾은 문제는 재출제하지 않는다.
- 복습 부채가 60분 넘으면 신규 학습 잠금.
- 맞았지만 confidence 3 이하이면 fragile.
- 맞았지만 90초 초과이면 fragile.
- 3회 lapse이면 rebuild.
- 매주 일요일에는 `weekly_review.md`를 만든다.
- 격주말에는 `mock_results.md`를 업데이트한다.

## 21. 웹앱 전환 요구사항

웹앱 전환은 새 제품 범위가 아니다.  
Codex 운영을 더 편하게 만드는 UI와 저장소 전환이다.

전환 조건:

- Codex 운영으로 최소 2주 이상 실제 로그가 쌓임
- 반복 입력 필드가 안정됨
- `question_id` 체계가 고정됨
- review queue가 수동으로라도 효과를 보임
- selector versioning이 실제로 필요한 수준까지 데이터가 생김

핵심 테이블:

```yaml
questions:
  id
  source_exam_id
  source_version
  year
  subject
  question_no
  body
  choices
  official_answer
  source_url
  source_type: official_past_exam | user_uploaded_past_exam
  official_text_hash
  license_scope
  immutable: true
  archived_at

micro_skills:
  id
  subject
  chapter
  first_principle_id
  description
  priority_weight

first_principles:
  id
  subject
  chapter
  principle
  plain_example
  rule
  exception
  trap
  test_question
  evidence_question_ids
  validation_status
  version
  supersedes_id
  active

review_items:
  id
  source_question_id
  reissue_question_id
  micro_skill_id
  subject_selector_type
  status
  due_at
  lapse_count
  confidence
  response_time
  stability
  difficulty
  recall_probability
  parameter_version

retest_events:
  id
  review_item_id
  source_question_id
  reissue_question_id
  official_text_hash
  first_principle_version
  shown_at
  predicted_recall
  result
  selected_choice
  response_time
  confidence
  explanation_opened
  selector_version

study_logs:
  id
  date
  start_time
  end_time
  net_minutes
  subject_time_estimate
  activity_type
  solved_count
  correct_count

mock_results:
  id
  date
  exam_year
  subject_scores
  wrong_counts_by_skill
  decision
```

## 22. 리스크

| 리스크 | 대응 |
|---|---|
| 300-400시간 동차가 너무 낙관적 | 8월 말 1차 평균 70 gate |
| 사진 인식 실패 | vision 추출 후 사용자 확인 필수 |
| AI 해설 hallucination | 질문한 문제만, 출처/검증 상태 표시 |
| 복습 부채 폭발 | 신규 학습 잠금 |
| 오래된 법령 문제 | 당시 정답 기준, 오래된 2차 기출 제한 |
| 예쁜 노트화 | 모든 산출물은 재시험 큐로 연결 |
| first principle 과잉 | 단순 객체로 시작, 실전 정답 전환율로 검증 |
| selector 폭주 | shadow test 후 승격, 실패 시 롤백 |
| 웹앱 과설계 | Codex 운영과 1:1 대응하지 않으면 보류 |

## 23. Open Questions

- 실제 기출 PDF 파싱 난이도
- 과목별 최적 interval
- Gen의 민법 지문 처리속도
- 매일 최소 입력 방식의 지속 가능성
- 사진 vision 추출 정확도
- first principle map을 어느 깊이까지 만들지
- `question_id` 체계 최종 형식

## 24. 다음 액션

2026-06-29 월요일:

1. 전 과목 단원별 기출 회전 시작.
2. 공부 시작/종료 시간만 기록.
3. 오답 사진 또는 오답 번호 5-10개 기록.
4. Codex가 `daily_logs/2026-06-29.md`, `wrong_answers.md`, `review_queue.md`, `micro_skills.md`, `study_plan.md` 생성.
5. 다음날부터 복습 부채 먼저 처리.

## 25. 참고 자료

- Q-Net 공인중개사: https://www.q-net.or.kr/man001.do?gSite=L&gId=08
- Q-Net 기출문제: https://www.q-net.or.kr/cst003.do?id=cst00309&gSite=L&gId=08
- EBS 기출/답안: https://www.ebs.co.kr/land/examData/previous/30004650703?p=Yy5wYWdlPTEmYy5wYWdlU2l6ZT0yMCZzZWFyY2hLZXl3b3JkPSZzZWFyY2hDb25kaXRpb249
- Alpha School: https://alpha.school/
- 2 Hour Learning: https://2hourlearning.com/
- Khanmigo: https://www.khanmigo.ai/
- Synthesis Tutor: https://www.synthesis.com/tutor
- ALEKS: https://www.aleks.com/about_aleks
- MATHia: https://www.carnegielearning.com/solutions/math/mathia
- Riiid EdNet: https://arxiv.org/abs/1912.03072
- OpenAI Image Inputs: https://platform.openai.com/docs/guides/images
- OpenAI Structured Outputs: https://platform.openai.com/docs/guides/structured-outputs
- Google Cloud Vision OCR: https://cloud.google.com/vision/docs/ocr
- Retrieval Practice: https://www.retrievalpractice.org/why-it-works
- Dunlosky et al. 2013: https://doi.org/10.1177/1529100612453266
- Roediger & Karpicke 2006: https://doi.org/10.1111/j.1467-9280.2006.01693.x
- Gick & Holyoak 1983: https://doi.org/10.1016/0010-0285(83)90002-6
- Retrieval-Augmented Generation: https://arxiv.org/abs/2005.11401
- Bayesian Knowledge Tracing: https://doi.org/10.1007/BF01099821
- FSRS: https://github.com/open-spaced-repetition/fsrs4anki/wiki
- SuperMemo SM-2: https://www.supermemo.com/en/archives1990-2015/english/ol/sm2
- SuperMemo 20 rules: https://www.supermemo.com/en/blog/twenty-rules-of-formulating-knowledge
- Anki Manual: https://docs.ankiweb.net/
