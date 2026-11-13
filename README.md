# Bastean AI Evidence Check

A research skill for Claude that holds every claim to a verification standard before it reaches the report. It is built for work where a wrong fact costs something: due diligence, policy and regulatory research, literature and market scans, fact-checking a document before it goes out, or comparing contested positions fairly.

Its core principle is the Galileo test, named for the astronomer Galileo Galilei: report what the primary evidence shows, even when popular opinion says otherwise, and hold any claim that a consensus is wrong to at least the same standard of evidence as the consensus itself.

## What it does

When you ask Claude for research, the skill has it:

- **Fetch before citing.** Each claim is checked against the full source page, not a search snippet, and backed by a short supporting quote and a link.
- **Triangulate key findings.** Central claims need two independent sources or are flagged as single-source.
- **Label confidence.** Every finding is marked VERIFIED, SUPPORTED, REPORTED, UNVERIFIED or NOT FOUND, with a 1–10 rating for key claims. Unverified material stays out of the main findings.
- **Handle numbers strictly.** Figures are reported exactly as stated, with method and date. Any calculation is shown and labeled DERIVED.
- **Give dissent equal scrutiny.** Contradicting evidence is searched for and held to the same verification standard as the main findings, then compared side by side.
- **Separate fact from inference.** Interpretation is allowed, but it goes in a labeled Analysis section, never disguised as a finding.
- **Report the gaps.** Every report includes a "What Was Not Found" section.
- **Two versions in one file.** A full report comes first as a clean version, ready to review and publish, then as an Evidence Check version where every fact (F1, F2...), dissenting view (D1, D2...) and hypothesis carries its confidence label and score in red. Both carry an AI-assistance disclaimer.
- **Show the audit trail.** The file ends with a Validation Report on its own page: counts of claims by confidence level, the method used, a register of every claim and number keyed to the same IDs, the dissent check, red flags, exclusions, and the results of the quality checklist.

It has two depth modes: a quick verification for checking one or a few claims, which ends with a short validation summary, and a full structured research report.

## Install

From the Claude directory: search for "Bastean AI Evidence Check" and select Install.

From GitHub in Claude Code:

```
/plugin marketplace add bbastean/BAI_Evidence_Check
/plugin install bastean-ai-evidence-check@bastean-ai
```

## Using it

The skill activates on its own for research, fact-checking and "verified" or "sourced" requests. To call it directly, ask Claude to "use Bastean AI Evidence Check." For the best results, say what the research is for, the time frame, and your confidence threshold. `skills/evidence-check/references/research-request-guide.md` has a worked example.

## Making sure it runs

Claude decides on its own whether a request needs this skill, and for ordinary research questions it often starts researching without it. To make sure it runs:

- Name it in the request: "Use Evidence Check to research..." or "Run this through Evidence Check."
- Or add one line to your Claude profile preferences or to a project's instructions: "For any research request, use the Evidence Check skill."
- If you have another research or fact-checking skill installed, name this one, or turn the other off, so the two don't compete.

## Adding your own field

The framework is topic-neutral. To add rules for your field (authoritative sources, an evidence hierarchy, recency rules, field-specific red flags), copy `skills/evidence-check/references/domain-module-template.md`, fill it in, and keep it alongside the skill. A module can tighten the core rules but never loosen them.

## What this plugin runs, sends and fetches

This plugin contains only written instructions (Markdown files). It has no scripts, hooks, MCP servers or bundled code, and it sends no data anywhere. It asks Claude to use whatever web search and page-fetch tools your Claude environment already provides, so the pages Claude visits during research are fetched by those tools under your existing settings. If no web tools are available, the skill tells Claude to work only from documents you supply and to mark everything else as unverified.

## Limitations

The framework reduces the risk of fabricated or unsupported claims; it does not eliminate it. Sources can be wrong, pages change, and confidence ratings are judgments. Treat the output as well-documented research to review, not as professional, legal, medical or financial advice. Check anything consequential against the cited sources yourself.

## Author and license

Created by Brian Bastean, PharmD, RPh, MBA, Founder and Managing Director of Bastean AI Consulting ([bastean.com](https://bastean.com)). Licensed under the Apache License 2.0: you may use, modify and share it, including commercially. Copies and adaptations must keep the license and the attribution in `NOTICE`, and modified files must say they were changed. See `LICENSE` and `NOTICE`.
