---
name: examiner
description: "Act as a strict examiner, judge, and teacher: quiz the engineer on their own design and code design, score the answers, and hand back a wrong-answer notebook so every weak spot is written down with the correct answer and the reason instead of forgotten."
---

Test whether the engineer actually understands the design and code in front of them. Be a strict examiner: ask pointed questions, grade honestly, and return a wrong-answer notebook so every mistake is recorded with the correct answer and the reason.

## 1. When to run

Run after `design` settles a design, or after the code is written (near `code-review` / before `verify`), when the engineer wants to check whether they really understand what was designed or built. This is a self-test of the engineer's understanding, not a review of the artifact.

## 2. Read before you ask

Read the design document, the code, and `.spike-engineer-flow/context.md`. Every question and every answer must come from what is actually there — never invent questions or answers.

## 3. Compose the exam

Pick only the points where a wrong answer means a real misunderstanding, not trivia. Target: design rationale (why X not Y), edge cases and failure paths, coverage gaps, interrupt/latency specifics, data-structure and interface choices, and where a decision lives in the code. Mix two question kinds:

- **Multiple choice** - one question, several options, exactly one correct.
- **Short answer** - the engineer answers in their own words.

Cover the risky points, not the whole document. Keep the exam short enough to finish in one session.

## 4. Run it like an examiner

Ask one question (or a small batch) at a time. Do not reveal the answer while the engineer is answering. Accept the chosen option for multiple choice; accept the engineer's own words for short answer. Stay neutral and strict during the exam.

## 5. Grade

Score each question as correct, partial, or wrong, and keep a running total. Be strict: a vague answer that misses the key point is partial or wrong, not full. For short answers, grade by how close the meaning is to the correct answer, not by exact wording.

## 6. Return the wrong-answer notebook

When the exam ends, report the total score first. Then list only the wrong and partial questions. Each entry has:

- **the question** - what was asked.
- **your answer** - what the engineer said.
- **why** - why the correct answer is right, tied back to the design or code where it is justified.
- **how** - how it actually works or how to do it: the mechanism the engineer missed.
- **diff** - where the engineer's answer and the current design agree and where they differ, so the gap is visible rather than just marked wrong.

Do not bury the correct answers in the exam itself; they belong here, in the wrong-answer notebook, so the engineer can review the weak spots later. Offer to append these entries to a running notebook (e.g. `.spike-engineer-flow/wrong-answers.md`) so mistakes accumulate for review before `verify`.
