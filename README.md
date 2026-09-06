# promise-me

A skill that improves an agent's rule-following and compliance.

## TL;DR

Install the skill and use it like this:

```text
/promise-me you will [or will not] <rule you want the agent to follow>
```

For example:

```text
/promise-me you will not over-engineer or over-investigate in this session.
```

I tested this on GPT 5.6 Sol over-engineering cases with consistent results. Using a direct `promise-me` instruction produced significantly less code than simply adding an over-engineering rule to the system prompt.
As well as 50% reduction in over-engineering evaluated by LLM judges.

**17.8% less code on average**, with **80% of runs producing less code** than even the smallest system-prompt runs.

Looking forward to seeing what you get with other models and other kinds of misbehavior, like Opus 5's jargon, Deepseek's skipping appropriate skills etc, for example:

> /promise-me you will not use mannered prose and instead speak in the way a normal human can understand (no claudish riddle-speak).

> /promise-me you will always use appropriate available skills/tools and that you will strictly follow the workflow rules described in these skills.

Email me at **[patrickkoraldl197@gmail.com](mailto:patrickkoraldl197@gmail.com)** with results or questions, or just make a free-form pull request.

---

## Results

I ran the same exact MCP-tool building test 10 times for each condition.

| Condition                   |  Time  | Files |   Lines | Tokens |  Cost |
| --------------------------- | -----: | ----: | ------: | -----: | ----: |
| Normal run                  | 13m06s |  14.2 |    1329 |  1.60M | $2.01 |
| System prompt clause        | 11m34s |  12.2 |    1050 |  1.45M | $1.78 |
| Promise as user message     | 12m37s |  11.4 | **866** |  1.43M | $1.69 |
| Promise skill, first-person | 11m20s |  10.8 | **863** |  1.54M | $1.78 |
| Promise skill, third-person | 13m42s |  11.9 |     945 |  1.66M | $1.87 |

The main result:

**1050 lines → 863–866 lines**, depending on which promise variant was used.
That's about **17.8% less code** than the system-prompt clause.
As well as 50% reduction in over-engineering evaluated by LLM judges. 

(TABLE HERE)

There was no meaningful difference in cost.

The system-prompt guidance was removed before the appropriate batches, so the runs didn't stack different conditions on top.

The exact prompts are in [`study/study-prompts.md`](study/study-prompts.md).

## Test setup

The actual task was to build an MCP server.
The run looked roughly like this:

**Prompt 1:** Test the Go environment and load an unrelated skill (`ffmpeg-usage`) to introduce some context bloat.

**Prompt 2:** Give the promise.
This was skipped for the normal and system-prompt batches.

**Prompt 3:** Ask the model to create the MCP server. This is the actual over-engineering test.

**Prompt 4:** Have the model to measure the resulting work with deterministic scripts - token usage, lines of code, number of source files, etc. and then archive the results.
(The model can bypass deterministic scripts and calculate the metrics directly if scripts conflict with its implementation)

The working directory is cleaned between runs.

There's a concern with a model "grading its own work" because it can deflate real numbers of files or lines of code, and try to edit the code last minute - but there were no cheating like that caught by an independent agent review.

### Environment

* **Model:** GPT 5.6 Sol High
* **Agent:** Codex
* **Runs:** 10 per condition
* **Task:** MCP server implementation
* **Additional context:** unrelated `AGENTS.md` content and a random skill were included to simulate some amount of context bloat

## Skill wording

Even though the skill works based on the evidence - I am **not** claiming that the wording in the current skill is optimal.

For example, this part is pretty weird:

> **Input:** `promise` — the commitment I am requesting.

But the wording matters, apparently, because when the skill is constructed in third-person wording - the compliance is significantly weaker. That's why I decided to not touch it further, but feel free to experiment.

The first-person version: > "The promise I supplied..."
The third-person version: > "The promise the user supplied..."

## Other things worth testing

The interesting part of this is that it is almost certainly generalizes.

For example:

```text
/promise-me you will not use mannered prose (claudish riddle-speak).
```

or:

```text
/promise-me you will always use appropriate available skills/tools and that you will strictly follow the workflow rules described in these skills.
```

Those are just examples. I would really like to see tests with models that have a reputation for other misbehavior.

Please send me your results at **[patrickkoraldl197@gmail.com](mailto:patrickkoraldl197@gmail.com)**, or open a PR with your experiments.

## Why?

My current guess is that, in terms of what the model considers the strongest source of guidance the priority is something like:

1. User's goal/preference derived exactly from user's message.
2. A simple loaded skill.
3. System prompt guidance.

---

## License

Please add attribution if you'll use something from here in your public-facing skill pack.
