# Instructor Reference: Session 2.2 — AI for Documents and Research

[Duration: 90 min teaching (5 segments) + 10 min Common Mistakes + 2×5-min breaks + 10 min final recap block = 120 min total | Domain: Mixed (conceptual framing + hands-on with live AI chat tools) | Tools: ChatGPT (Free), Claude (Free), Gemini (Free) | Prior: Prompting Patterns: Chaining, Critique and Personas (2.1) | Next: Colab, Variables and Condition Logic (3.1) | Visual load: Medium]

> **Note for the Industry Mentor — Tracked Learning Objectives for This Session:**
> This session is formally tracked against the following LO Statements from the curriculum LO bank. Please ensure each one gets substantive, identifiable coverage during delivery — a student should be able to point to the specific moment each was taught:
> - **PROMPT-024:** Write a prompt that instructs the model to answer only from supplied reference text
> - **LLM-028:** Describe a model's knowledge cutoff and its effect on recent-fact questions
> - **LLMEVAL-013:** Classify a generated claim as grounded in or unsupported by the provided context

**Goal:** Turn a free AI chat tool into a reliable document-research assistant — grounded to the source, cutoff-aware, and fact-checked before use.

**Student profile:** A learner who can already chain and template prompts from last session, but hasn't yet uploaded a real document and restricted a model's answer to it.

**Key outcome:** By the end, a student can upload a document, write a grounded prompt restricted to it, flag when a knowledge-cutoff risk applies to a question, and classify a generated claim as grounded or unsupported.

---

## SEGMENT 1 — Uploading and Summarising a Document Inside a Free AI Chat Tool `(18 min)`

> Instructor note: Last session (2.1) covered chaining, self-critique, and templates for conversational prompting. Today assumes a real document enters the picture for the first time.

**Hook-in** `(30 sec)`
Everything so far has been typed questions. What happens the moment you hand the model an actual file instead?

**Concept** `(3–5 min)`
Handing a colleague a 40-page report and asking "can you summarise this for me by tomorrow" gets you a usable summary only if you also say what to focus on and how long you want it. **Most free AI chat tools let you attach a document directly to the conversation, after which the model can read its contents the same way it reads typed text — but a vague summarisation request still returns an unpredictable result.** This matters because the upload step and the instruction step are two separate actions, and skipping the second one is the single most common reason a first attempt disappoints.

**Visual** `(visual only, no extra time)`
```
VAGUE REQUEST:
"Summarise this."
-> length and focus are whatever the model guesses

SPECIFIC REQUEST:
"Summarise this report in 150 words for someone who has
 never read it, focusing on the recommendations section."
-> length, audience, and focus are all fixed in advance
```
> **Say while pointing:** "The file only gets you into the room — the specific request on the second line is what actually controls what comes back out."

**Implementation / Demonstration** `(5–10 min)`
Live demo: the instructor uploads a short public report (or sample PDF) into a free chat tool and runs the vague request first, then the specific one, comparing both outputs on screen.

Expected:
```
Vague request:    a generic-length summary, uneven focus, no
                   clear audience assumed
Specific request: exactly the requested length, organised around
                   the recommendations section specifically
```

**Key point**
**Uploading a document only gives the model access to it — the summary's length, audience, and focus still have to be stated explicitly in the prompt.**

**Room check** `(30 sec)`
> **Ask:** "You've uploaded a 10-page research paper and want a summary a non-expert could follow in under a minute of reading. What two things does your prompt need to specify?"
> **Answer:** A word/length limit, and an explicit non-expert audience — without both, the summary may be too long or too technical.

**Student try** `(2–3 min)`
Using any document you have on hand (or a public PDF/article), write one summarisation prompt that specifies length, audience, and a focus area, all in a single request.

Success: The written prompt names a specific length, a specific audience, and a specific focus — not a bare "summarise this."

---

## SEGMENT 2 — Grounding a Prompt: Answering Only From What Was Uploaded `(18 min)`

**Hook-in** `(30 sec)`
The model now has your document — but it also still has everything it learned during training. How do you make sure its answer comes only from your file?

**Concept** `(3–5 min)`
Asking a lawyer "what does this contract say about termination" without telling them to ignore everything else they know about contract law in general risks getting an answer that blends the actual clause with general legal knowledge. **Grounding means explicitly instructing the model to answer only using the supplied reference text, and to say so if the answer isn't present in it, rather than filling the gap from general knowledge.** This matters because an ungrounded answer can look exactly as confident and well-formatted as a grounded one, with no visible difference in tone.

**Visual** `(visual only, no extra time)`
```
UNGROUNDED PROMPT:
"What does this contract say about termination notice?"
-> may silently blend the actual clause with generic
   contract-law knowledge the model already has

GROUNDED PROMPT:
"Using ONLY the attached contract, what does it say about
termination notice? If it isn't covered in this document,
say so explicitly — do not use outside knowledge."
-> restricted to the document; a missing clause is
   reported as missing, not invented
```
> **Say while pointing:** "'Using only the attached contract' is the exact phrase doing the restricting — remove it, and the model is free to blend in outside knowledge."

**Implementation / Demonstration** `(5–10 min)`
Live demo: the instructor asks an ungrounded question against an uploaded sample document, then re-asks the same question with explicit grounding language, comparing whether either answer cites outside knowledge not in the file.

Expected:
```
Ungrounded answer: includes at least one general-knowledge
                    statement not actually present in the
                    uploaded document
Grounded answer:    restricted to document content, and
                    explicitly flags anything the document
                    doesn't cover
```

**Key point**
**"Using only the attached document" is the specific instruction that triggers grounding — a bare upload plus a bare question does not.**

**Room check** `(30 sec)`
> **Ask:** "You uploaded a syllabus and asked 'when is the deadline for the final project?' The model gave a confident date. How do you check whether that answer was actually grounded?"
> **Answer:** Re-read the syllabus yourself and confirm that exact date appears in it — a confident tone is not proof the date came from the document.

**Student try** `(2–3 min)`
Take your Segment 1 document and write one grounded version of a question about it, explicitly restricting the model to the document and asking it to flag anything not covered.

Success: The prompt includes an explicit restriction phrase ("using only," "based solely on") and an instruction to flag missing information.

---

## Break 1 `(5 min)`

Re-entry hook: "You can now get a summary and a grounded answer from a document. Next: what happens when the question you're asking is about something more recent than the document — or the model itself — knows?"

---

## SEGMENT 3 — Knowledge Cutoff: Why the Model Can Be Confidently Out of Date `(18 min)`

**Hook-in** `(30 sec)`
You ask a grounded, well-phrased question and get a confident, specific-sounding answer. Is a confident answer always a current one?

**Concept** `(3–5 min)`
A textbook printed two years ago can describe last decade's topic perfectly while being completely silent on anything that happened after it went to print — not because it's wrong, but because it was finished before that event occurred. **A model's knowledge cutoff is the date after which it has no training data, so it cannot reliably know about events, prices, or facts that occurred after that point — and it will often still answer confidently instead of declining.** This matters for research tasks specifically, because a question like "what is the latest version of this tool" or "who currently holds this role" is exactly the kind a cutoff silently breaks.

**Visual** `(visual only, no extra time)`
```
Model's knowledge cutoff: [a stated past date]
Question: "What is the latest version of this software?"
-> answer reflects whatever was true AS OF the cutoff date,
   not necessarily what's true today
-> the model may not flag this gap unless asked to
```
> **Say while pointing:** "The gap between the cutoff date and today is exactly where an answer can be stale without sounding stale."

**Implementation / Demonstration** `(5–10 min)`
Live demo: the instructor asks the chat tool directly for its own knowledge cutoff date, then asks a deliberately time-sensitive question ("what is the newest version of [a fast-moving tool]") and checks the answer against the stated cutoff.

Expected:
```
Stated cutoff:     a specific past date, given directly when asked
Time-sensitive Q:   answer reflects information as of (or before)
                    that cutoff date, not necessarily current
                    real-world state
```

**Key point**
**A confident tone is not evidence of a recent, accurate answer — always check whether a question is newer than the model's stated cutoff before trusting a date-sensitive answer.**

**Room check** `(30 sec)`
> **Ask:** "Which of these two questions is most at risk from a knowledge-cutoff problem: 'explain how photosynthesis works' or 'who is this company's current CEO'?"
> **Answer:** The CEO question — it depends on a fact that can change after the cutoff, while photosynthesis is stable, well-established science unlikely to have changed.

**Student try** `(2–3 min)`
Ask your chat tool for its own stated knowledge cutoff, then write one question you were about to ask it that is now clearly at risk of being outdated because of that cutoff.

Success: The student reports an actual stated cutoff date and names one specific, plausible question that depends on information newer than it.

---

## SEGMENT 4 — Fact-Checking: Classifying a Claim as Grounded or Unsupported `(18 min)`

**Hook-in** `(30 sec)`
Grounding restricts the model's source. Knowledge cutoff flags staleness. Is there still a way the model's answer can be wrong even after both of those are handled?

**Concept** `(3–5 min)`
A grounded, cutoff-aware answer can still misread a document, generalise a single number into a trend, or state something the document only implies rather than says outright — the same way a rushed human summary can drift from its source without anyone intending it to. **Fact-checking means taking each individual claim the model produced and checking it directly against the source document, sorting each one into grounded (the document actually states or clearly supports this) or unsupported (the document doesn't say this, even if it sounds plausible).** This matters because an unsupported claim embedded inside an otherwise accurate summary is the hardest kind of error to catch — everything around it reads correctly.

**Visual** `(visual only, no extra time)`
```
CLAIM: "The report recommends expanding into three new regions."
CHECK: Does the report's actual text name three regions and
       recommend expansion?
-> GROUNDED if yes
-> UNSUPPORTED if it only discusses one region, or doesn't
   recommend expansion at all
```
> **Say while pointing:** "Fact-checking happens claim by claim, not paragraph by paragraph — one sentence can be grounded while the next, right beside it, isn't."

**Implementation / Demonstration** `(5–10 min)`
Live demo: the instructor takes a grounded summary generated earlier in the session, breaks it into 3–4 individual claims, and checks each one directly against the source document line by line.

Expected:
```
Claim 1: GROUNDED — exact figure appears in the source text
Claim 2: GROUNDED — recommendation is explicitly stated
Claim 3: UNSUPPORTED — document discusses the topic but
         never states the specific number the model gave
```

**Key point**
**Read the model's output one claim at a time, not as a single block — a paragraph can be mostly grounded and still contain one invented detail.**

**Room check** `(30 sec)`
> **Ask:** "A grounded summary says 'the company's revenue grew significantly last year,' but the source document never gives a revenue figure at all. Grounded or unsupported?"
> **Answer:** Unsupported — "significantly" implies a specific trend that the document doesn't actually state or quantify anywhere.

**Student try** `(2–3 min)`
Take the grounded answer you generated in Segment 2, split it into its individual claims, and classify each one as grounded or unsupported against the actual document text.

Success: At least two distinct claims are identified and each is explicitly labelled grounded or unsupported with a one-line reason.

---

## Break 2 `(5 min)`

Re-entry hook: "Upload, ground, check the cutoff, fact-check the claims — four separate habits. The last stretch puts all four together in one real research task, start to finish."

---

## SEGMENT 5 — Putting It Together: A Full Grounded Research Workflow `(18 min)`

**Hook-in** `(30 sec)`
You now have four separate skills. What does it look like to run all four, in order, on one real task?

**Concept** `(3–5 min)`
A researcher preparing a briefing doesn't summarise, then separately ground, then separately fact-check as disconnected one-off steps — they run through the same sequence every time a new document lands on their desk, the same way a chef runs the same mise-en-place steps before every dish regardless of what's being cooked. **A repeatable document-research workflow runs four steps in order: upload the document, write a grounded prompt restricted to it, flag any part of the question that risks the model's knowledge cutoff, and fact-check every resulting claim against the source before using it.** This matters because any one step skipped reintroduces the exact risk the other three were built to prevent.

**Visual** `(visual only, no extra time)`
```
1. UPLOAD    -> attach the actual source document
2. GROUND    -> "using only the attached document..."
3. CUTOFF    -> flag anything time-sensitive vs. the stated cutoff
4. FACT-CHECK -> classify each claim: grounded or unsupported
```
> **Say while pointing:** "Four boxes, always in this order — skip box 2 and box 4 catches more errors; skip box 4 and nothing catches the errors that remain."

**Implementation / Demonstration** `(5–10 min)`
Live demo: the instructor runs a full end-to-end example — uploading a short public document, writing a grounded summarisation prompt, checking one date-sensitive claim against the stated cutoff, and fact-checking the final output claim by claim.

Expected:
```
Step 1 (upload):      document attached and confirmed readable
Step 2 (ground):       summary restricted to document content
Step 3 (cutoff check): one claim flagged as cutoff-risky,
                        verified or caveated accordingly
Step 4 (fact-check):   each remaining claim labelled grounded
                        or unsupported
```

**Key point**
**The four steps only work as a sequence — upload, ground, cutoff-check, fact-check — run in that order, every time, regardless of how confident the output looks.**

**Room check** `(30 sec)`
> **Ask:** "A classmate grounds their prompt and fact-checks the output, but skips the knowledge-cutoff check entirely. What specific kind of error could still slip through?"
> **Answer:** A claim that's genuinely stated in the document but is itself now outdated (e.g. a role, a price, a version number) — grounding and fact-checking against the document won't catch staleness the document itself already has.

**Student try** `(2–3 min)`
Pick any short document and run the full four-step workflow on one question about it, writing down what happened at each of the four steps.

Success: All four steps are shown in order with at least one concrete observation per step (what was uploaded, the grounding phrase used, the cutoff risk noted, and at least one claim classified).

---

## SEGMENT 6 — Common Mistakes `(10 min)`

### Mistake 1: Treating the Upload Itself as Grounding

**Wrong:**
Uploading a document and assuming the model will automatically restrict its answer to it, with no explicit grounding instruction.

**Right:**
Always add an explicit restriction phrase — "using only the attached document" — every time the answer needs to be grounded (Segment 2).

**Why it matters:**
Without the phrase, the model is free to blend in outside knowledge, and nothing in the output visibly signals that it has.

---

### Mistake 2: Trusting a Confident Answer to a Time-Sensitive Question

**Wrong:**
Asking about a current price, version, or role-holder and accepting the answer at face value because it sounds specific and certain.

**Right:**
Check the question against the model's stated knowledge cutoff first (Segment 3) — a confident tone is not evidence the answer is current.

**Why it matters:**
This is the single most common way a research answer looks polished but is quietly wrong.

---

### Mistake 3: Fact-Checking the Summary as One Block

**Wrong:**
Reading an entire grounded summary once and accepting it as a whole because most of it checks out.

**Right:**
Break the output into individual claims and check each one separately against the source (Segment 4) — grounded and unsupported claims can sit side by side in the same paragraph.

**Why it matters:**
A single invented detail hides easily inside an otherwise accurate summary when checked only at a glance.

---

### Mistake 4: Running the Four Steps Out of Order or Skipping One

**Wrong:**
Fact-checking the output but never having grounded the prompt in the first place, or grounding carefully but skipping the cutoff check entirely.

**Right:**
Run all four steps, in order, every time (Segment 5) — each step catches a different failure the others don't.

**Why it matters:**
Skipping any one step reopens exactly the risk that step exists to close, no matter how carefully the other three were done.

---

## SEGMENT 7 — Session Recap

| Learning Outcome | What to Remember |
|---|---|
| Write a prompt that instructs the model to answer only from supplied reference text | The phrase "using only the attached document" is what triggers grounding — uploading alone does not restrict the model |
| Describe a model's knowledge cutoff and its effect on recent-fact questions | A confident tone is not evidence of a recent answer — always check a time-sensitive question against the stated cutoff date |
| Classify a generated claim as grounded in or unsupported by the provided context | Check claim by claim, not paragraph by paragraph — a mostly-accurate summary can still contain one unsupported detail |

**Path forward:**
Next session is **Colab, Variables and Condition Logic (3.1)** — it moves from prompting an AI tool conversationally into writing your own Python code in Google Colab, starting with running a cell, storing values in variables, and branching with if/else.

---

## Knowledge Check

Five scenario-based questions covering grounding, knowledge cutoff, and fact-checking — use these as a closing quiz, a cold-call set, or a take-home check.

**1.** A student uploads their college's fee-refund policy PDF and asks: "What does this document say about the refund deadline?" with no further instruction. The model answers confidently with a specific date. What is missing from this prompt, and why does that matter here specifically?

> **Answer:** The prompt has no explicit grounding instruction (e.g. "using only the attached document"), so the date given isn't guaranteed to come from the PDF at all — it could be blended with general knowledge about refund policies elsewhere. The fix is adding the restriction phrase and asking the model to flag it if the deadline isn't actually stated.

**2.** A user grounds a prompt carefully — "using only the attached document, what is this product's current price?" — and gets a precise, confident price back. The document is a product brochure dated two years ago. Is this answer trustworthy? Why or why not?

> **Answer:** Not necessarily — the grounding worked correctly (the price did come from the document), but the document itself is two years old, so the price it states may no longer be current. Grounding guarantees the answer matches the source; it doesn't guarantee the source itself is still accurate today.

**3.** You ask a chat tool, "Who is the current CEO of [a company]?" without uploading anything. It gives a specific name immediately. What should you check before using that name in a report, and why?

> **Answer:** Check the question against the model's stated knowledge cutoff — a CEO can change after that date, so the name given may reflect who held the role as of the cutoff, not necessarily today. This is exactly the kind of fact that can go stale silently.

**4.** A model produces this grounded summary from an uploaded research paper: "The study surveyed 500 participants and found that remote work significantly improves productivity." Classify this as fully grounded, fully unsupported, or mixed — and explain your classification.

> **Answer:** Likely mixed — the "500 participants" figure may be directly grounded if that number literally appears in the paper, but "significantly improves productivity" is a strong, specific claim that needs its own check: if the paper reports a modest or mixed effect rather than a clear, significant improvement, that part of the claim would be unsupported even though the participant count is accurate.

**5.** A teammate says: "I always fact-check my AI summaries by rereading the whole thing once and seeing if it feels right." What is the gap in this approach, and what should they do instead?

> **Answer:** Rereading the whole summary at once is likely to miss a single unsupported detail embedded inside an otherwise accurate paragraph, since the surrounding accurate text makes the whole thing feel trustworthy. They should instead break the summary into individual claims and check each one separately against the source document.

**6.** A student uploads a syllabus and asks a grounded question about the grading breakdown, gets a correct, well-cited answer, and stops there, calling the task complete. Which of the four workflow steps from Segment 5 did they actually use, and which (if any) did this particular task not need?

> **Answer:** They used upload and grounding, and implicitly fact-checked by confirming the answer was well-cited to the source. The knowledge-cutoff step mattered least here, since a syllabus's grading breakdown for an ongoing course is unlikely to be the kind of fact a training cutoff would affect — though it's still worth a quick check if the syllabus could have been revised after the document was created.

**7.** Two students ground the same prompt against the same uploaded contract: Student A writes "based on this document, when can either party terminate the agreement?" and Student B writes "using only the attached contract, when can either party terminate the agreement — if this isn't covered, say so explicitly." Whose prompt gives you more confidence in the answer, and why?

> **Answer:** Student B's — it includes both an explicit restriction ("using only") and an instruction to flag missing information. Student A's phrasing ("based on this document") is weaker grounding language and doesn't tell the model what to do if the contract is silent on termination, leaving more room for an invented or blended answer.
