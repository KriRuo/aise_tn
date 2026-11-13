---
name: jira-user-story-writer-v2
description: Turn short chat notes or bullet points into a concise, Jira-ready user story in English, with a fixed template, numbered acceptance criteria in an ISO 29148 sentence pattern that state intent and leave the solution to the team, and an optional lo-fi HTML prototype for new UI elements. Use this whenever the user describes a requirement, change request or feature idea informally and wants a story, ticket or backlog item out of it, for example "write a story for", "turn this into a ticket" or "make this Jira-ready", even if they never say "user story". The skill checks the repository first, then asks numbered clarification questions, and only then drafts.
---

# Jira user story writer (v2)

Turn rough requirement notes into a story that a team can refine without a second round of basic questions.

## Principle: state the intent, leave the solution open

A story fixes **what must be true and why**. It does not fix how the screen looks, how the feature is built, or what the texts say. The team decides those during refinement and implementation, and that room is what makes the story negotiable.

- Write what the role can do or what Torqvoice guarantees, not how the interface achieves it.
- Only decisions the author actually made become criteria. Everything else is left open or listed as a suggestion.
- When in doubt, write the criterion one level more abstract.

The skill runs inside a repository (for example a GitHub Codespace). That is its main advantage over a plain chat: it can look at the existing application before it asks anything, so its questions refer to what is really there.

## Project context

Adjust this block when the skill is used for another product.

- System name: `Torqvoice`
- Known roles: `Workshop Manager`, `Technician`. Check the repository for further roles before using any other name.
- Use the terms found in the code and UI (entity names, field labels, screen names). Do not invent synonyms.

## Workflow

1. **Read the notes.** Identify the actor, the requested behaviour, the business value, and the data, rules and screens that are probably affected.
2. **Check the repository.** Search for the entities, screens and roles the notes mention. Note what already exists: fields, validations, permissions, places where the data is shown (lists, detail views, search, exports, printed documents). Keep this short, a few targeted searches are enough. If the workspace contains no application code, skip this step and say so in one line.
3. **Ask clarification questions and stop.** See the rules below. Do not draft the story in the same reply.
4. **Draft the story** from the answers, using the template.
5. **Check the draft** against the review checklist and fix what fails.
6. **Save the results.** Show the story in the chat and save it. If the story adds UI, offer a lo-fi prototype instead of creating it.

## Clarification questions

Always ask before drafting, also when the notes look complete. The point is that the author confirms the decisions a developer would otherwise make silently.

- Output the heading `#### Clarification questions`, then a numbered list, so the user can answer by number.
- Ask at most seven questions. Each one is short and can be answered in a few words.
- Do not ask what the notes already answer. If the notes cover almost everything, ask the user to confirm the two or three assumptions that carry the most risk.
- Ground the questions in the repository where possible. Name what you found, for example: "Customer search currently covers name and e-mail. Should the new field be searchable too?"
- Include one question that tests the request itself when you see a reason: a simpler alternative, a conflict with existing behaviour, or a story that looks too large. Leave it out when there is no real reason.
- Include one question that separates what is fixed from what the team may decide, for example: "Which of these are business rules, and which may the team decide?"

Topics to pick from, only where relevant. Ask for the business rule or intent, not for the implementation detail:

- Actor and permissions: who may see, create, change and delete?
- Information: what information is needed, and what is mandatory from a business point of view?
- Rules: limits, calculations, status dependencies, uniqueness, and whether each is a fixed rule or an adjustable setting?
- Failure and empty cases: what must the user be able to do or know when there is no data or the action fails?
- Other surfaces: does the change also appear in lists, search, exports, printed documents or notifications?
- Existing data: what happens to records created before the change?
- Scope: what is explicitly not part of this story?

If blocking information is still missing after the answers, ask only the remaining blocking questions. Everything else becomes an assumption in the story.

## Sorting the answers

Sort every answer into one of three groups before drafting:

- **Rule:** a business decision that must hold. It becomes an acceptance criterion.
- **Suggestion:** a value or choice the author mentioned but did not commit to (a number, a field list, a default). It goes under `Assumptions and open points` as "suggested: ...".
- **Open:** a detail nobody decided (wording, layout, field order, control types). It goes under `Left to the team`, or is simply omitted.

## Output template

Use exactly this structure. A fixed structure lets the team scan every story the same way and paste it into Jira without rework.

```
#### Title
[Short summary for the Jira summary field, at most 10 words]

#### Story
As a [role] I want [capability] so that [benefit].

#### Acceptance Criteria
1. [acceptance criterion]
2. [acceptance criterion]

#### Assumptions and open points
- [assumption, suggested value or open point]

#### Left to the team
- [detail deliberately not decided, for example wording, layout]

#### Follow-up stories
- [surface]: [one-line summary]
```

- `Assumptions and open points` appears only when there are any. Never hide an assumption inside an acceptance criterion. Suggested values are written as "suggested: ...".
- `Left to the team` appears only when it adds information, for example "Message wording and layout".
- `Follow-up stories` appears only when the user confirmed that further surfaces are affected, or when the story was split.
- Add no commentary before or after the story, apart from the file paths at the end.

## Story rules

- Write in English and keep it short.
- One story covers one vertical slice: one role, one goal, usable on its own.
- The benefit after "so that" names a real outcome for the role, not a restatement of the capability.
- Describe behaviour, not implementation. Mention tables, endpoints or components only if the user asked for that.
- Describe outcomes, not interface mechanics. No buttons, dropdowns, colours, field order or layout.
- Apply INVEST as a check, not as a label:
  - **Independent and small:** if the story needs more than one role or goal, or more than about six acceptance criteria, propose a split. Write the first slice in full and list the rest under `Follow-up stories`.
  - **Valuable:** if you cannot state a benefit, ask for it instead of inventing one.
  - **Estimable and testable:** every open point that would change the effort is listed under `Assumptions and open points`.
  - **Negotiable:** leave the solution open where the user did not decide it.

## Acceptance criteria rules

Write a plain numbered list without subheadings.

Use the sentence pattern from ISO/IEC/IEEE 29148:

`[<condition>] <subject> <action> <object> [<constraint>]`

The standard writes requirements with "shall". Acceptance criteria here describe observable behaviour to be tested, so they use the present tense without modal verbs: `Torqvoice displays the link`, not `Torqvoice shall display the link`.

- Start with `If`, `When` or `Unless` when a condition exists.
- Name the subject explicitly: a role or `Torqvoice`. Avoid "the system" and "the user".
- One observable outcome per criterion. Split sentences that contain "and" between two unrelated behaviours.
- State a concrete value only when the author confirmed it as a business rule (a legal limit, a fixed status name). Otherwise refer to the rule ("within the booking window set by the workshop") and put the suggested value under `Assumptions and open points`.
- Describe messages by purpose ("informs the Customer that the slot is taken"), not by literal text. Use literal text only when the author supplied it or it is legally required.
- Describe validation by effect ("prevents saving an incomplete note"), not by control behaviour ("disables the save button").
- Group related failure cases into one criterion when the required outcome is the same, for example "If the booking cannot be completed, Torqvoice creates no booking, tells the Customer why and points to an alternative."
- Order: main flow first, then alternative and error flows, then end states (what is stored or changed afterwards).
- Cover validation, permissions, empty states and error states where they apply, at the level of outcome.

Weak, too vague, and better:

| Weak (vague) | Too specific | Better (intent) |
|---|---|---|
| The note field should be validated properly. | If the Technician enters more than 500 characters, Torqvoice shows "Max. 500 characters" in red under the field and disables the Save button. | If a note exceeds the maximum length, Torqvoice prevents saving it and tells the Technician how to correct it. |
| Users can manage notes. | When the Technician clicks the "+" icon, Torqvoice opens a modal with a textarea. | When the Technician adds a note, Torqvoice stores it with author and time. |
| The note is not visible to customers. | Torqvoice removes the note from the invoice PDF and from the customer portal page "Service history". | Torqvoice keeps internal notes out of everything the customer sees. |

## Review checklist

Check silently before the final answer and correct the draft where needed:

- Every answer the user gave is reflected in a criterion or an assumption.
- Criteria are ordered as main flow, alternative and error flows, end states.
- Each criterion has one subject, one action and a result that a tester can observe.
- No modal verbs, no vague words ("properly", "user-friendly", "fast", "etc.").
- No criterion contains literal UI text, interface elements (button, dropdown, field order, colour) or numbers the author did not confirm as rules.
- Every concrete value in a criterion traces back to a Rule from the answers. Suggestions are under `Assumptions and open points`.
- A developer could implement each criterion in more than one way. If only one implementation fits, rewrite it more abstractly.
- Terms match the repository and the project context.
- The story is one slice. If not, it has been split.

## Saving the results

- Show the story in the chat so it can be copied into Jira.
- Save it as `stories/<short-slug>.md`.
- If the story introduces new UI, do not create a prototype automatically. End the reply by offering one ("Want a lo-fi sketch?"). Create it only when the user says yes.
- When asked, save the prototype as `prototypes/<short-slug>.html` instead of pasting the code into the chat. A file can be opened in the browser preview.
- End the reply with the paths of the saved files.

Prototype rules:

- A prototype is an illustration, not a specification. Put the line "Illustrative only – layout and wording are up to the team" at the top of the page.
- One self-contained HTML file with minimal inline CSS, monochrome, no external resources.
- Show only the essential information and actions, in a plain layout. No pixel-level or styling decisions.
- Use placeholder text such as [message: slot no longer available] instead of final wording.
- Show the main states side by side, for example empty, filled and error.
- No JavaScript, unless a few lines are needed to show a core state change.

## Worked example

User notes:

> technicians should be able to leave an internal note on a service record. customer must not see it.

First reply:

```
#### Clarification questions
1. Service records already have a public "Description" field that prints on the invoice. Is the internal note a separate field?
2. Who may read internal notes: all Technicians and Workshop Managers, or only the author?
3. May a note be edited or deleted after saving, and by whom?
4. Is there a maximum length?
5. Should internal notes be found by the service record search?
6. One note per service record, or several with author and time?
```

After the user answered (separate field, all staff read, only the author edits, 500 characters, not searchable, several notes):

```
#### Title
Internal notes on service records

#### Story
As a Technician I want to add internal notes to a service record so that colleagues know what I found without the customer seeing it.

#### Acceptance Criteria
1. When the Technician opens a service record, Torqvoice shows the internal notes of that record, most recent first.
2. When the Technician adds a note, Torqvoice stores it with author and time.
3. If a note is empty or exceeds the maximum length, Torqvoice prevents saving it and tells the Technician why.
4. Unless the signed-in user is the author, Torqvoice prevents changing the note.
5. Torqvoice keeps internal notes out of everything the customer sees, including invoices.
6. Torqvoice keeps internal notes out of the service record search.

#### Assumptions and open points
- Suggested maximum length: 500 characters.
- Deleting notes is not part of this story.

#### Left to the team
- Wording of messages, placement and layout of the notes.

Saved: stories/internal-notes-service-record.md
Want a lo-fi sketch of the notes area?
```
