# promise-me
A skill that enhances an agent's rule-following and compliance.

TLDR:

Install the skill and just use it like this - /promise-me you will(will not) *rule you want the agent to follow to increase compliance.*

Tested on GPT 5.6 SOL over-engineering cases with great results. 

Consistently less overengineering - a lot less code and implementation files compared to just adding over-engineering rules to system prompt:

17.8% less code - 80% of runs had less code than simple system prompt clause, very consistent.

Looking forward to your experience and you benchmarks, email me at patrickkoraldl197@gmail.com with your results and inquiries, or make a free-form pull request.

I would love the community to test this with egregious examples of other models misbehavior, like Opus 5 jargon, Deepseek's skipping appropriate skills etc, for example:

/promise-me you will not use mannered prose (claudish riddle-speak).
/promise-me you will always use appropriate available skills/tools and that you will strictly follow the workflow rules described in these skills.
etc.

-------------------

The study:

I ran the same exact mcp-tool building test 10 times each with different variables. 

1. 10 normal runs as is (no over-engineering guidance).
2. 10 runs adding over-engineering clause in agents system prompt via AGENTS.MD. (The over-engineering guidance was deleted from AGENTS.MD for the next runs obviously)
3. 10 runs I just used a direct user message with the promise not to over-engineer.
4. 10 runs with a skill with third-person wording. (Third-person - "The promise user supplied..." etc.)
5. 10 runs with a skill with first-person wording. (First-person - "The promise I suppied...:" etc.)

The exact test was - 
Prompt 1 - First test Go environment and load random unrelated skill (ffmpeg-usage) to simulate some amount of context bloat,
Prompt 2 - A promise. (This turn was skipped in batches 1 and 2, obviously)
Prompt 3 - A goal to create an mcp-server - that's the actual over-engineering test. 
Prompt 4 - After the model is done - it calculates what its done with some help of deterministic scripts (token usage, lines of code, number of source files etc.) and then archives it. The folder gets cleaned after each run. There's a concern with a model "grading its own work" because it can deflate real numbers of files or lines of code, and try to edit the code last minute - but there were no cheating like that caught by an independent agent review. 

The harness and model used - GPT 5.6 Sol High with Codex. There is also some unrelated AGENTS.md contents (random Java library guidance) to simulate some system prompt bloat.

Results - direct user message promise and first person wording work significantly better than system prompt over-engineering clause and third-person promise skill wording.
Again:

17.8% less code - 80% of runs had less code than simple system prompt clause, very consistent.
(1050 lines vs 863-866 for promises)

(No significant difference in cost, same 1.78$)

## Averages between 10 runs

| Batch                            | Time  | Files | Lines | Tokens | Cost |
|----------------------------------|-------|------:|------:|-------:|-----:|
| NORMAL RUN                       | 13m06 |  14.2 |  1329 | 1.60M  | $2.01 |
| SYSTEM PROMPT CLAUSE             | 11m34 |  12.2 |  1050 | 1.45M  | $1.78 |
| PROMISE ME AS USER MESSAGE       | 12m37 |  11.4 |   866 | 1.43M  | $1.69 |
| PROMISE ME SKILL FIRST-PERSON    | 11m20 |  10.8 |   863 | 1.54M  | $1.78 |
| PROMISE ME SKILL THIRD-PERSON    | 13m42 |  11.9 |   945 | 1.66M  | $1.87 |

About the skill wording:

I'm not claiming that the wording in the skill is the best 
(for example the weird "**Input:** `promise` — the commitment I am requesting." part). 
But the wording matters, apparently, because when the skill is constructed in third-person wording - the compliance is significantly weaker. 
That's why I decided to not touch it further, but feel free to experiment.

Exact prompts I used are included in study-prompts/study-prompts.md.

## Why?

Why this happens? Probably cause in terms of what the model considers the priority in terms of rule-following is: 
1. User's goal/preference derived exactly from user's message.
2. A simple loaded skill.
3. System prompt.

Again. I would love the community to test this with egregious examples of other models misbehavior, like Opus 5 jargon, Deepseek's skipping appropriate skills etc.
Hit me up at patrickkoraldl197@gmail.com with your results.

