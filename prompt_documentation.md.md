# Prompt Documentation: Kubernetes vs. Docker Swarm vs. AWS Fargate

## 1. Project Overview

**Objective:** Compare Kubernetes, Docker Swarm, and AWS Fargate using a
structured prompting workflow. The workflow generates background
knowledge, drafts a comparison report, checks factual claims, revises
the report, identifies hidden assumptions, and produces a comparison
table and executive summary.

**Role:** Lead Systems Architect

**Final deliverables:** - A factual background knowledge sheet - A
technology comparison report - Verification questions and independently
checked answers - A corrected final report - An analysis of hidden
assumptions and potential bias - A comparison table - A 150-word
executive summary with a recommendation

> **Important:** Replace bracketed placeholders with the relevant
> content before running each prompt. Verify technical claims against
> current official documentation before submitting the final report.

------------------------------------------------------------------------

## 2. Prompt 1 --- Generate Background Knowledge

**Purpose:** Collect factual information about the three technologies
before writing a comparison. This step is intended to reduce unsupported
claims and premature recommendations.

``` text
Act as a technical research assistant supporting a Lead Systems Architect.

Generate a factual background sheet detailing the core architecture, scalability,
setup complexity, operational requirements, and cost structures of:

1. Kubernetes
2. Docker Swarm
3. AWS Fargate

Focus on documented specifications, architecture, constraints, pricing mechanisms,
and clearly attributable facts. Do not compare the technologies or recommend one
at this stage.

For each technology, organize the information under:
- Core architecture
- Scaling model and documented limits, if applicable
- Setup and configuration requirements
- Operational responsibilities
- Cost model and potential additional charges
- Important limitations and workload restrictions
- Official documentation sources

Distinguish documented facts from estimates or general observations. If a figure
depends on version, configuration, Region, or workload, state that dependency.
Do not invent missing figures. Mark claims that require verification.
```

### Expected output

A factual sheet with separate sections for Kubernetes, Docker Swarm, and
AWS Fargate, including source links and a list of claims that need
further verification.

------------------------------------------------------------------------

## 3. Prompt 2 --- Draft the Technology Comparison Report

**Purpose:** Use the background sheet to create a structured first draft
without adding unsupported facts.

``` text
Act as a Lead Systems Architect.

Write a technology comparison report using only the background facts below as
the primary factual basis.

=== BACKGROUND FACTS ===
[Paste the fact sheet generated in Prompt 1]
========================

Compare:
- Kubernetes
- Docker Swarm
- AWS Fargate

Use these H2 headings in this exact order:
## Introduction
## Tech Overviews
## Detailed Comparison
## Final Verdict

Discuss architecture, scalability, setup complexity, operational overhead, cost
model, reliability considerations, flexibility, and suitable use cases.

Explain important trade-offs rather than treating any technology as universally
best. Distinguish AWS Fargate as a managed container compute service used with
an orchestrator such as Amazon ECS or Amazon EKS.

Do not include a summary comparison table in this draft. Do not invent facts,
precise limits, prices, or performance figures that are not supported by the
background facts. Identify any uncertainty and include relevant official
documentation references.
```

### Expected output

A report with the four required H2 headings, a balanced discussion of
the technologies, and documentation references.

------------------------------------------------------------------------

## 4. Prompt 3 --- Generate Verification Questions

**Purpose:** Identify factual claims in the baseline report that should
be checked independently.

``` text
Review the baseline report below as a technical fact-checker.

=== BASELINE REPORT ===
[Paste the initial comparison report]
=======================

Generate exactly four specific verification questions about claims that could
be inaccurate, incomplete, version-dependent, or misleading.

Prioritize:
1. Kubernetes documented scale limits and the conditions under which they apply.
2. Docker Swarm manager-node guidance, distinguishing recommendations from hard
   technical limits.
3. AWS Fargate pricing units, billing minimums, included storage, and additional
   charges.
4. Amazon EKS on Fargate workload restrictions, including DaemonSets and GPU
   workloads.

For each question, identify the claim to verify and the type of official
documentation needed. Do not answer the questions yet. Do not assume that a
claim is true merely because it appears in the report.
```

### Expected output

Exactly four verification questions tied to concrete claims in the
draft.

------------------------------------------------------------------------

## 5. Prompt 4 --- Answer the Verification Questions

**Purpose:** Check each verification question independently and record
any qualifications or corrections.

``` text
Act as an independent technical fact-checker.

Answer each of the four verification questions below. Use current official
documentation from Kubernetes, Docker, and AWS wherever possible.

=== VERIFICATION QUESTIONS ===
[Paste the four questions generated in Prompt 3]
==============================

For every question:
1. State the verified finding.
2. Give the relevant technical details and conditions.
3. Distinguish a documented limit from a recommendation or common practice.
4. Note version, configuration, Region, or workload dependencies.
5. Provide the official source URL.
6. State whether the original report should be corrected, qualified, or can
   remain unchanged.

If official sources appear inconsistent, explain the discrepancy instead of
silently choosing one interpretation. Do not fabricate a source or claim to
have verified a detail that the documentation does not establish.
```

### Expected output

Four answers, each with a finding, qualifications, correction guidance,
and official documentation source.

------------------------------------------------------------------------

## 6. Prompt 5 --- Revise the Report Using Verified Findings

**Purpose:** Produce the corrected report by incorporating verified
information and removing or qualifying unsupported claims.

``` text
Act as a Lead Systems Architect and technical editor.

Rewrite the baseline report using the verification findings below. Preserve the
original report's purpose and required structure, but correct factual errors,
qualify uncertain claims, and remove unsupported statements.

=== BASELINE REPORT ===
[Paste the baseline report]
=======================

=== VERIFIED FINDINGS ===
[Paste the answers to the four verification questions]
========================

Use these H2 headings in this exact order:
## Introduction
## Tech Overviews
## Detailed Comparison
## Final Verdict

Requirements:
- Include the verified Kubernetes scale figures only with their version and
  applicable conditions.
- Explain Docker Swarm manager-node guidance accurately, distinguishing
  recommendations from hard limits.
- Describe AWS Fargate's resource-based pricing, billing minimums, included
  storage, and possible additional charges only to the extent supported by the
  findings.
- Explain relevant EKS-on-Fargate restrictions without implying that every
  EKS deployment has those same restrictions.
- Keep the discussion balanced and context-dependent.
- Include official documentation references.
- Do not add a summary table at this stage.
- Do not claim that a technology is always cheapest, fastest, or best.
```

### Expected output

A corrected report that retains the required headings and incorporates
the fact-checking results.

------------------------------------------------------------------------

## 7. Prompt 6 --- Identify Hidden Assumptions and Bias

**Purpose:** Critically examine the finalized report for assumptions
that could influence its conclusions.

``` text
Analyze the finalized technology comparison report below.

Identify and list exactly three hidden assumptions the writer makes about
Kubernetes, Docker Swarm, or AWS Fargate. Possible areas include scalability,
simplicity, cost, operational effort, portability, and suitability for teams.

For each assumption:
1. State the hidden assumption clearly.
2. Explain what in the report suggests the assumption.
3. Explain why the assumption may not hold in every organization or workload.
4. Identify whether it introduces bias and name the type of bias.
5. Suggest how to make the analysis more objective.

=== FINALIZED REPORT ===
[Paste the corrected report]
========================

Base the analysis on the report. Do not present an assumption as a verified
fact, and distinguish reasonable inference from explicit statements in the
report.
```

### Expected output

Three clearly explained assumptions, the possible bias each introduces,
and a practical way to reduce that bias.

------------------------------------------------------------------------

## 8. Prompt 7 --- Create the Comparison Table

**Purpose:** Summarize the main differences using consistent qualitative
ratings.

``` text
Using the finalized technology comparison report, create a Markdown table
comparing Kubernetes, Docker Swarm, and AWS Fargate across exactly these columns:

- Technology
- Scalability (High/Med/Low)
- Setup Complexity (High/Med/Low)
- Operational Overhead (High/Med/Low)
- Cost Model (e.g. Pay-per-node, Pay-per-use, Free)

Use one row per technology. Keep the ratings relative and explain that actual
results depend on workload, configuration, deployment model, and team expertise.

For cost model:
- Distinguish the cost of open-source orchestration software from infrastructure
  and operations costs.
- Describe AWS Fargate as usage-based managed compute, with applicable related
  service charges.
- Avoid implying that open-source software means a deployment has no cost.

Do not add unsupported exact prices. Output the Markdown table followed by a
brief note explaining the limits of qualitative ratings.
```

### Expected output

A Markdown table with the five requested columns, three technology rows,
and a brief qualification note.

------------------------------------------------------------------------

## 9. Prompt 8 --- Write the Executive Summary and Recommendation

**Purpose:** Synthesize the comparison and recommend a suitable
technology for a startup prioritizing speed over infrastructure scaling.

``` text
Write an executive summary of approximately 150 words synthesizing the findings
of the finalized comparison of Kubernetes, Docker Swarm, and AWS Fargate.

Context:
The target organization is a fast-growing startup that prioritizes speed of
product development and delivery over directly managing infrastructure scaling.

Requirements:
- Briefly describe the main strengths and trade-offs of all three technologies.
- Recommend the best fit for this startup and explain why.
- Consider operational overhead, deployment speed, scalability, cost, and
  dependence on a cloud provider.
- Treat AWS Fargate as managed container compute used with Amazon ECS or EKS.
- Make the recommendation conditional on the startup's actual requirements
  rather than claiming it is universally best.
- Mention that usage-based costs can rise as workloads grow.
- Keep the summary near 150 words and use clear, professional language.

Base the summary on the finalized comparison. Do not introduce new technical
claims or unsupported cost estimates.
```

### Expected output

An approximately 150-word executive summary with a clear, justified
recommendation.

------------------------------------------------------------------------

## 10. Recommended Source Checklist

Use official documentation when verifying technical claims:

-   **Kubernetes:** https://kubernetes.io/docs/
-   **Kubernetes large-cluster guidance:**
    https://kubernetes.io/docs/setup/best-practices/cluster-large/
-   **Docker Swarm overview:** https://docs.docker.com/engine/swarm/
-   **Docker Swarm node behavior:**
    https://docs.docker.com/engine/swarm/how-swarm-mode-works/nodes/
-   **AWS Fargate pricing:** https://aws.amazon.com/fargate/pricing/
-   **AWS Fargate FAQs:** https://aws.amazon.com/fargate/faqs/
-   **Amazon EKS documentation:**
    https://docs.aws.amazon.com/eks/latest/userguide/

Check that each source supports the specific claim being made. Pricing,
service limits, supported features, and product behavior can change over
time.

------------------------------------------------------------------------

## 11. Suggested Workflow

1.  Run Prompt 1 and save the background sheet.
2.  Use that sheet in Prompt 2 to draft the report.
3.  Use Prompt 3 to generate four verification questions.
4.  Use Prompt 4 to answer those questions with official sources.
5.  Use Prompt 5 to create the corrected report.
6.  Use Prompt 6 to analyze hidden assumptions and potential bias.
7.  Use Prompt 7 to create the comparison table.
8.  Use Prompt 8 to write the executive summary.
9.  Review the final output for factual accuracy, consistent
    terminology, and source quality.

**Suggested final project files:** - `generated_knowledge.md` -
`baseline_report.md` - `verification_questions.md` -
`verification_answers.md` - `final_report.md` -
`hidden_assumptions.md` - `comparison_table.md` -
`executive_summary.md` - `prompt_documentation.md` (this document)
