Context: Act as a senior requirements engineer. The Torqvoice repository is open.
Task: Reconstruct the as-is process "vehicle drop-off to invoice" from the code.
Output:
1. BPMN 2.0 XML in process/as-is-repair-order.bpmn, one pool, one lane per role
   found in the code. Task names: verb + object. Include the BPMNDiagram section.
2. Step table: Step ID | Lane | Task | Source (file:line) | Confidence (High/Med/Low)
3. Max 8 candidate user stories: "As a <role from the code>, I want ..., so that ..."
   plus source step ID plus one open question for the stakeholder.
Rules: No step without a source. Anything inferred and not seen in code is Low and
goes to a list "To confirm with stakeholder". Do not invent roles.
