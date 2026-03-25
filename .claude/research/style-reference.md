# Style Reference Guide

This file contains real excerpts from three reference pieces, organized by writing pattern.
The editorial agent reads this before revising any paper. Match the rhythm and structure of
these examples — not by copying, but by using them as direct templates.

**Reference pieces:**
- **PG** — Paul Graham, "How to Do Great Work" (paulgraham.com/greatwork.html)
- **SA** — Leopold Aschenbrenner, "Situational Awareness: The Decade Ahead" (situational-awareness.ai)
- **Altman** — Sam Altman, "How To Be Successful" (blog.samaltman.com/how-to-be-successful)

---

## Pattern 1: Opening a Section

The first sentence states the claim. No warmup, no scene-setting, no "in this section we will explore."
The reader learns the point immediately, then the paragraph earns it.

**Examples:**

> "Compounding is magic. Look for it everywhere. Exponential curves are the key to wealth generation."
> — Altman, §1

> "Self-belief is immensely powerful. The most successful people I know believe in themselves almost to the point of delusion."
> — Altman, §2

> "Focus is a force multiplier on work."
> — Altman, §6

> "You get truly rich by owning things that increase rapidly in value."
> — Altman, §12

> "The first step is to decide what to work on. The work you choose needs to have three qualities: it has to be something you have a natural aptitude for, that you have a deep interest in, and that offers scope to do great work."
> — PG

> "AGI by 2027 is strikingly plausible. GPT-2 to GPT-4 took us from ~preschooler to ~smart high-schooler abilities in 4 years."
> — SA

**Why it works:** The reader knows what they're about to read. They either agree or disagree — either way, they keep reading. The claim does the work a headline used to do.

**Anti-pattern to avoid:**
> ❌ "In this section, we examine the role that compounding plays in wealth generation and career development, with particular attention to how exponential curves differ from linear trajectories."

---

## Pattern 2: Grounding an Abstraction with a Named Example

Every abstract claim needs one concrete anchor: a company name, a person, a specific number, a dated event.
The example doesn't just illustrate — it makes the claim checkable.

**Examples:**

> "I remember when Elon Musk took me on a tour of the SpaceX factory many years ago. He talked in detail about manufacturing every part of the rocket, but the thing that sticks in memory was the look of absolute certainty on his face when he talked about sending large rockets to Mars. I left thinking 'huh, so that's the benchmark for what conviction looks like.'"
> — Altman (grounding: "self-belief almost to the point of delusion")

> "Airbnb is my benchmark for this. There are so many stories they tell that I wouldn't recommend trying to reproduce (keeping maxed-out credit cards in those nine-slot three-ring binder pages kids use for baseball cards, eating dollar store cereal for every meal, battle after battle with powerful entrenched interest, and on and on) but they managed to survive long enough for luck to go their way."
> — Altman (grounding: "be willful — keep going until it works")

> "Write the story you want to read; build the tool you want to use."
> — PG (grounding: "make something people actually want")

> "Knowledge expands fractally, and from a distance its edges look smooth, but once you learn enough to get close to one, they turn out to be full of gaps."
> — PG (grounding: "learn enough to reach the frontier")

> "Over the past year, the talk of the town has shifted from $10 billion compute clusters to $100 billion clusters to trillion-dollar clusters."
> — SA (grounding: "massive industrial mobilization is underway")

> "GPT-2 to GPT-4 took us from ~preschooler to ~smart high-schooler abilities in 4 years."
> — SA (grounding: "AGI timeline is plausible")

**Why it works:** A named company, person, or dollar figure makes the abstract claim falsifiable. The reader can check it. That's what makes the argument feel honest rather than rhetorical.

**Anti-pattern to avoid:**
> ❌ "Many successful founders demonstrate exceptional self-belief and willingness to persist through adversity."

---

## Pattern 3: The Non-Consensus Thesis

The paper's core argument should be a claim that a smart person might disagree with.
If everyone already believes it, it isn't worth writing. State it plainly, early, without hedging.

**Examples:**

> "AGI by 2027 is strikingly plausible."
> — SA (non-consensus when written; stated as flat claim, not possibility)

> "The biggest economic misunderstanding of my childhood was that people got rich from high salaries."
> — Altman (opens by naming a common belief as wrong)

> "Most people get bogged down in linear opportunities."
> — Altman (implicit: most people are making a mistake you can avoid)

> "The trouble with planning is that it only works for achievements you can describe in advance. You can win a gold medal or get rich by deciding to as a child and then tenaciously pursuing that goal, but you can't discover natural selection that way."
> — PG (challenges the "have a plan" orthodoxy directly)

> "Boldly chase outlier ideas, even if other people aren't interested in them — in fact, especially if they aren't."
> — PG (inverts conventional wisdom: unpopularity is a signal, not a warning)

> "I believe that it's easier to do a hard startup than an easy startup."
> — Altman (deliberately counter-intuitive, then earns it)

**Why it works:** A non-consensus claim creates tension. The reader either wants to agree or to argue. Either way they read on.

**Anti-pattern to avoid:**
> ❌ "AI is transforming the financial services industry in significant ways, and companies that adapt will be well-positioned for the future."

---

## Pattern 4: Explaining a Technical Concept Without Jargon

Technical concepts get one clause of inline context, then are used freely. No footnotes. No separate glossary.
The analogy should come from something the reader already understands.

**Examples:**

> "GPT-2 to GPT-4 took us from ~preschooler to ~smart high-schooler abilities in 4 years."
> — SA (OOM gains → human development stages. No prior AI knowledge required.)

> "Hundreds of millions of AGIs could automate AI research, compressing a decade of algorithmic progress into ≤1 year."
> — SA (abstract scaling argument → concrete time compression)

> "an RLHF'd small model was equivalent to a non-RLHF'd >100x larger model"
> — SA (RLHF defined by its effect, not its mechanism)

> "Knowledge expands fractally, and from a distance its edges look smooth, but once you learn enough to get close to one, they turn out to be full of gaps."
> — PG (fractal geometry → epistemology, no math required)

> "I call this approach 'staying upwind.' This is how most people who've done great work seem to have done it."
> — PG (new term introduced, immediately explained by implication)

**Why it works:** The reader does not stop. They grasp the concept through the analogy, then encounter the term — by which point they already understand it.

**Anti-pattern to avoid:**
> ❌ "Reinforcement learning from human feedback (RLHF) is a technique used to align language model outputs with human preferences through iterative reward modeling."

---

## Pattern 5: Ending a Section with a Sharp Implication

The last sentence of a section should tell the reader what to do with what they just learned,
or sharpen the stakes. Not a summary — a conclusion that points forward.

**Examples:**

> "Trust the exponential, be patient, and be pleasantly surprised."
> — Altman (closing §1 on compounding — action + attitude in 8 words)

> "Hard work compounds like interest, and the earlier you do it, the more time you have for the benefits to pay off."
> — Altman (closing §7 — ties the section's claim to a specific implication)

> "Most people get bogged down in linear opportunities. Be willing to let small opportunities go to focus on potential step changes."
> — Altman (closing thought — tells you exactly what to do differently)

> "But always preserve excitingness."
> — PG (four words that close a long paragraph about evolving ambitions — compression is the point)

> "If you're interested, you're not astray."
> — PG (closing a section on staying true to your interests — epigrammatic)

> "You can win a gold medal or get rich by deciding to as a child and then tenaciously pursuing that goal, but you can't discover natural selection that way."
> — PG (closes the section against over-planning — the implication lands in the negative)

**Why it works:** The reader finishes the section knowing something they didn't know before, phrased in a way that sticks.

**Anti-pattern to avoid:**
> ❌ "In summary, this section has explored the importance of compounding and its relevance to career development. In the next section, we will examine the role of self-belief."

---

## Pattern 6: Urgency Without Hype

Urgency comes from specificity, not adjectives. Specific numbers and named events create more urgency
than words like "rapidly," "dramatically," or "unprecedented."

**Examples:**

> "Over the past year, the talk of the town has shifted from $10 billion compute clusters to $100 billion clusters to trillion-dollar clusters."
> — SA (the escalation IS the urgency — no "rapidly" needed)

> "Exponential curves are the key to wealth generation. A medium-sized business that grows 50% in value every year becomes huge in a very short amount of time."
> — Altman (50% is specific; "huge in a very short amount of time" earns its vagueness because the number anchored it)

> "I am willing to take as much time as needed between projects to find my next thing. But I always want it to be a project that, if successful, will make the rest of my career look like a footnote."
> — Altman (stakes are named; "footnote" is visceral)

> "Self-belief must be balanced with self-awareness. I used to hate criticism of any sort and actively avoided it. Now I try to always listen to it with the assumption that it's true."
> — Altman (personal admission creates urgency through honesty, not drama)

**Why it works:** The reader can picture it. Numbers and named facts bypass the part of the brain that filters out marketing language.

**Anti-pattern to avoid:**
> ❌ "AI capabilities are advancing at an unprecedented pace, with transformative implications for every industry."

---

## Pattern 7: Sentence Rhythm

Short sentences land claims. Longer sentences build reasoning. Never two long sentences in a row.

**Examples — notice the alternation:**

> "Compounding is magic. [short — claim] Look for it everywhere. [short — command] Exponential curves are the key to wealth generation. [medium — elaboration] A medium-sized business that grows 50% in value every year becomes huge in a very short amount of time. [long — evidence] Few businesses in the world have true network effects and extreme scalability. [medium — qualification] But with technology, more and more will. [short — implication]"
> — Altman, §1

> "The first step is to decide what to work on. [medium — claim] The work you choose needs to have three qualities: it has to be something you have a natural aptitude for, that you have a deep interest in, and that offers scope to do great work. [long — elaboration] In practice you don't have to worry much about the third criterion. [medium — qualification] Ambitious people are if anything already too conservative about it. [medium — surprising twist] So all you need to do is find something you have an aptitude for and great interest in. [medium — simplified conclusion]"
> — PG

**Why it works:** The short sentence after a long one feels like emphasis. The reader's eye rests on it.

---

## Pattern 8: What to Cut — Anti-Patterns With Examples

These patterns appear in first drafts. Cut them every time.

| Pattern | Example to cut | Why |
|---|---|---|
| Throat-clearing | "Before examining the competitive landscape, it is worth establishing the broader context in which these dynamics play out." | Says nothing. Start with the claim. |
| Academic hedge | "It seems possible that AI may play an increasingly significant role in financial services." | State it or don't. "AI is eating financial services compliance" is a claim. |
| Empty intensifier | "The transformative potential of this technology cannot be overstated." | Remove. Replace with a specific data point. |
| Transition recap | "Having established the market size and timing signals, we now turn to the competitive dynamics." | Just turn to it. |
| Passive voice | "It has been observed that..." / "Studies have shown that..." | Name the observer. Name the study. |
| Vague attribution | "Many experts believe..." / "Industry observers have noted..." | Name one expert. Quote them. |
| Balanced non-conclusion | "While there are arguments on both sides, the truth likely lies somewhere in the middle." | This is the opposite of a thesis. Take a position. |

---

## Tone Calibration: Who Is Reading This

The reader is one of:
- An **a16z GP** — has seen 1000 pitches, reads fast, allergic to buzzwords, rewards non-consensus
- A **Stripe/Coinbase product leader** — wants to know what's happening in their market right now, named competitors, specific numbers
- A **SV founder** — wants to know what to build and why now
- An **AI/fintech operator** — technically literate, wants mechanism not vibes

They all share: **high pattern recognition, low tolerance for filler, hunger for something they don't already know.**

Write to the person who will put the paper down if the first page doesn't earn their attention.
The Altman and PG essays hold this reader because every paragraph contains at least one thing they haven't heard stated that cleanly before. That's the standard.
