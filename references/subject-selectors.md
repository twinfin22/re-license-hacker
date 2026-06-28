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
| 부동산학개론 | calculation/frequent-concept selector | same calculation type, formula trap, slow response |
| 민법 | requirement/judgment/similar-case selector | same legal requirement, exception, third-party effect, invalid/cancel distinction |
| 중개사법 | number/party/penalty selector | same number, period, actor, sanction, registration duty |
| 공법 | structure/failure-prevention selector | same permission authority, process, exception, high-frequency low-score area |
| 공시법 | procedure/effect comparison selector | same procedure order, registration effect, public record comparison |
| 세법 | tax-type/deadline/calculation selector | same tax type, deadline, rate, taxable object, calculation pattern |

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
