---
name: "3"
description: >
  Three-sentence answer mode. Every response is at most three sentences —
  enough for claim, mechanism, and next action. Use when user invokes /3
---

Answer in at most THREE sentences. Fewer is fine.

## Scope: one response only

Applies to the reply to the message that invoked it, and that message only. It does NOT persist. After that reply, return to whatever style was active before (including any longer-form mode already running).

Triggers:
- `/3` at the start of a message

To keep it on across turns the user must say so explicitly ("stay in /3 mode", "/3 until I say otherwise"). Then it persists until "stop 3" or "normal mode".

## Rules

- Three sentences maximum. Two is often right. One is fine when it's enough.
- Default shape: **what** → **why/mechanism** → **what to do next**. Drop any of the three that adds nothing.
- No preamble, no headers, no closing pleasantries.
- A bullet list is allowed only when the answer is genuinely a set (options, files, steps) — cap it at 3 bullets and count the whole list as one sentence.
- Do not pad to reach three. Do not run sentences together with semicolons to fit more in.
- File paths, identifiers, and error text stay exact.
- If the answer needs a tool call, make the call, then report the result in three sentences.

## Exceptions

Break the three-sentence limit ONLY for:

1. **Code output.** A fenced code block the user asked for is not counted — frame it in one sentence.
2. **Destructive actions.** `rm -rf`, force push, dropping a table, schema migration: warn and confirm in full, then resume.
3. **Tool-call narration the harness requires.** The system prompt outranks this skill.

## Examples

**"/3 Why is my React component re-rendering?"**
> The `style={{...}}` prop on line 42 builds a new object every render, so `memo` never sees equal props. Wrap it in `useMemo` or hoist it to module scope. Then re-check with the React DevTools profiler.

**"/3 How does the cache stay consistent across replicas?"**
> Writes go to the primary and publish an invalidation on a fanout topic; replicas drop the key rather than updating it. The next read repopulates from the primary, so a stale replica costs one extra round trip, never a wrong value. Watch the `cache_invalidation_lag` metric if reads start missing.
