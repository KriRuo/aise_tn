# Context slices

Read only the section for the slice you are running. Each section has:

- **Purpose**: what this slice is for
- **Belongs elsewhere**: what to park for another slice
- **Topics**: what must be covered, each tracked as a state in the slice note
- **Starting questions**: examples, not a script. Adapt them to the product.
- **Crucial when**: what makes information in this slice important enough to dig into
- **Quick exit**: when the whole slice can be marked not applicable

Contents: Anchor, Customer, Market, Operating, Ecosystem, Regulatory

---

## Anchor

**Purpose:** Establish what the product is for, so every other slice can judge what matters. Keep it short, about 10 minutes.

**Belongs elsewhere:** Details about users (customer), competitors (market), systems (ecosystem), laws (regulatory).

**Topics:**
- Problem: what is wrong today, and for whom
- Goals: what changes if this succeeds, and how anyone would notice
- Scope statement: one or two sentences on what the product does, plus anything explicitly out
- Key stakeholders: who decides, who pays, who uses, who can block
- Phase: idea, discovery, in development, live and being extended

**Starting questions:**
- What happens today, without this product, that someone wants to change?
- If this goes live and works, what is different six months later?
- Who can stop this project?

**Crucial when:** A goal cannot be observed or measured, or two stakeholders want different outcomes.

**Quick exit:** None. The anchor is always needed.

---

## Customer

**Purpose:** Understand the people the product serves, and how they work today.

**Belongs elsewhere:** Competing products (market), internal operations and support (operating).

**Topics:**
- Customer groups: who uses, who buys, who benefits, and whether these are different people
- Current way of working: tools, workarounds, frequency, volume
- Pain points, with real examples
- What the customers would have to change to use the product
- Access: can the team actually talk to real customers, and who controls that access

**Starting questions:**
- Walk me through the last time a user did this task. What did they use?
- Who decides to buy or adopt this, and is that the same person who uses it?
- What would a user have to stop doing, or learn, to use the new product?

**Crucial when:** The buyer and the user differ, or the product assumes a way of working customers don't have today.

**Quick exit:** Rarely. Even internal tools have users. Only skip if the anchor says the product has no human users.

---

## Market

**Purpose:** Understand why someone would choose this product over the alternatives, including doing nothing.

**Belongs elsewhere:** Individual user behaviour (customer), integration with other products (ecosystem).

**Topics:**
- Alternatives the customer has today, including spreadsheets, manual work, or doing nothing
- Competitors and how the product differs from them
- Pricing or business model, and any pressure on it
- Timing: what makes now the right moment, or a deadline driven by the market
- Reasons the product could fail commercially

**Starting questions:**
- If this product didn't exist, what would customers use instead?
- Why would someone switch to this from what they use today?
- What would have to be true for this not to be worth building?

**Crucial when:** The reason to switch is unclear, or the timing depends on something outside the team's control.

**Quick exit:** Internal systems with no buyer choice, for example a mandated in-house tool. Record the reason, and ask once whether users could ignore the tool and keep their old way of working. If yes, that is a market question after all.

---

## Operating

**Purpose:** Understand how the solution will run once it is live, and what in the organisation constrains that.

**Belongs elsewhere:** External systems and data exchange (ecosystem), laws and standards (regulatory).

**Topics:**
- Who operates, supports, and maintains the solution after go-live
- Business processes the solution changes, and who owns those processes
- Hosting and environment limits, for example cloud not allowed, air-gapped, on-site only
- Rollout: how users get access, training, migration from the old way
- Budget and running cost, and who pays
- Availability and support hours expected by the business

**Starting questions:**
- After go-live, who gets the call when something breaks?
- Which existing process changes because of this, and who owns that process?
- Are there limits on where this can run or what it may connect to?

**Crucial when:** Nobody owns operations yet, or the environment rules out an obvious technical approach.

**Quick exit:** None for products that will go live. For throwaway prototypes, record that and keep only hosting limits.

---

## Ecosystem

**Purpose:** Map what lies around the system: neighbouring systems, data sources and receivers, partners, platforms. This is where the IREB system boundary and context boundary are drawn, and the grey zone between them is the main focus.

**Belongs elsewhere:** Internal operations (operating), legal requirements on data (regulatory).

**Topics:**
- Neighbouring systems: what sends data in, what receives data out
- Owner of each neighbouring system, and how cooperative they are
- Key business data: what it is, where it comes from, who owns it
- Platform or vendor dependencies
- Partners or third parties involved in delivering the product
- Grey zone: things nobody has decided are in or out of scope

**Starting questions:**
- Where does the data this product needs come from today?
- Which of these systems does your team not control? Who does?
- Is there anything you assume someone else will build or change for this to work?

**Crucial when:** A dependency is outside the team's control, or data ownership is unclear.

**Quick exit:** Only for fully standalone tools with no data exchange. Ask twice before accepting this; it is rarely true.

---

## Regulatory

**Purpose:** Find the hard constraints from laws, standards, and compliance rules.

**Belongs elsewhere:** Internal process rules that are not compliance-driven (operating).

**Topics:**
- Applicable laws and regulations, for example data protection, industry rules
- Standards and certifications required or expected
- Personal or sensitive data handled, and where it may be stored
- Internal compliance policies, for example security, records retention
- Who is accountable for compliance, and who signs off
- Audit and evidence obligations

**Starting questions:**
- Does the product store or process personal data? Whose, and where?
- Is there any certification or audit the product, or the client, has to pass?
- Who in the organisation would have to approve this before it goes live?

**Crucial when:** A rule would change the architecture or scope, or nobody knows who is accountable. If the user is unsure whether a law applies, do not answer it yourself; record it as an open question for a compliance or legal role.

**Quick exit:** Rarely appropriate. If the user says nothing applies, ask about personal data and internal security policy before accepting.
