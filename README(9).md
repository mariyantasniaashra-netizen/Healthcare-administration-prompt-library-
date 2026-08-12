# CareLink Medical Centre AI Prompt Library

## Overview

This repository contains a 10-prompt AI Prompt Library for **CareLink Medical Centre**, designed to automate repetitive **patient appointment scheduling and administrative follow-up** tasks.

The project was developed for an **AI in Business** assessment focused on applying prompt engineering to a real business workflow, demonstrating iterative prompt improvement, evaluating business value, and addressing responsible AI risks.

---

## Business Context

**Business field:** Healthcare Administration  
**Organisation:** CareLink Medical Centre  
**Organisation type:** Medical clinic / outpatient healthcare provider  
**Selected workflow:** Patient appointment scheduling and administrative follow-up  
**Primary objective:** Reduce repetitive administration while improving patient communication and service efficiency.

Healthcare reception and administration teams frequently perform repetitive tasks such as:
- reading appointment requests
- identifying missing booking information
- sending confirmations
- sending reminders
- handling rescheduling
- processing cancellations
- managing waitlists
- answering routine appointment questions
- following up missed appointments
- preparing daily administrative summaries

These tasks are suitable for AI-assisted automation because they are repetitive, rules-based, text-heavy, and usually non-clinical.

---

## Business Problem

Manual appointment administration creates several operational problems:

- staff spend time rewriting similar messages
- response times can be slow during busy periods
- communication can be inconsistent
- missing information creates additional back-and-forth
- cancelled appointments may not be filled quickly
- routine enquiries consume reception capacity
- missed appointments reduce clinic utilisation
- managers may lack a concise view of unresolved administrative work

The proposed Prompt Library addresses these issues by standardising and partially automating the workflow.

---

## Proposed AI Solution

The solution is a structured prompt library containing 10 reusable prompts.

| # | Prompt | Workflow |
|---|---|---|
| 1 | Appointment Request Information Extraction | Convert unstructured patient requests into structured booking data |
| 2 | Missing Booking Information Request | Ask only for information required to continue booking |
| 3 | Appointment Confirmation Generator | Produce standardised booking confirmations |
| 4 | Appointment Reminder Generator | Produce appointment reminders |
| 5 | Rescheduling Request Processor | Match patient preferences with available slots |
| 6 | Cancellation Request Processor | Process clear cancellation requests consistently |
| 7 | Waitlist Slot Matching | Match cancelled slots to eligible waitlisted patients |
| 8 | Routine Appointment FAQ Response | Answer common non-clinical administrative questions |
| 9 | Missed Appointment Follow-up | Draft respectful no-show follow-up communication |
| 10 | Daily Appointment Administration Summary | Summarise appointment operations and unresolved work |

---

## Prompt Engineering Strategies

The prompts use several techniques to increase reliability and automation readiness.

### 1. Role prompting
Each prompt gives the model a specific role such as:

> “You are an AI healthcare administration assistant.”

This reduces ambiguity and keeps the model focused on administrative responsibilities.

### 2. Context prompting
The prompts specify the healthcare setting, workflow, and business objective.

### 3. Structured input variables
Inputs are clearly separated using variables such as:

```text
PATIENT_MESSAGE:
{{patient_message}}

AVAILABLE_SLOTS:
{{available_slots}}
```

This makes prompts reusable and easier to integrate into workflows.

### 4. Task decomposition
Complex tasks are broken into numbered instructions.

### 5. Explicit constraints
The prompts state what the AI must not do, especially:
- do not invent missing information
- do not provide medical advice
- do not diagnose
- do not make clinical prioritisation decisions
- do not expose unnecessary patient information

### 6. Structured output
Prompts use:
- JSON
- labelled fields
- status indicators
- fixed report sections

Structured outputs improve consistency and enable downstream automation.

### 7. Grounding
Where factual accuracy is important, the model is restricted to supplied data or an approved clinic knowledge base.

### 8. Human-in-the-loop escalation
The prompts escalate:
- ambiguous requests
- clinical questions
- disputes
- exceptions
- low-confidence cases
- policy decisions requiring authority

### 9. Validation
Many prompts include a final quality or validation check before output.

### 10. Privacy and responsible AI controls
The prompts minimise unnecessary patient-identifying information and prevent the AI from making autonomous clinical decisions.

---

## Why This Workflow Was Selected

Appointment administration was selected instead of a highly clinical workflow because it provides a strong balance between:

- automation potential
- business value
- low-to-moderate implementation complexity
- measurable outcomes
- responsible AI feasibility

It demonstrates how generative AI can reduce repetitive work without replacing healthcare professionals.

---

## Expected Business Impact

The Prompt Library could provide the following benefits:

### Operational impact
- faster response times
- lower repetitive workload
- more consistent patient communications
- quicker processing of cancellations and rescheduling
- improved waitlist utilisation
- fewer administrative errors

### Patient impact
- faster replies
- clearer instructions
- easier rescheduling
- improved communication consistency
- potentially fewer missed appointments

### Management impact
- improved visibility of unresolved booking work
- measurable process performance
- better use of reception staff time

---

## Suggested KPIs

Success could be measured using:

| KPI | Purpose |
|---|---|
| Average appointment enquiry response time | Measures service speed |
| Average admin handling time per request | Measures efficiency |
| % of enquiries handled without manual drafting | Measures automation level |
| No-show rate | Measures reminder effectiveness |
| Waitlist fill rate | Measures utilisation |
| Rescheduling turnaround time | Measures workflow speed |
| Patient satisfaction score | Measures service quality |
| AI output correction rate | Measures quality |
| Human escalation rate | Measures exception frequency |
| Incorrect booking rate | Measures operational safety |

---

## Risks and Limitations

### 1. Hallucination
AI may generate information not present in the source.

**Mitigation:**  
Prompts explicitly prohibit invention and require grounding in supplied information.

### 2. Privacy
Healthcare administration may involve sensitive patient information.

**Mitigation:**  
Use minimum necessary information, appropriate access controls, secure systems, and approved data-handling procedures.

### 3. Clinical scope creep
Patients may include symptoms or clinical questions in administrative messages.

**Mitigation:**  
The prompts prohibit diagnosis and treatment advice and require escalation to qualified clinical staff.

### 4. Incorrect scheduling data
If the source appointment system is outdated, AI-generated responses may also be wrong.

**Mitigation:**  
Use live scheduling data and final system validation.

### 5. Bias
Waitlist automation could become unfair if inappropriate criteria are used.

**Mitigation:**  
The waitlist prompt uses only approved administrative criteria and prohibits protected-characteristic or inferred clinical ranking.

### 6. Over-automation
Some cases require empathy, discretion, authority, or clinical judgement.

**Mitigation:**  
Maintain human review for exceptions and ambiguous cases.

---

## Responsible AI Position

This project proposes **AI-assisted administration**, not autonomous healthcare decision-making.

The AI may:
- extract
- classify administrative intent
- draft
- summarise
- check information
- suggest administrative next steps

The AI must not:
- diagnose
- recommend treatment
- interpret symptoms clinically
- prioritise patients based on inferred medical urgency
- override clinic policy
- resolve disputes autonomously
- make unsupported decisions from missing information

Human staff remain accountable for final decisions where judgement or authority is required.

---

## Repository Structure

```text
carelink-medical-centre-ai-prompt-library/
├── README.md
├── prompt-library.md
├── iteration-log.md
├── examples/
│   ├── appointment-extraction-test.md
│   ├── reminder-test.md
│   └── waitlist-test.md
└── screenshots/
    ├── prompt-lab-v1.png
    ├── prompt-lab-v2.png
    └── prompt-lab-v3.png
```

---

## How to Use This Repository

1. Open `prompt-library.md`.
2. Select the prompt for the required workflow.
3. Replace placeholders such as `{{patient_message}}` with test data.
4. Run the prompt in the selected AI or Prompt Lab environment.
5. Record the output and score.
6. Compare the result against the criteria in `iteration-log.md`.
7. Refine the prompt if required.
8. Save screenshots or test evidence in the repository.

---

## Iteration Evidence

The `iteration-log.md` file demonstrates how prompts evolved from:
- basic instructions
- to structured prompts
- to automation-ready prompts with safety, validation, privacy, and escalation controls.

This provides evidence of iterative prompt engineering rather than one-stage prompt creation.

---

## Suggested Management Pitch

The core recommendation is to introduce the prompt library as a **controlled pilot** within appointment administration.

A suitable implementation approach would be:

1. begin with low-risk tasks such as information extraction, confirmations, reminders, and FAQs
2. measure output accuracy and administrative time saved
3. maintain human review during the pilot
4. expand to rescheduling, cancellations, and waitlist support after validation
5. review privacy, governance, and clinic policies before broader deployment

The proposed solution should support staff rather than replace them.

---

## Assessment Alignment

This repository addresses the main assessment requirements by providing:

- a clearly defined business field
- a repetitive workflow suitable for automation
- 10 structured prompts
- the intended workflow for each prompt
- the problem being solved
- automation potential
- risks and limitations
- evidence of iterative improvement
- responsible AI analysis
- measurable business impact
- material suitable for a consultancy-style management pitch

---

## Note on Prompt Lab Scoring

The prompts were designed to perform strongly against common prompt-quality criteria by using:
- clear roles
- explicit tasks
- defined inputs
- detailed constraints
- predictable output formats
- grounding
- safety controls
- human escalation
- validation checks

However, a specific **90+ score cannot be guaranteed** because Prompt Lab scores can vary depending on the rubric, model, test cases, and evaluation settings. The strongest submission approach is to run the prompts, capture the scores, and include evidence showing how later versions improved over earlier ones.

---

## Author

**Student:** [Your Name]  
**Course:** AI in Business  
**Assessment:** AI Prompt Library for Workflow Automation  
**Business Field:** Healthcare Administration  
**Business Name:** CareLink Medical Centre
