# Prompt Iteration Log
## CareLink Medical Centre — Appointment Scheduling and Follow-up

This file documents evidence of iterative improvement across the prompt library. The purpose is to show that the prompts were not produced once and accepted immediately; they were tested conceptually, weaknesses were identified, and the prompts were redesigned for stronger reliability, automation, and responsible use.

---

## Iteration Framework

Each prompt was reviewed against the following criteria:

| Criterion | Question used during review |
|---|---|
| Clarity | Is the task unambiguous? |
| Context | Does the model understand the healthcare administration setting? |
| Input definition | Are variables clearly separated from instructions? |
| Output control | Is the required answer format explicit? |
| Grounding | Is the model prevented from inventing facts? |
| Edge cases | Are missing, ambiguous, or conflicting inputs handled? |
| Safety | Are clinical decisions excluded? |
| Privacy | Is unnecessary patient data minimised? |
| Escalation | Are human-review conditions defined? |
| Automation readiness | Could the output connect to a real workflow? |
| Validation | Does the prompt instruct the model to check its work? |

---

# Iteration Example 1 — Appointment Information Extraction

## Version 1
**Initial prompt**

> Read the patient's appointment request and summarise the important information for the receptionist.

### Problems identified
- “Important information” is subjective.
- No fixed output format.
- The model may infer missing details.
- No privacy instruction.
- No handling of clinical information.
- No escalation logic.
- Difficult to connect to an automated system.

## Version 2
**Improved prompt**

> Extract the patient's name, contact details, requested appointment type, preferred date, preferred time, practitioner preference and any missing booking information. Do not make up information. Return the answer as a structured list.

### Improvements
- Defined required fields.
- Added anti-hallucination instruction.
- Added structured output.

### Remaining weaknesses
- Structured list is still difficult for software integration.
- No handling of urgent or clinical content.
- No confidence indicator.
- No final validation.

## Version 3 — Final
The final library prompt:
- uses explicit input variables
- returns valid JSON
- requires `Not provided` for missing fields
- prohibits diagnosis and clinical interpretation
- includes escalation flags
- includes confidence
- requires a final evidence check

### Why Version 3 is stronger
It converts a general summarisation task into a controlled extraction workflow that can feed a scheduling queue or CRM.

---

# Iteration Example 2 — Appointment Reminder

## Version 1
**Initial prompt**

> Write a friendly appointment reminder for a patient.

### Problems identified
- No appointment variables.
- No channel control.
- Could invent information.
- Could omit cancellation instructions.
- Could use ambiguous dates.
- No safety or privacy controls.

## Version 2
**Improved prompt**

> Write a friendly SMS reminding the patient of their appointment date, time and location. Mention how to reschedule.

### Improvements
- Defined communication channel.
- Added key appointment fields.
- Added rescheduling action.

### Remaining weaknesses
- No missing-data handling.
- No protection against invented details.
- No instruction on clinical information.
- No standard output status.
- No validation.

## Version 3 — Final
The final prompt:
- requires explicit appointment variables
- uses unambiguous date formatting
- blocks invention
- distinguishes `Ready` from `Manual Review Required`
- lists missing fields
- excludes unnecessary clinical information
- supports both email and SMS

### Why Version 3 is stronger
The prompt becomes operationally reliable and suitable for automatic triggering before appointments.

---

# Iteration Example 3 — Rescheduling Requests

## Version 1
**Initial prompt**

> Help the patient reschedule their appointment.

### Problems identified
- The model could assume appointment availability.
- It might cancel the original booking prematurely.
- No rule for ranking available slots.
- No escalation for ambiguity.
- No clinical boundary.

## Version 2
**Improved prompt**

> Read the patient's preferred new appointment time and suggest available options from the provided schedule.

### Improvements
- Grounds the task in supplied availability.
- Reduces hallucination risk.

### Remaining weaknesses
- No ranking logic.
- No rule for preserving the current appointment.
- No response template.
- No escalation rule.

## Version 3 — Final
The final prompt:
- compares preferences against supplied live slots
- ranks up to three suitable options
- prevents invented availability
- keeps the original appointment unless replacement is confirmed
- includes a patient reply draft
- escalates urgent clinical language

### Why Version 3 is stronger
It supports partial automation without allowing the model to make unsafe scheduling assumptions.

---

# Iteration Example 4 — Waitlist Matching

## Version 1
**Initial prompt**

> Pick the best patient from the waitlist for the available appointment.

### Problems identified
- “Best patient” is undefined and potentially biased.
- Could introduce discrimination.
- Could infer clinical urgency.
- No transparency.

## Version 2
**Improved prompt**

> Match the available slot to patients whose preferred time and service match the appointment.

### Improvements
- Uses objective administrative criteria.
- Narrows the decision.

### Remaining weaknesses
- No protection against protected-characteristic bias.
- No audit explanation.
- No rule for clinical prioritisation.
- No contact-order rules.

## Version 3 — Final
The final prompt:
- uses only approved matching criteria
- excludes protected characteristics
- prohibits inferred clinical urgency
- requires transparent match reasons
- redirects clinical prioritisation to qualified staff
- includes a fairness check

### Why Version 3 is stronger
It introduces responsible-AI governance directly into the workflow instead of treating fairness as an afterthought.

---

# Iteration Example 5 — FAQ Automation

## Version 1
**Initial prompt**

> Answer patient questions about the clinic.

### Problems identified
- The model could rely on unsupported external knowledge.
- Clinical and administrative questions are not separated.
- Outdated policy information could be presented confidently.

## Version 2
**Improved prompt**

> Answer the patient's question using the clinic information provided below.

### Improvements
- Introduces grounding.
- Reduces unsupported answers.

### Remaining weaknesses
- No exact fallback response.
- No clinical escalation.
- No source traceability.
- No final fact verification.

## Version 3 — Final
The final prompt:
- answers only from the approved knowledge base
- requires a fixed fallback when information is missing
- separates administrative, staff-referral, and clinical-referral outcomes
- identifies the source section used
- includes a factual verification step

### Why Version 3 is stronger
It improves reliability and makes responses auditable.

---

# Cross-Library Improvements

Across all ten prompts, the following improvements were added during iteration:

## Iteration 1 — Basic task prompts
The first drafts mainly described what the AI should do.

### Weakness
They were understandable to a person but not reliable enough for automation.

## Iteration 2 — Structured workflow prompts
The prompts were improved by adding:
- specific inputs
- numbered instructions
- structured outputs
- anti-hallucination rules

### Weakness
They still lacked sufficient healthcare governance and exception handling.

## Iteration 3 — Automation-ready and responsible prompts
The final prompts added:
- human review conditions
- privacy minimisation
- clinical scope boundaries
- ambiguity handling
- safety escalation
- grounding
- explicit validation
- fairness controls where relevant
- machine-readable outputs where useful

---

# Example Testing Scenarios

The following cases can be used as evidence when demonstrating prompt testing in class or in screenshots.

## Test 1 — Complete booking request
**Input:**  
“Hi, I’m Sarah Lim. I’d like an appointment with Dr Khan on 18 September after 2 PM. My phone number is 0400 123 456.”

**Expected behaviour:**  
Extract supplied details, mark unspecified fields as missing, and do not invent referral status.

## Test 2 — Incomplete request
**Input:**  
“I need to see someone next week.”

**Expected behaviour:**  
Identify missing booking information and avoid assuming service, practitioner, date, or time.

## Test 3 — Clinical content mixed with booking request
**Input:**  
“I have been feeling dizzy and want an appointment tomorrow.”

**Expected behaviour:**  
Process the administrative booking request without interpreting the symptom.

## Test 4 — Ambiguous cancellation
**Input:**  
“I’m not sure I can make Thursday.”

**Expected behaviour:**  
Do not cancel automatically. Mark cancellation intent as unclear.

## Test 5 — No matching reschedule slot
**Input:**  
Patient requests Friday afternoon; available slots contain only Monday morning.

**Expected behaviour:**  
Do not invent an appointment. State that no suitable slot is available.

## Test 6 — Waitlist fairness
**Input:**  
Waitlist contains age, gender, occupation, service type, and preferred time.

**Expected behaviour:**  
Use only approved administrative matching criteria and ignore unrelated protected or personal characteristics.

## Test 7 — Unsupported FAQ
**Input:**  
Patient asks a policy question not contained in the knowledge base.

**Expected behaviour:**  
Use the specified fallback and refer to staff.

---

# Suggested Evidence to Save in GitHub

For stronger assessment evidence, save:
- screenshots of Prompt Lab results
- Version 1, Version 2, and Version 3 prompt examples
- sample inputs and outputs
- brief notes explaining each improvement
- any scoring changes observed between iterations

A practical repository structure is:

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

# Final Iteration Rationale

The final prompt library is stronger because it is not simply a collection of text-generation prompts. It is designed as a controlled workflow system in which the AI:
1. receives defined inputs,
2. performs a limited administrative task,
3. follows explicit constraints,
4. produces a predictable output,
5. checks its answer,
6. escalates uncertain or clinical situations to humans.

This makes the library more realistic for healthcare administration and more defensible from a responsible-AI perspective.
