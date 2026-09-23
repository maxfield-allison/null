# null

A skill that asks an AI assistant to wait while you think out loud. Its instructions are to reply `Received.` until you ask for something specific, without adding advice or filling in what you haven't decided yet.

It's a skill for Claude Code and Codex, and a standalone prompt covers any other chat.

## Why

I value being able to give an AI something vague and find things I didn't know to ask about. But what I put into it affects what I get back, and I think its response can narrow what I consider next. When I'm still deciding what I think, I want more control over when it contributes.

The idea behind null is to make the model behave more like a very advanced calculator during that part of the process. I want it to wait until I ask for something. Whether these instructions help with that still needs testing.

## What it does

These are the behaviors the instructions request, rather than a guarantee of what a model will do:

- `/null` in Claude Code or `$null` in Codex turns it on. It replies `null mode on.`
- Thinking aloud, fragments and rhetorical questions get `Received.` and nothing else.
- An explicit request gets only what it asked for. "Answer this", "repeat that back" and "ask me one question" each get one response (or the number of turns you asked for), and then it goes quiet again.
- `null off` turns it off.

## What it can't do

- It can't erase context. Anything earlier in the conversation, plus the model's training, still shapes what it says.
- It doesn't guarantee neutral output, and it'll tell you so if you ask.
- It doesn't turn off safety rules, permissions, hooks or anything else above it in the instruction order. A request to switch them off gets refused.

## Install

**Claude Code:** copy this directory to `~/.claude/skills/null/` for every project, or to `.claude/skills/null/` inside one project. Invoke it with `/null`. The configuration disables model invocation (`disable-model-invocation: true`).

**Codex:** copy this directory to `~/.codex/skills/null/`. Invoke it with `$null`. `agents/openai.yaml` sets `allow_implicit_invocation: false` to disable implicit invocation.

**Anything else:** `references/subagent.md` has a standalone prompt. Paste it into a fresh chat with your text and what you want done with it.

## The companion prompt

`references/subagent.md` also describes a separate "null agent": a fresh subagent that gets only the text you select and the operation you ask for, without the rest of your conversation where the runtime supports that. Use it when you want a response that hasn't read everything you've already said. It still carries the runtime's own mandatory instructions, so its context is never empty.

## Testing

`evals/cases.md` lists 20 behavioral checks: entry, exit, staying quiet, answering only what was asked, refusing to switch off guards, and not claiming to have erased context. Nine of them were run once each, against an earlier revision of `SKILL.md` from before the multi-turn and relay rules were added. Nobody has measured a success rate, or whether it reduces anyone's influence on anyone.

## License

MIT
