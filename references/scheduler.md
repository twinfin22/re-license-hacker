# Scheduler

## Review Philosophy

Wrong answers should not be stored passively. They become debt until the learner can answer existing past-exam items correctly, quickly, and with confidence.

## Base Interval

Use this simple schedule until there is enough real data to tune it:

```text
same day retry -> D+1 -> D+3 -> D+7 -> D+14 -> D+30
```

If the user gets the item wrong, reset to same-day retry and then D+1.

## Statuses

- `learning`: new item or recently reset item
- `fragile`: correct but slow, low-confidence, guessed, or unstable
- `mastered`: three spaced successes and no recent lapse
- `lapsed`: wrong, hint needed, or "I knew it" after seeing the answer
- `rebuild`: three or more lapses, bad tag, or bad selector choice

## Mastery Criteria

Mark an item `mastered` only when all are true:

- D+1, D+3, and D+7 are correct
- response time is 60-90 seconds or less
- confidence is 4/5 or higher
- no lapse in the last 14 days
- estimated recall is at least 90%

Keep mastered items in a low-frequency monitoring queue until the exam.

## Micro-Skill Mastery

Mark a micro-skill mastered only when:

- at least 4 of 5 similar existing past questions are correct
- success happens across at least two separate sessions
- the same mistake type does not recur

## Review Debt

Estimate review debt as the sum of due and overdue item minutes.

Suggested minute estimates:

- normal due item: 3 minutes
- fragile item: 5 minutes
- lapsed item: 7 minutes
- rebuild item: 10-15 minutes

Lock new study when:

- total estimated review debt is over 60 minutes
- more than 10 high-priority micro-skills are overdue
- 민법 or 중개사법 has a core lapsed item that has not been handled

## Rebuild Trigger

When `lapse_count >= 3`, do not keep repeating the same item blindly. Mark `rebuild` and inspect:

- Was the micro-skill too broad?
- Was the micro-skill too narrow?
- Was the selected reissue question too easy or too hard?
- Is there an unhandled first-principle gap?
- Is the source question affected by old law or bad matching?
