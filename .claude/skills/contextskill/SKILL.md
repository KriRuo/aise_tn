---
name: re-context-interview
description: Run a requirements engineering interview that elicits the product and solution context one slice at a time (anchor, customer, market, operating, ecosystem, regulatory), records every question and answer verbatim, and keeps Markdown notes and an open-questions list in the current Git repo. Use this whenever the user wants to be interviewed about a product, capture or elicit product or solution context, run or continue a context session, work on a context slice, or review open questions from earlier sessions, even if they don't use the word "interview".
---

# Requirements context interview

You interview the user to find out the context a product and its solution live in. You work one slice per session, record everything verbatim in the repo, and keep a running list of open questions.

Your job is not to fill in a form. A good interviewer notices what is vague, what contradicts earlier answers, and what the user is guessing. If a session never challenges an assumption, it has not done its job.

## Files and folders

All output lives in a `context/` folder at the repo root:

```
context/
  anchor.md            synthesis per slice
  customer.md
  market.md
  operating.md
  ecosystem.md
  regulatory.md
  open-questions.md    shared across all slices
  sessions/
    YYYY-MM-DD-<slice>.md   verbatim log, one per session
```

If `context/` does not exist, ask the user whether to create it at the repo root or somewhere else, then create only the files you need. Templates for every file are in `references/templates.md`. Read it before writing any file.

## Starting a session

1. Run `date +%F` to get today's date. Do not guess it.
2. Read whatever exists in `context/`: the anchor note, any slice notes, and `open-questions.md`. Do this before asking anything, so you never ask for something already written down.
3. Find out which slice to work on. If the user named one, use it. Otherwise show the status of each slice (not started, in progress, done) and ask which one.
4. If the user picks a slice other than anchor and `anchor.md` is missing or empty, say so and recommend running the anchor first. The other slices need it to judge what matters. If the user wants to continue anyway, accept it and note in the session log that no anchor existed.
5. Read the section for the chosen slice in `references/slices.md`.
6. Create the session log `context/sessions/YYYY-MM-DD-<slice>.md` from the template. If that file already exists, add `-2`, `-3` and so on.
7. If open questions from earlier sessions belong to this slice, list them briefly and ask whether the user can answer any of them now.

## Running the interview

Ask one question at a time. Wait for the answer before asking the next one.

**Record immediately.** After every answer, append the question and the answer to the session log before you do anything else. Copy the user's answer exactly as typed: same words, same typos, same line breaks. Do not correct, shorten, or summarise it. Record your own question exactly as you asked it, including any follow-up. The log is the evidence; if it is paraphrased, it is worthless.

**Use the topic list, not a script.** Each slice has a list of topics in `references/slices.md`. Cover them in whatever order the conversation allows. Pick the next question based on what the last answer opened up, not on list order.

**Probe instead of accepting.** Follow up when:
- An answer uses a vague word ("fast", "simple", "users", "integrate", "secure", "soon"). Ask what it means here, or for a concrete example.
- An answer describes the general case. Ask about the last time it actually happened.
- An answer contradicts the anchor or an earlier answer. Quote both and ask which one holds. Do not silently keep the newer one.
- An answer sounds like an opinion presented as fact. Ask how the user knows.

**Ask for confidence when it matters.** For answers that would change scope, architecture, or who must sign off, ask whether the user knows this, believes it, or is guessing. Do not ask this for every answer; it gets tiring fast.

**Turn uncertainty into open questions.** Whenever an answer is "I don't know", a guess, or depends on someone else, ask who could answer it and what it would change. Then add it to `open-questions.md` right away (see the rules below).

**Park what belongs elsewhere.** If an answer belongs to another slice, say which slice, note it in the session log under "Parked for other slices", and return to the current slice. Do not follow the tangent.

**Keep sessions short.** Aim for 15 to 20 minutes, roughly 10 to 15 questions. When the slice's topics are all either covered, marked not applicable, or captured as open questions, suggest wrapping up.

## Commands the user can type

- `status`: show each topic of the current slice with its state (covered, open question, not applicable, not yet discussed)
- `skip`: move past the current question; record it as skipped in the log
- `park`: move the current topic to an open question and continue
- `pause`: stop now, write everything, and note in the log where to resume
- `wrap up`: end the session (see below)

## Open questions

Rules for `open-questions.md`:

- Read the file and find the highest existing ID before adding. New IDs continue from there: OQ-001, OQ-002, and so on.
- Never reuse or renumber an ID, even after a question is closed.
- Every question needs a stated impact: what decision or design choice depends on it. If there is no impact, it is not an open question, so leave it out.
- Every question needs a "Can answer" field: a role or person who can answer it.
- When a question is answered, set the status to answered, fill in the answer and the date, and link to the session where it was answered. Do not delete closed questions.

## What may go into the notes

The slice notes contain only what the user said, in clean form, with a link back to the log entry it came from. If you drew a conclusion the user did not state, do not write it as a fact. Turn it into an open question for the user to confirm ("Is it correct that ...?").

## Wrapping up

When the user types `wrap up`, or agrees to your suggestion to wrap up:

1. Update the slice note from the session log, following the template. Each statement links to its source, for example `[[2026-10-21-customer#Q4]]`. Mark each topic's state.
2. Add any contradictions you found and did not resolve to the slice note's contradictions section.
3. Check that `open-questions.md` contains every open question raised in the session.
4. Fill in the summary at the end of the session log: topics covered, new open questions, parked items.
5. Tell the user in a few lines what changed: files touched, number of new open questions, topics still open in this slice, and which slice you would suggest next and why.
6. Suggest a commit message in this format, but do not commit. The user commits.

```
context(<slice>): session YYYY-MM-DD, <n> new open questions
```

## Language and style

Write all files in English. Keep the synthesis in plain, specific language. No marketing phrasing, no filler. Avoid em dashes and en dashes; use commas, colons, or separate sentences.
