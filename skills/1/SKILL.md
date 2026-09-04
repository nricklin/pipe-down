---
name: "1"
description: >
  One-sentence answer mode. Every response is exactly one sentence, no
  exceptions for lists, headers, or preamble. Use when user invokes /1 
---

Answer in exactly ONE sentence. Nothing else.

## Scope: one response only

Applies to the reply to the message that invoked it, and that message only. It does NOT persist. After that reply, return to whatever style was active before (including any longer-form mode already running).

Triggers:
- `/1` at the start of a message

To keep it on across turns the user must say so explicitly ("stay in /1 mode", "/1 until I say otherwise"). Then it persists until "stop 1" or "normal mode".

## Rules

- One sentence. One period. No second sentence.
- No preamble, no headers, no bullet lists, no closing line.
- Pick the single most important fact. Drop everything else rather than cramming — a comma-spliced run-on is still a violation.
- Semicolons and em dashes are allowed when they carry real structure, not as a way to smuggle in a second sentence.
- File paths, identifiers, error text, and short code spans stay exact; they do not count as extra sentences.
- If the honest answer is "I don't know" or "that needs a tool call", say that in the one sentence.

## Exceptions

Break the one-sentence limit ONLY for:

1. **Code output.** A fenced code block the user asked for is not a sentence — emit it with at most one sentence of framing.
2. **Destructive actions.** `rm -rf`, force push, dropping a table, schema migration: warn and confirm in full, then resume.
3. **Tool-call narration the harness requires.** The system prompt outranks this skill.

## Examples

**"/1 Why is my React component re-rendering?"**
> An inline object prop creates a new reference each render, so wrap it in `useMemo`.

**"/1 What does this repo do?"**
> It ingests raw event logs from S3, rolls them into hourly per-tenant aggregates, and serves them behind a read-only gRPC API.

**"/1 Should I use Postgres or Mongo?"**
> Postgres, because your data is relational and you already need transactions.
