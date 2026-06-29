# Subject Selectors

Selectors choose existing past-exam `question_id`s for reissue. They do not generate new questions.

## Common Inputs

- source question ID
- subject
- chapter
- micro-skill
- trap
- first principle
- previous reissue result
- response time
- confidence
- lapse count
- overdue status

## Common Outputs

- 1-5 existing `question_id`s for reissue
- selection reason
- selector version
- rollback note

## Subject Rules

| Subject | Selector | Priority Signal |
|---|---|---|
| 부동산학개론 | calculation/frequent-concept selector | score-source item, same calculation type, formula trap, slow response, high-frequency concept |
| 민법 | requirement/judgment/similar-case selector | first-exam defense item, same legal requirement, exception, third-party effect, invalid/cancel distinction |
| 중개사법 | number/party/penalty selector | high-score item, same number, period, actor, sanction, registration duty |
| 공법 | structure/failure-prevention selector | floor-defense item, same permission authority, process, exception, high-frequency low-score area |
| 공시법 | procedure/effect comparison selector | maintenance item, same procedure order, registration effect, public record comparison |
| 세법 | tax-type/deadline/calculation selector | maintenance item, same tax type, deadline, rate, taxable object, calculation pattern |

## Strategy Roles

Selector choice must support the 300-hour score plan.

- `민법 first-exam defense`: choose items that train legal requirement judgment and similar-case discrimination. Keep 민법 inside its weekly min/max guardrail even when another subject has more visible wrong answers.
- `부동산학개론 score-source`: favor calculation, finance, economics, and frequent concepts that can move the subject toward 70+.
- `중개사법 high-score`: favor numbers, periods, actors, sanctions, and registration duties that can produce fast repeatable points toward 75+.
- `공법 floor-defense`: favor high-frequency structure questions that protect the 40-point floor before expanding into low-yield detail.
- `공시법/세법 maintenance`: favor procedure order, deadlines, taxable objects, rates, and common calculation patterns. Maintain 55-65 combined; avoid deep expansion while first-exam risk is unresolved.

When two selectors compete, choose the one that protects the nearest hard gate. Week 8 first-exam risk overrides second-exam expansion.

## Escalation Rules

Use a harder or wider selector when:

- the same trap repeats
- confidence stays low after correct answers
- response time remains slow
- the learner can answer the original item but fails similar cases

Use an easier or narrower selector when:

- the learner repeatedly fails before understanding the basic rule
- overdue debt is growing
- the selector produces too many `rebuild` items

## Versioning

When changing selector behavior:

1. Log the old selector version.
2. Apply the new version as a shadow or limited test.
3. Compare repeated wrong rate, response time, confidence, and overdue growth.
4. Promote only if performance improves without increasing debt.
5. Roll back if repeated wrong rate or debt worsens.

## Bad Selector Smells

- It picks questions because keywords match but legal structure differs.
- It only chooses easy items and creates false mastery.
- It chooses very hard items and turns review into explanation reading.
- It ignores old-law risk.
- It fails to connect repeated traps across years.
