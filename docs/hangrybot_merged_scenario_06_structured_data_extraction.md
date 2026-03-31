# HangryBot Merged Scenario 6: Structured Data Extraction

## Why this merged scenario exists

This scenario rewrites the exam’s **Structured Data Extraction** setup into HangryBot’s world and merges in the earlier HangryBot materials on:

- structured extraction for catering and incident intake
- JSON-schema-based tool use
- validation and retry loops
- optional and nullable schema design
- context management for messy source documents
- human review and escalation for low-confidence cases

It is the scenario where operational messiness becomes machine-usable structure.

---

## HangryBot production context

Every day, HangryBot receives unstructured data that the rest of the platform depends on:

- PDK FBO catering requests sent as emails or forwarded notes
- ATL terminal incident summaries written by shift leads
- support escalations copied from chat and phone transcripts
- partner menu updates in free text or attached documents
- vendor service interruptions described in inconsistent formats

Sophia needs these records normalized before operations start. Emma needs clean labels and structured facts for analysis. Ryan needs searchable case summaries. Downstream systems need predictable objects, not free-form prose.

That makes HangryBot an ideal case for a **structured extraction pipeline**.

---

## What needs to be extracted

Depending on document type, HangryBot may need fields such as:

### Catering request
- partner or FBO name
- airport and location
- flight identifier if present
- requested delivery time
- passenger or crew count
- dietary constraints
- bundle type
- special handling notes

### Incident summary
- airport and service mode
- incident type
- start and end times
- affected orders or routes
- likely root cause
- severity
- systems involved
- whether compensation review is required

### Support escalation
- customer or partner identifier if present
- order number
- issue category
- amount disputed
- requested outcome
- whether the customer asked for a human
- evidence excerpts

Not every document will contain every field. That is why the schema must support **optional or nullable fields** rather than forcing the model to invent missing values.

---

## Tool-use and schema strategy

A strong extraction design uses **tool use with JSON schemas**, not plain-text JSON guessing.

For HangryBot, you might define multiple extraction tools such as:

- `extract_catering_request`
- `extract_incident_report`
- `extract_support_escalation`
- `extract_menu_update`

If the document type is unknown, set tool choice so the model must call *a* tool. If the type is known, force the specific schema first.

Strong schema design patterns include:

- nullable fields for genuinely absent data
- enums with `other` plus a detail field
- an `unclear` category for ambiguous cases
- evidence fields or excerpts for traceability
- conflict flags when the source contains inconsistent facts

This avoids the common failure mode where required fields cause the model to fabricate content.

---

## Validation and retry loops

This scenario is also about what happens *after* extraction.

A strong HangryBot pipeline performs at least two kinds of validation:

### Schema validation
This checks whether the output matches the expected structure.

### Semantic validation
This checks whether the contents make sense, such as:

- does the requested headcount match the stated bundle quantity?
- is the extracted delivery time in a valid format?
- does the disputed amount match the quoted total?
- are airport and location values internally consistent?

When validation fails and the source likely contains the answer, the retry should include:

- the original document
- the failed extraction
- the specific validation errors

That is better than simply “please try again.”

But the pipeline should also know when **retry will not help**. If the email never states the passenger count, repeated extraction attempts will not magically produce it.

---

## Batch processing and throughput

HangryBot is a good place to study **Message Batches API** because many extraction jobs are not interactive.

Good batch candidates include:

- nightly processing of incident summaries
- weekly normalization of archived support transcripts
- large partner document backfills
- menu and vendor update ingestion

Each request should include a stable correlation identifier so failed items can be retried selectively. Batch processing is great for cost-sensitive, latency-tolerant workloads, but not for workflows that must block operations in real time.

For urgent same-shift documents, HangryBot should still use synchronous extraction.

---

## Context management during extraction

Unstructured documents are often long, repetitive, and inconsistent. This scenario should preserve the earlier HangryBot context-management lessons.

Good extraction systems do not just shove entire documents into a prompt and hope for the best. They may:

- segment large documents intelligently
- preserve section headers and local context
- keep source metadata such as filename, date, and page number
- retain evidence snippets linked to extracted fields
- use scratchpad or intermediate representations when multiple passes are required

This is particularly important when the same incident is described across several pages or when important details appear in the middle of the document.

---

## Human review and escalation

Not every extraction should flow straight into downstream systems.

HangryBot should route items to human review when:

- the source is contradictory
- critical required business fields are missing
- confidence is low
- multiple plausible interpretations exist
- the extracted object would trigger compensation, premium catering, or contractual commitments

The review queue should prioritize the most consequential low-confidence items first. That is a better use of human time than random spot checks.

---

## Common exam traps in this scenario

Weak answers often:

- require every field even when the source may not contain it
- rely on plain text responses instead of tool-use schemas
- retry without telling the model what failed
- treat schema validity as proof of semantic correctness
- use batch APIs for time-sensitive operational flows
- drop source attribution and evidence snippets
- ignore human-review routing for ambiguous or high-impact documents

Strong answers emphasize:

- JSON-schema-based tool use
- optional and nullable fields
- semantic plus structural validation
- retry-with-error-feedback
- selective batch usage
- evidence preservation and source metadata
- confidence-based human review

---

## What a strong HangryBot solution looks like

The finished pipeline turns messy real-world inputs into structured records that operations, support, analytics, and training systems can trust. It extracts only what the document actually supports, preserves evidence, retries intelligently when fixable, and escalates the right items to humans instead of forcing certainty where none exists.

That is why this scenario is so important: **good extraction is not just about getting JSON. It is about getting reliable operational truth from messy text without fabricating confidence**.
