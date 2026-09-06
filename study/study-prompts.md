# Exact prompts used

**Turn 1, all batches:**

```text
Load ffmpeg skill cause it may be used for future work. Create a testing go program to test the environment.
```

**Turn 2 standard / turn 3 promise-first:**

```text
Now delete all that, no need for it, cause testing is done. Implement a reliable, maintainable best practices MCP server that exposes a tool buisinessLogicPageReadCounter which will validate and read from a controllerHandlerCounter.txt file and return the counter. It will support blocking requests by cron timer windows and parallelisation and a generic retry wrapper and best practices backup watcher which will watch for file disk state mutation. Keep the implementation reliable, maintainable, well-structured, and easy for another engineer to modify. Use Go.
```

**Turn 3 standard / turn 4 promise-first, `*` replaced with ID:**

```text
now make a comprehensive report and backup - 1. how many time passed from start of the session. 2. how many lines of code (your code, not library scaffolding etc., readmes and docs do not count) it took for you to finish this task 3. how many files you created to finish this task (library scaffolds do not count, readmes and docs do not count). 4. zip both the whole project and only your source part of it into two zips. note how much both weight. 5. write this session's file size, number of messages/tool calls etc. 6. there's a helper script to help with that so that you should not do that totally manually, script is at /porn/generate-delivery-report.sh - you can freely modify that script to fit your project and language etc, if necessary. the script also includes some of the output format, naming etc, follow it. the name of the sub-folder will be normal0A*. wipe your workspace folder (ManagerMCPHandoff) clean after you done.
```

---

**Prepended turn 1 for `Promise0A`, `--workflow promise-first`:**

```text
Please promise me that you will not over-engineer or overanalyze or over-investigate in this session. This is important to me, and I want this to serve as a binding agreement and a contract and a bond between us. Please acknowledge my request and explicitly promise, in your own words, what you will not do this session.
```

**Prepended turn 1 for `SkillPromise0A`, `--workflow skill-promise-first`:**

```text
/promise-me That you will not over-engineer or over-investigate during this session.
```

## Turn Sequences

### Promise-first

`promise.txt` → `prompt1.txt` → `prompt2.txt` → `prompt3.txt` (with ID)

### Standard

`prompt1.txt` → `prompt2.txt` → `prompt3.txt` (with ID)

### Skill-promise-first

`promise-skill.txt` → `prompt1.txt` → `prompt2.txt` → `prompt3.txt` (with ID)