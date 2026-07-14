# Prompt Arena — Live Strategy Comparator

A tiny web tool that shows you how the **same AI model** can give different results depending on **how you ask it** the question.

You paste in any piece of text (a review, a tweet, a news update — anything), and the tool asks the AI to figure out its sentiment (Positive / Negative / Neutral) **three separate times**, using three different "asking styles." You see all three answers side by side, along with how long each took and how much it cost in tokens.

---

## Why this exists (the simple version)

If you're building anything with AI, you have to write instructions ("prompts") telling it what to do. But there's no single "correct" way to write a prompt — and picking the wrong style quietly costs you speed, money, or accuracy.

This tool lets you **see** that tradeoff instead of just guessing.

---

## The 3 strategies, explained like you're new here

Same AI. Same question. Three different levels of "help" given to it.

### 1. Zero-Shot — "Just answer, no help given"
The AI gets the bare question, nothing else.
- ✅ Fastest, cheapest
- ⚠️ Can miss subtle or tricky cases

### 2. Few-Shot — "Here are 3 examples, now you try"
Before asking, we show the AI 3 worked examples (one positive, one negative, one neutral) so it knows the pattern we want.
- ✅ More consistent answers
- ⚠️ Slightly slower and pricier (the examples get sent every time)

### 3. Chain-of-Thought (CoT) — "Think it through step-by-step first"
We tell the AI to reason out loud — spot the facts, spot the emotional language, then decide — before giving its final answer.
- ✅ Usually the most accurate on tricky, nuanced text
- ⚠️ Slowest and most expensive (it "thinks" more, which costs tokens)

---

## How to read the results on screen

Each of the 3 cards shows:

| What you see | What it means |
|---|---|
| Colored badge (green/red/yellow) | The sentiment verdict: Positive / Negative / Neutral |
| Latency | How many seconds that strategy took to respond |
| Prompt tokens | How much text was sent *to* the AI (your input + instructions) |
| Completion tokens | How much text the AI sent *back* |
| Total tokens | The sum — this is basically "what you'd be billed for" |
| Reasoning box | The AI's own explanation for its answer |
| 🥇 Gold ribbon | Marks whichever strategy responded fastest |

---

## What to actually look for

- **All 3 agree?** → The task was easy. Zero-shot is good enough — no reason to pay more for few-shot or CoT.
- **CoT disagrees with the other two?** → The text was probably genuinely tricky (sarcasm, mixed signals), and the extra reasoning caught something the fast methods missed.
- **Few-shot/CoT cost way more tokens for the same answer?** → That's wasted cost if you're doing this thousands of times a day.

This mirrors a real finding from prompt engineering research: **zero-shot often matches expert-level chain-of-thought accuracy at a fraction of the time and cost** — but only on tasks that aren't actually that hard. This tool lets you test, live, whether *your* task falls into that bucket.

---

## How to use it

1. Get a free API key at [console.groq.com/keys](https://console.groq.com/keys)
2. Paste the key into the box (it only lives in your browser — never sent anywhere except directly to Groq)
3. Paste any text you want to test, or click one of the preset examples
4. Click **Run Comparison**
5. Compare the 3 results

---

## Tech stack

Just one file — `index.html`. No installs, no build step, no backend.
- Plain HTML, CSS, and JavaScript
- Calls the [Groq API](https://groq.com/) directly from the browser
- Model used: `llama-3.1-8b-instant`

---

## Try these examples

**Clear-cut — strategies should agree:**
```
The company reported record profits this quarter, employee satisfaction hit an all-time high, and the CEO announced a company-wide bonus for every staff member.
```

**Mixed signals — a fairer test for disagreement:**
```
The new manager made a lot of changes in her first month. Meetings are shorter now, but half the team feels like they weren't consulted before the changes were rolled out.
```

```
Ticket prices went up by 15% this year, but the venue also added more seating and a new fan zone with free food trucks.
```

**Negative start, positive ending — tests if the model reads the full arc:**
```
It was a disaster for the first two hours — the server kept crashing and we thought the launch was dead. But we fixed the root cause live and shipped ahead of schedule with the best feedback we've ever gotten.
```

**Sarcasm — tests if reasoning catches tone vs. literal words:**
```
Oh great, another 6am mandatory meeting that could've been an email. Truly the highlight of my week.
```

> Note: in testing, Llama 3.1 8B stayed pretty consistent across all three strategies even on these trickier cases — verdicts rarely flipped. The real differentiator between strategies showed up in **latency and token cost**, not accuracy. That's actually the finding worth highlighting: zero-shot can match the "smarter" strategies on correctness while being faster and cheaper.

---

## License

MIT — feel free to use, adapt, and learn from it.
