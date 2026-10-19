# File templates

Use these exactly. Replace placeholders in angle brackets. Dates are YYYY-MM-DD.

---

## Session log: `context/sessions/YYYY-MM-DD-<slice>.md`

Create the file at the start of the session with the frontmatter and the "Interview" heading. Append one Q/A pair after every answer. Fill in the summary only at wrap-up.

```markdown
---
type: session-log
slice: <slice>
date: <YYYY-MM-DD>
status: in-progress
---

# <Slice> session, <YYYY-MM-DD>

Notes at start: <for example "no anchor note existed" or "resumed from 2026-10-14-customer">

## Interview

### Q1

<question exactly as asked>

**Answer:**

<answer exactly as typed by the user>

### Q2

<question>

**Answer:**

<answer>

## Parked for other slices

- <slice>: <short description>, see Q<n>

## Summary

- Topics covered: <list>
- New open questions: <OQ IDs>
- Answered open questions: <OQ IDs>
- Skipped: <Q numbers>
- Resume from: <only if paused>
```

At wrap-up, change `status` to `done`, or to `paused` if the user paused.

Use headings `### Q1`, `### Q2` and so on so that Obsidian links like `[[2026-10-21-customer#Q4]]` work.

---

## Slice note: `context/<slice>.md`

One per slice. Update it at every wrap-up; do not create a new one per session.

```markdown
---
type: context-slice
slice: <slice>
status: <not-started | in-progress | done>
last_session: <YYYY-MM-DD>
sessions:
  - "[[<YYYY-MM-DD>-<slice>]]"
---

# <Slice> context

## <Topic name from slices.md>

State: <covered | open question | not applicable | not yet discussed>

- <statement in clean form> (<known | believed | guessed>, [[<session>#Q<n>]])
- Open: [[open-questions#OQ-<nnn>]]

## <Next topic>

...

## Contradictions

- <what conflicts with what>, [[<session>#Q<n>]] vs [[<session or anchor>]]

## Not applicable

- <topic>: <reason given by the user>, [[<session>#Q<n>]]
```

Rules:
- The confidence tag is optional. Add it only where you asked for it, or where the user volunteered it.
- When a newer session changes a statement, replace it and keep the link to the newer source. The old answer stays in the old session log.

---

## Open questions: `context/open-questions.md`

```markdown
---
type: open-questions
---

# Open questions

## OQ-001

- Question: <question as a full sentence>
- Slice: [[<slice>]]
- Raised: <YYYY-MM-DD>, [[<session>#Q<n>]]
- Can answer: <role or person>
- Impact: <what decision or design choice depends on this>
- Status: open
- Answer:
- Answered:
```

When answered, set `Status: answered`, put the answer in `Answer:`, and the date and session link in `Answered:`. New questions go at the end of the file.

Keep each heading to the bare ID (`## OQ-001`), with the question on the first line below it. Obsidian heading links need the full heading text, so this keeps links like `[[open-questions#OQ-001]]` stable.
