# Pitch Deck MCP — Design and Editorial Reference

Version: 0.1 · 6 November 2026  
Context: UJIStartup Bootcamp 2026  
Status: research and implementation proposal; no MCP server has been implemented, installed, or deployed.

## Purpose

Give a team working with different AI applications a common, versioned method for explaining a venture concisely, checking its claims, and preparing a pitch deck. Preserve freedom over voice, brand, language, and slide composition.

The server would distribute the method and run explicit checks. The connected AI would interpret the venture, propose language, and discuss editorial choices. Shared rules improve consistency; they do not guarantee identical text, visual rendering, or evaluator approval.

## Source and review coverage

Reference: [PowerPrompt · Senda](https://senda.partners/powerprompt), attributed on the page to Nacho Sánchez. Correction prompts are signed “Skynet 4.8”. Inspected interactively on 6 November 2026 through the page's normal navigation and LinkedIn link. No LinkedIn follow or connection request was submitted.

All 15 sections were opened. For each, the initial slide, the correction-prompt stage, and the final-slide stage were inspected. The table below is a paraphrased analytical index, not a transcript or a reproduction of the slide assets.

| Section | Editorial lesson from the comparison |
| --- | --- |
| Cover | Explain the offering concretely; identify the presenter and date, and provide a relevant visual. |
| Problem | Identify the affected customer and connect the underlying cause with a sourced economic consequence. |
| Why now | Show a recent external change that enables or strengthens the opportunity; avoid repeating the problem. |
| Product | Make the actual product legible, select a few essential functions, and distinguish present capability from future vision. |
| How it works | Make the user journey and underlying mechanism understandable; distinguish proprietary work from standard components. |
| Value proposition | Translate the customer problem into a measurable improvement. |
| Business model | Explain the principal payment mechanism and what one customer contributes economically. |
| Market | Build an annual revenue estimate from customer segments and pricing, including a plausible initial niche. |
| Competitors | Compare meaningful alternatives across several relevant dimensions, using degrees and numbers where useful. |
| Go-to-market | Explain the team's specific route to customers and how it develops through successive phases. |
| Traction | Prefer evidence of adoption and business progress over attention metrics; show change over a defined period. |
| Roadmap | Link near-term product and commercial milestones to measurable outcomes and financing. |
| Team | Explain relevant execution ability through clear responsibilities and selected achievements. |
| Funding | Connect the requested capital, funding status, allocation, runway, and intended milestones. |
| Closing | Leave a recognizable identity and an easy way to make contact or take the next step. |

These are functions of a narrative, not a requirement to produce 15 slides. A short bootcamp pitch may merge or omit sections according to its brief.

## Critical interpretation

The source is an investor-oriented teaching example. Its example prices, customer counts, funding amounts, growth rates, and timelines are illustrative; none is evidence about the team's project.

The principles take precedence over incidental layouts. For example, a 24-month roadmap, three product functions, a six-block mechanism, monochrome styling, and a contact QR can be useful defaults without becoming universal constraints. A static deck should communicate without requiring a video to play; a live demo may still be appropriate when the event format permits it.

Some final examples retain generic or inconsistent material: the value slide still depicts a loss despite its benefit-oriented title, and the closing slide retains the generic slogan criticized in the cover example. The implementation should check the resulting message instead of assuming that every final example is a complete template.

## Proposed method

### 1. Establish the presentation contract

Record audience, intended decision, venture stage, language, live versus standalone format, available time, mandatory event requirements, and brand preferences. Ask only for information that changes the narrative or the validity of a claim.

A pitch seeking pilot customers needs a different final request from a fundraising deck. A pre-validation venture needs an honest validation plan rather than invented traction.

### 2. Maintain a claim register

Each material claim should have an identifier, statement, status, source reference, date or period, and owner. Numeric claims additionally need a value, unit, denominator where relevant, and calculation or measurement method.

Suggested statuses: `observed`, `reported`, `estimated`, `target`, `hypothesis`, and `unknown`.

- `observed` requires a supporting observation or measurement record.
- `reported` identifies the reporting person or source; it does not mean independently verified.
- `estimated` exposes assumptions and a calculation.
- `target` belongs to a future period and must be labelled accordingly.
- `hypothesis` remains a proposition to test.
- `unknown` creates a missing-information item rather than a fabricated figure.

The tool can detect missing metadata or arithmetic conflicts. It cannot establish the truth of an external source merely because a citation field is populated.

### 3. Build the narrative before rendering slides

For each proposed slide, record:

- Its purpose and the audience question it answers.
- One principal takeaway and its evidence references.
- The essential visible copy, separated from speaker notes and appendix detail.
- A visual brief explaining what the visual must demonstrate.
- Any unresolved question or dependency.

Conciseness must preserve qualifications that change meaning. Move supporting detail into notes or an appendix when possible; never shorten “pilot planned” into “pilot secured”.

### 4. Review in two complementary ways

**Mechanical checks** can validate required fields, configurable copy budgets, evidence references, numeric units, totals, dates, and cross-slide use of canonical figures. Examples include annual price versus monthly price, market arithmetic, funding allocation totals, and conflicting customer counts for the same period.

**Editorial review** evaluates clarity, relevance, credibility, causal connections, meaningful differentiation, and fit to the audience. The connected AI should explain its judgments and propose revisions. These judgments should not be represented as objective or investor-predictive scores.

### 5. Render and verify separately

The first implementation should produce a stable deck specification, readable Markdown, speaker notes, and a review report. Producing a deck in PowerPoint, Google Slides, Canva, or another renderer is a separate adapter.

Rendered output needs a visual inspection for text overflow, contrast, hierarchy, chart readability, citations, and working links or QR destinations. Text validation alone cannot certify the appearance of a deck.

## MCP interface proposal

MCP supports resources, prompts, and tools. The proposed split follows the [official server concepts](https://modelcontextprotocol.io/docs/learn/server-concepts) and [architecture overview](https://modelcontextprotocol.io/docs/learn/architecture), checked on 6 November 2026. Implementation must select SDK and protocol support against the actual target clients before claiming compatibility.

| Interface | Proposed responsibility |
| --- | --- |
| Resources | Versioned editorial method, section criteria, claim and slide schemas, and optional visual profiles. |
| Prompts | Guided workflows for intake, outlining, compression, slide critique, and complete-deck review. |
| Tools | Retrieve criteria, assemble contextual review instructions, validate structured decks, and export supported textual formats. |

Proposed tools, subject to client requirements:

| Name | Inputs | Output and execution boundary |
| --- | --- | --- |
| `get_pitch_method` | Method version and optional section | Criteria and provenance; no generative-model call. |
| `prepare_pitch_workflow` | Presentation contract and chosen task | Contextual instructions and expected output schema for the connected AI. |
| `validate_pitch_deck` | Structured deck, claim register, profile | Deterministic findings with slide IDs, rule IDs, severity, and explanation. |
| `export_pitch_package` | Valid structured deck and format | Markdown or JSON content; no publication or external document edits. |

Writing and semantic critique can run in the connected AI without embedding a second model in the server. This avoids requiring a shared paid model account merely to distribute the method. If independent server-side AI review is desired later, it requires a separate provider, cost, and data-handling decision.

Because client support for resources and prompts must be verified, core method retrieval and workflow preparation should also be exposed through tools. An equivalent portable Markdown package gives collaborators another way to use the method when their application cannot connect to the server.

## Collaboration and state

Agree on one canonical project package: presentation contract, claims, deck specification, and method version. Exchange this package between contributors rather than relying on private chat memory.

A server distributing common rules does not automatically synchronize the team's deck. A first release can be stateless and operate on the package supplied in each request. A later shared workspace would need persistent storage, access control, revision history, and conflict handling. Updates should use an expected revision so one collaborator cannot silently overwrite another's work.

Local stdio suits locally launched clients. A remotely hosted Streamable HTTP service is a candidate for team access across devices, subject to each platform's supported connection modes. Hosting and access arrangements remain undecided.

## Adaptable visual profile

Suggested starting profile: uncluttered background, strong typographic hierarchy, ample spacing, limited accent colors, and visuals that explain a claim. Brand assets, colors, and composition remain configurable.

Word and item limits should produce warnings by default, with a reasoned override. Do not reduce readability by shrinking text to satisfy a slide limit. Do not impose a full fundraising sequence on a short validation pitch.

## Implementation acceptance criteria

1. Every inspected source section maps to an editable criterion with source attribution.
2. The same structured package can be consumed by at least two selected target clients, with supported capabilities documented.
3. An unsourced monetary claim produces an explicit evidence gap; the workflow does not fill it with an invented amount.
4. A hypothesis, planned pilot, or target cannot silently become a validated result during compression.
5. Cross-slide discrepancies in price, customer counts, funding, and time periods produce actionable findings.
6. Changing audience, duration, or brand does not require changing the method's code.
7. A narrative-only export preserves claim references, speaker notes, and unresolved items.
8. Proposed method changes carry a version so collaborators can identify which rules informed a draft.

## Decisions needed before implementation

- Which exact applications and account tiers must connect, including any collaborator whose application has no MCP support?
- Is the first deliverable a content-and-review package, or must it also generate an editable deck in a specific presentation tool?
- Is the first use case the immediate bootcamp pitch, with its duration and intended ask, or a general reusable toolkit?

These choices determine deployment and adapters. They do not prevent using the editorial reference above immediately.
