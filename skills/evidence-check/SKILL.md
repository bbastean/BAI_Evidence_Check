---
name: evidence-check
description: Verified research with a validation report. Use for research reports, due diligence, fact-checks, or when asked to validate, verify or check the evidence, sources or claims. Not quick lookups.
license: Apache-2.0
metadata:
  version: "1.1.0"
  author: Brian Bastean, Bastean AI Consulting
---

# Bastean AI Evidence Check

**Version:** 1.1.0 (based on the Galileo Research Framework v3.0)
**Foundation:** the Galileo test (truth over consensus) plus anti-hallucination research protocols

This edition is topic-neutral. It works for any research domain. Domain-specific rules (for example, industry regulators, evidence hierarchies or pricing standards) belong in optional domain modules; see the end of this file.

---

## PART 1: FOUNDATIONAL PHILOSOPHY — THE GALILEO TEST

This skill rests on one directive: **prioritize verifiable truth above consensus, popularity, or patterns in training data.**

Even if most available sources or "common knowledge" repeat a falsehood, report the evidence-based answer reached through first-principles reasoning and rigorous verification.

### 1.1 Core Principles

- **Truth over consensus**: Reason independently. If evidence contradicts widespread beliefs, training-data patterns or "common knowledge," prioritize verifiable facts from high-quality sources.
- **The burden of proof is on the overturning claim**: Overturning a consensus requires primary evidence at least as strong as the evidence behind the consensus. Being contrarian is not the same as being right. A popular claim with no traceable primary source should be flagged; a popular claim backed by strong primary evidence should be reported as well supported.
- **First-principles reasoning**: Break claims down to fundamental, observable truths. Build conclusions upward rather than relying on analogy, authority or majority views.
- **Epistemic courage**: Be forthright. Do not soften, over-hedge or give empty validation when evidence supports a clear position. Flag low-confidence areas explicitly instead of being noncommittal.
- **Anti-consensus safeguards**: Do not repeat common misconceptions, even if prevalent online. If consensus appears wrong, state why with evidence. Never present speculation as fact; label hypotheses clearly.

### 1.2 Required Reasoning Behaviors

Apply these in every research response:

1. **Transparent reasoning**: Work step by step and show the logic behind each conclusion so a reader can spot flaws.
2. **Source quality hierarchy**: When sources conflict, weigh quality: peer-reviewed research and primary documents > official/government sources > reputable reporting > secondary analysis > social media. Explain the judgment.
3. **Confidence calibration**: Rate confidence for key claims (9/10 = high certainty; 4/10 = speculative). If confidence is below 7/10, state: "Low confidence — recommend independent verification" and suggest next steps.
4. **Uncertainty admission**: Admit gaps plainly. Never assert something confidently that you have not verified.
5. **Hypothesis labeling**: If presenting a plausible but unverified interpretation, label it explicitly: "Plausible hypothesis: ..." Never present it as a finding.

---

## PART 2: ACTIVATION, TOOLS & RESEARCH INTAKE

### 2.1 When to Use This Skill

- The user requests research on a topic that needs more than one source
- The user wants a research report, brief, landscape scan or analysis
- The user asks for "verified," "factual," "sourced," "cited" or "fact-checked" information
- The research will inform a decision, due diligence, compliance work or publication
- The user asks you to check the claims in an existing document

For a one-line factual lookup, answer normally; the full protocol is disproportionate there.

### 2.2 Tool Requirements and Fallbacks

The verification workflow assumes two capabilities: web search, and fetching the full text of a page or document. Check which tools you actually have before starting.

- **Search and fetch available**: run the full workflow below. A connector that returns a source's full text or abstract (a literature database, a document store) counts as fetching it.
- **Search only, no page fetch**: you cannot complete Step 3 of the workflow. Classify everything as REPORTED at best, and say so at the top of the output.
- **No web access**: work only from documents the user provides. Treat anything from your own background knowledge as UNVERIFIED, keep it out of the main findings, and tell the user which claims they would need to check.

Never write as if you fetched a page you did not fetch. That single rule prevents most fabricated citations.

### 2.3 Depth Modes

Match the output to the request:

- **Quick verification** (one claim or a handful): for each claim give a verdict (VERIFIED / SUPPORTED / REPORTED / UNVERIFIED / NOT FOUND), the supporting quote and link, a numeric confidence rating, and any contradicting evidence. Skip the full report structure, but end with a short validation summary (Section 6.4).
- **Standard research report**: one file holding a clean version, then the Evidence Check version, then the Validation Report (Part 6).

If the user hasn't said which they want and the scope is unclear, ask.

### 2.4 Context Gathering

For a standard report, establish the following before searching. Ask only for what the request leaves genuinely unclear; don't make the user fill out a form.

**Core question:** "Research: [specific question or topic]"

**Context & scope:**
- **Purpose**: decision-making, analysis, compliance, due diligence, publication, etc.
- **Time frame**: current, last N years, historical
- **Geographic / sector scope**: any limits
- **Depth**: overview or comprehensive
- **Confidence threshold**: VERIFIED only, or SUPPORTED acceptable

**Specific information needs:**
1. Specific data points, trends or questions
2. Comparisons needed
3. Quantitative requirements (statistics, sizes, rates)
4. Qualitative needs (expert views, case studies, approaches)

**Source requirements** (defaults; the user can override):

| Source Tier | Examples |
|-------------|----------|
| **Required / priority** | Peer-reviewed journals; primary documents such as statutes, regulations, court records, official filings and published standards; national statistics agencies; original datasets |
| **Acceptable secondary** | Reputable news organizations, conference proceedings, established research firms and think tanks (note their funding or affiliation) |
| **Non-traditional** (if relevant) | Named experts' public posts, organization blogs, patent databases, study and trial registries, public code repositories, archived web pages |
| **Leads only, never cited as evidence** | Encyclopedias, wikis, AI-generated summaries, aggregator sites. Use them to find primary sources, then cite the primary source. |
| **Excluded** | Anonymous or unverifiable user-generated content. Marketing material is excluded as evidence for anything except what an organization says about itself. |

**Angles to explore:** case studies (how many, how deep), expert perspectives (practitioner, academic, regulatory, executive), and evidence types (statistics, trends, benchmarks, regulatory detail, cost data, technical specifications).

**Analysis requirements:** perspectives to include (proponents and critics, different stakeholders), comparisons, and gap identification.

The user-facing guide in `references/research-request-guide.md` has a worked example of a well-specified request. Read it if you need to show the user how to frame one.

---

## PART 3: SOURCE VERIFICATION & ANTI-HALLUCINATION PROTOCOLS

These protocols are constraints, not suggestions. Each exists because skipping it is how research outputs end up with invented facts.

### 3.1 Source Verification Workflow

Follow this for **each factual claim** before including it:

```
┌─────────────────────────────────────────────────────────────────┐
│ STEP 1: Identify the specific claim to be made                  │
├─────────────────────────────────────────────────────────────────┤
│ STEP 2: Locate a potential source via search                    │
├─────────────────────────────────────────────────────────────────┤
│ STEP 3: Fetch the actual page (not just the search snippet)     │
├─────────────────────────────────────────────────────────────────┤
│ STEP 4: Extract the exact text that supports the claim          │
├─────────────────────────────────────────────────────────────────┤
│ STEP 5: Confirm the text DIRECTLY supports the claim            │
│         (not just tangentially related)                         │
├─────────────────────────────────────────────────────────────────┤
│ STEP 6: Assess source authority and recency                     │
├─────────────────────────────────────────────────────────────────┤
│ STEP 7: Seek a corroborating source (for key claims)            │
├─────────────────────────────────────────────────────────────────┤
│ STEP 8: Assign a confidence classification                      │
├─────────────────────────────────────────────────────────────────┤
│ IF ANY STEP FAILS → Do NOT include as verified fact             │
│ Instead → Document in "What Was Not Found" or the appendix      │
└─────────────────────────────────────────────────────────────────┘
```

Search snippets are often truncated, outdated or stitched from different parts of a page, which is why Step 3 matters.

### 3.2 Source Documentation Requirements

For each source, record:

1. **Link**: a working URL (or a precise citation for offline documents the user supplied)
2. **Supporting quote**: the exact words that support the claim, in quotation marks. Quote the shortest span that proves the point, usually one sentence or less. Long verbatim passages add little and can run into copyright and platform limits.
3. **Source type**: primary document, official publication, news article, press release, etc.
4. **Date**: publication or last-updated date
5. **Authority**: why this source is credible for this claim

**Quote-to-interpretation mapping:**
- **Source quote**: "[exact text]" — [URL]
- **Use**: [how this supports the finding]

Show the original wording before you paraphrase or interpret it, so the reader can check that the interpretation is fair.

### 3.3 Source Triangulation

Any claim central to the findings, or that will inform a decision, needs at least two independent sources:

- **Primary source**: [URL and quote]
- **Corroborating source**: [URL and quote]

"Independent" means they did not get the information from each other or from the same upstream source.

**If single-source only**, flag it as **SINGLE-SOURCE FINDING** and note:
- why corroboration may be unavailable (niche topic, proprietary data, very recent development)
- your reliability assessment of that source
- whether the finding should be treated as preliminary

### 3.4 Confidence Classification

Assign one level to every finding:

| Confidence Level | Definition | Use in Report |
|------------------|------------|---------------|
| **VERIFIED** | Multiple independent authoritative sources confirm; quotes available from each | Main findings |
| **SUPPORTED** | One authoritative primary source with a supporting quote | Main findings, with source noted |
| **REPORTED** | Found in secondary sources but not traceable to a primary source | Main findings only with an explicit caveat about source type |
| **UNVERIFIED** | Appeared in search results but could not be confirmed on a fetched page | Appendix only, with disclaimer |
| **NOT FOUND** | Actively searched for; no credible source located | "What Was Not Found" section |

UNVERIFIED claims never go in the main findings. In the appendix, introduce them with: "The following appeared in search results but could not be verified by accessing the original source."

**Numeric rating**: for key claims, add a 1–10 confidence rating alongside the label. Below 7/10, add "Low confidence — recommend independent verification."

### 3.5 Quantitative Data Protocol

For any statistic, size, percentage, financial figure or other number:

| Requirement | Description |
|-------------|-------------|
| **Exact figure** | Report the number exactly as the source states it (not rounded, converted or adjusted) |
| **Methodology** | Include the basis if stated (e.g., "survey of 500 executives") |
| **Collection date** | Note when the data was collected, not only when it was published |
| **Original source** | If a source cites another source, trace it back and cite the original |
| **No silent calculations** | Never present a calculated, extrapolated or projected number as if a source stated it |
| **Currency & units** | Keep original currency and units; any conversion must be labeled as such |

**Derived figures**: if the user asks for a calculation (a growth rate, a per-capita figure, a currency conversion), show the formula and the sourced inputs, and label the result **DERIVED**. A derived figure is analysis, not a finding, and inherits the lowest confidence level of its inputs.

**Proper citation example:**
> "The global market was valued at $4.2 billion in 2022" — [Source: company annual report, published March 2023, data as of December 31, 2022] — [URL]

**Not acceptable:**
> "The market is approximately $4–5 billion" (rounded/estimated)
> "This suggests the 2024 market could be around $5.1 billion" (unlabeled projection)

### 3.6 Source Recency Standards

| Information Type | Maximum Acceptable Age | Exception Handling |
|------------------|------------------------|--------------------|
| Market data / statistics | 2 years (or as the user specifies) | Flag as "DATED" if older; assess obsolescence risk |
| Laws, regulations, official guidance | Must be current | Check for superseding versions; note effective dates |
| Organization operational details | 12 months | Note that details may have changed |
| Scientific / technical findings | Context-dependent | Say whether recent studies or foundational work is needed |
| Prices / financial data | 12 months | Prices move quickly in most markets; prefer the latest figure |
| Policy / legislation in progress | Must be current | Check amendments and implementation status |

If only older sources exist, say so and assess whether the information may be outdated or superseded.

---

## PART 4: CONTRADICTORY EVIDENCE & THE PARITY REQUIREMENT

### 4.1 Contradictory Evidence Search

For each key finding, actively look for contradicting evidence or alternative views:

1. After establishing a finding, search for "[topic] criticism," "[topic] alternative view," "[topic] controversy," "[topic] disputed," "[topic] replication" or similar
2. Document what counter-evidence exists
3. If sources disagree, present both positions with their evidence
4. If nothing turns up, state: "Active search for contradictory evidence yielded no significant dissenting views"

Evaluate the substance of a disagreement, not just the number of sources on each side. Ten articles repeating one press release are one source.

### 4.2 Parity: Equal Credibility Standards

Contradictory evidence must meet the **same verification, triangulation and classification standards** as primary findings. Holding dissent to a lower bar would let weak claims undermine well-verified findings; holding it to a higher bar would bias the report toward its first conclusion. Both are failures.

| Requirement | Applied to Contradictory Evidence |
|-------------|-----------------------------------|
| **Source verification** | Same 8-step workflow (Section 3.1) |
| **Triangulation** | Material contradictory claims need two independent sources, or a single-source flag |
| **Confidence classification** | Assign a level, VERIFIED through NOT FOUND |
| **Quantitative protocol** | Same standards (Section 3.5) |
| **Recency** | Same thresholds (Section 3.6) |

### 4.3 Handling Contradictory Evidence by Confidence Level

| Contradictory Evidence Confidence | Handling |
|-----------------------------------|----------|
| **VERIFIED** | Include in "Dissenting Views" with full weight; may warrant revising conclusions |
| **SUPPORTED** | Include in "Dissenting Views"; note single-source status |
| **REPORTED** | Include with caveat: "This dissenting view appears in secondary sources but could not be traced to primary evidence" |
| **UNVERIFIED** | Keep out of the main report; the appendix may note that unverified contrary claims were found and excluded |
| **NOT FOUND** | State: "Active search for contradictory evidence yielded no verifiable dissenting views" |

### 4.4 Comparative Credibility Disclosure

When presenting a dissenting view next to a primary finding, compare their support explicitly:

```
PRIMARY FINDING: [Claim]
- Confidence: VERIFIED
- Sources: [X] independent sources
- Triangulation: Complete

CONTRADICTORY VIEW: [Dissenting claim]
- Confidence: SUPPORTED
- Sources: Single source ([source type])
- Triangulation: Single-source finding

CREDIBILITY COMPARISON: Primary finding has stronger evidentiary support
(multiple corroborating sources vs. a single source for the contrary view)
```

### 4.5 No Unbalanced Presentation

Do not:
- present single-source dissent as equivalent to multi-source findings
- put UNVERIFIED dissent in the main body
- let dissent undermine a conclusion without meeting the same verification standard
- use loose attribution for either side ("some say," "critics argue") without a verified source

**Dedicated section:**

> **Dissenting Views / Contradictory Evidence**
>
> | Dissenting View | Confidence Level | Source Count | Credibility vs. Primary Finding |
> |-----------------|------------------|--------------|---------------------------------|
> | [View 1] | [Level] | [Count] | [Higher/Equal/Lower] |
>
> [Summary of alternative perspectives and their verification status, or an explicit statement that no verifiable dissenting views were found]

---

## PART 5: RED FLAGS, PROHIBITIONS & SAFEGUARDS

### 5.1 Red Flags to Call Out

| Red Flag | Action |
|----------|--------|
| **Circular sourcing** | Several articles citing one original → trace to the original; count as one source |
| **Anonymous attribution** | "Industry experts" with no names → flag as low reliability |
| **Press release as sole source** | Organization's own announcement only → flag; seek independent confirmation |
| **Source discrepancies** | Sources disagree → document both; don't pick one arbitrarily |
| **Snippet-only information** | In a search snippet but not on the fetched page → don't use; mark UNVERIFIED |
| **Suspicious precision** | One source is oddly precise where others are vague → flag for verification |
| **Outdated information** | Older than the recency standard → flag as "DATED" |
| **Broken or inaccessible links** | Can't access the source → don't use the information |
| **Consensus without primary evidence** | Widely repeated claim with no traceable primary source → apply the Galileo test; flag as possibly unfounded |
| **Undisclosed interest** | Source has a financial or advocacy stake in the conclusion → note it; it doesn't disqualify the source but affects weight |

### 5.2 No Disguised Inference

Inference is not banned. Disguising inference as a finding is. Phrases like these signal a logical bridge being passed off as evidence:

- "It's reasonable to assume..."
- "This likely means..."
- "Based on similar cases, we can infer..."
- "Industry practice suggests..."
- "It stands to reason that..."
- "This implies..."

If direct evidence doesn't exist, say so. The absence of information is itself a finding. If an interpretation is useful to the user, put it in a clearly labeled **Analysis** or **Plausible hypothesis** paragraph, separate from the findings, with its confidence rating and the evidence it rests on.

### 5.3 Prohibited Practices

| Prohibition | Why |
|-------------|-----|
| Stating facts that can't be traced to a specific, accessible source | Untraceable claims can't be checked |
| Merging several sources into one synthesized "fact" no single source supports | Composite claims hide which part is unsupported |
| Using background knowledge to fill gaps when verification fails | This is the main route to hallucination |
| Rounding, converting or adjusting source numbers without labeling it | Silent changes are data manipulation |
| Presenting projections or forecasts as established facts | Conflates speculation with fact |
| Attributing claims to "common practice" or "typically" | Unverifiable generalization |
| Citing sources you could not access | Phantom citations |
| Filling silence with plausible-sounding information | Gap-filling hallucination |
| Repeating common misconceptions because they are popular | Fails the Galileo test |
| Softening a clear, evidence-based position to avoid controversy | Epistemic cowardice |

---

## PART 6: REQUIRED OUTPUT STRUCTURE

### 6.1 One File, Two Versions

A standard report is delivered as one file with three parts, in this order, each starting on a new page (page breaks as described in Section 6.3):

1. **Clean version**: the report a reader could review and publish as is
2. **Evidence Check version**: the same report with every claim labeled and scored
3. **Validation Report**: the audit trail (Section 6.3)

Write the Evidence Check version first, then derive the clean version from it by removing the labels. That keeps the two in step: both must make the same claims, with the same numbers, the same sources and the same level of certainty. The clean version drops the tags, not the caveats. A single-source or low-confidence finding still reads as tentative in plain words ("one 2024 trial found..."), and nothing UNVERIFIED appears in either version.

If the user asks for only one version, give them that one.

**Report sections** (both versions use the same sections in the same order):

1. **Executive Summary**: 2–3 paragraphs of key findings
2. **Detailed Findings**: by theme or question
3. **Supporting Evidence**: quotes with links, quote-to-interpretation mapping
4. **Case Studies / Examples**: if requested, verified the same way
5. **Analysis** (optional): interpretation and hypotheses, kept apart from findings
6. **Dissenting Views / Contradictory Evidence**
7. **What Was Not Found**: mandatory; in the clean version it may be titled "Limitations and Open Questions"
8. **Source Reference List**: all sources by category, with type and date

**Disclaimer (both versions).** Directly under each version's title, include a short, plain disclaimer, for example: "This report was prepared with AI assistance. It is for educational and informational purposes, may contain errors, and is not a substitute for professional advice. Check important facts against the cited sources."

**Clean version.** Directly under its title, add one line in red: "Clean version. The Evidence Check version follows." The reader deletes this line before publishing. Otherwise the clean version has no claim labels, dissent labels, confidence labels, confidence scores or credibility tables. Citations and the source list stay, because a publishable report still needs them.

**Evidence Check version.** The same report with labels in red, placed right after the sentence or table row they apply to:
- **Facts:** `[F1 · VERIFIED · 9/10]`, `[F2 · SUPPORTED · 7/10]`, `[F3 · REPORTED · 5/10]`, numbered in order through the whole report
- **Dissenting views:** `[D1 · SUPPORTED · 6/10]`, `[D2 ...]`, numbered separately
- **Derived figures:** `[F4 · DERIVED]`, with the calculation shown
- **Hypotheses and analysis:** `[H1 · ANALYSIS · 4/10]`
- The Dissenting Views section keeps its credibility comparison table, and the "Single-source finding" and "DATED" flags stay

Each ID is used once and matches its row in the Validation Report's claim register.

**Red, by format:** red font color (#C00000) in Word, PDF, HTML and document editors that support text color. Where color isn't available (chat, plain Markdown, an editor without text color), the labels appear as bold bracketed text and the clean-version note as a bold line.

Length follows the user's request and applies to the clean version. The Evidence Check version and the Validation Report don't count toward a length limit; they are the audit trail, not part of the argument.

### 6.2 Mandatory "What Was Not Found" Section

> **What Was Not Found / Research Gaps**
>
> - **Unanswered questions**: parts of the request that could not be answered
> - **Missing data points**: specific data searched for but not found
> - **Low-quality source areas**: topics where only unreliable sources existed
> - **Incomplete analysis**: where a conclusion wasn't possible
> - **Verification failures**: claims seen in search that couldn't be verified
> - **Consensus without evidence**: widely repeated claims with no traceable primary source

If everything was answered: "All research questions were addressed with VERIFIED or SUPPORTED findings."

### 6.3 Validation Report

The Validation Report lets a reader audit the research without redoing it. It's the last part of every standard report file, after the Evidence Check version, it starts on a new page, and it's titled **Validation Report**.

**Starting a new page.** The Evidence Check version and the Validation Report each start on a new page. Use the page break that the output format supports:
- Word (.docx): a hard page break immediately before the Validation Report heading
- PDF, HTML or anything printed: `break-before: page` on the section (or the generator's equivalent)
- A document editor or artifact with page breaks: that editor's page break
- An editor without page breaks, such as a Claude Docs document: a horizontal rule, then the heading
- Chat or plain Markdown, which have no pages: a horizontal rule, then the heading, so the section is plainly separate

**Contents, in this order:**

**A. Verification summary.** A table counting the claims in the report by label, with a total:

| Label | Count |
|-------|-------|
| VERIFIED | |
| SUPPORTED | |
| REPORTED | |
| DERIVED | |
| Analysis / plausible hypothesis | |
| UNVERIFIED (kept out of findings) | |
| NOT FOUND | |
| CORRECTED (only when checking an existing document: claims found wrong, with the fix) | |
| **Total claims checked** | |

Follow the table with one or two sentences on overall reliability, for example how many key findings are triangulated and where confidence is weakest.

**B. Method.** The date the verification was done; which tools were available (search, page fetch, user documents) and any limits that imposed; roughly how many searches were run and pages fetched; and the source policy applied (required, acceptable, leads-only, excluded).

**C. Claim register.** One row for every factual claim and every number in the report:

| ID | Claim (short form) | Report section | Label | Confidence (1–10) | Independent sources | Single-source? | Primary source |
|----|--------------------|----------------|-------|-------------------|---------------------|----------------|----------------|

Use the same IDs as the Evidence Check version (F1, D1, H1 and so on). Keep every row, even in a long report; group rows by report section if that helps reading. Don't sample or summarize the register.

**D. Dissent parity check.** For each dissenting view: its label, its source count, and whether it was stronger, equal or weaker than the finding it challenges.

**E. Red flags.** Each red flag from Section 5.1 that came up, where, and how it was handled.

**F. Exclusions and verification failures.** Claims that were left out or demoted, and what was tried before giving up on each.

**G. Quality checks.** The result of the Part 7 checklist. State "All checks met," or list each check that wasn't met and why.

**Before finalizing, reconcile all three parts.** Every labeled claim in the Evidence Check version must appear in the register with the same ID, label and number, and the clean version must make the same claims with the same numbers. A mismatch means one of them is wrong; fix it before delivering.

### 6.4 Validation Summary for Quick Verifications

A quick verification doesn't need the full Validation Report or a page break. End it with a short summary: the count of claims by label, the date checked, which tools were available, and any claim that couldn't be verified, with the reason.

---

## PART 7: QUALITY ASSURANCE CHECKLIST

Before finalizing, confirm:

**Source verification**
- [ ] Every factual claim has an accessible source and a supporting quote
- [ ] Numbers include the original figure, methodology (if available) and date
- [ ] Links work and lead to the cited content
- [ ] Recency standards are met or exceptions noted
- [ ] Nothing is described as fetched that wasn't fetched

**Confidence & classification**
- [ ] Every finding has a classification
- [ ] Key claims have a 1–10 rating; ratings below 7 are flagged
- [ ] No UNVERIFIED claims in the main findings
- [ ] Derived figures are labeled DERIVED with inputs shown

**Triangulation**
- [ ] Key findings are corroborated or flagged single-source, with a reliability note

**Contradictory evidence & parity**
- [ ] A contradictory-evidence search was run and documented
- [ ] Dissent meets the same standards as primary findings and has a classification
- [ ] Credibility comparison documented for each dissenting view
- [ ] No UNVERIFIED dissent in the main body

**Galileo test**
- [ ] First-principles reasoning applied, not consensus alone
- [ ] Any claim that a consensus is wrong rests on primary evidence at least as strong as the consensus
- [ ] Clear positions stated where the evidence supports them
- [ ] Hypotheses and analysis labeled and kept apart from findings

**Completeness**
- [ ] Red flags called out
- [ ] "What Was Not Found" complete
- [ ] No prohibited practices
- [ ] File order is clean version, Evidence Check version, Validation Report, each starting on a new page (or after a horizontal rule in chat)
- [ ] Both versions carry the AI-assistance disclaimer; the clean version has the red "Clean version" note
- [ ] Clean version has no F/D/H labels, confidence labels or scores, but keeps its citations and its plain-language caveats
- [ ] Evidence Check labels are in red, numbered once each, and match the claim register
- [ ] Clean and Evidence Check versions make the same claims with the same numbers

---

## PART 8: WORKING HABITS

**Before searching**: pin down scope, the specific metrics, time periods and entities involved, and the user's confidence threshold.

**During research**: fetch real pages, capture the supporting quote before writing the claim, track each claim's status as you go, and log gaps the moment you hit them.

**When presenting**: lead with the confidence level, make source quality visible, give dissent the same scrutiny as the main finding, never hide gaps, and disagree politely but firmly when the evidence warrants it.

**Quality over completeness**: "NOT FOUND" is better than a fabrication. Partial verified information is worth more than comprehensive unverified information.

---

## DOMAIN MODULES

The core framework is topic-neutral. A domain module adds field-specific rules on top of it: which primary sources count as authoritative in that field, stakeholder perspectives to separate, an evidence hierarchy, recency rules, and field-specific red flags. A module supplements the core protocols; it never relaxes them.

- **To use a module**: if the user's environment includes a module file for their field, read it alongside this one.
- **To create a module**: copy `references/domain-module-template.md` and fill it in for the field (law, finance, public health, engineering, journalism, etc.).

---

*The Galileo test — truth over consensus through first-principles reasoning and rigorous verification — is the standard for every research output produced under this skill.*
