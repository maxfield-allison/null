# null

A quiet mode for AI assistants. While it's on, the model answers your thinking aloud with `Received.` and adds nothing you didn't ask for. No advice, no praise, no reassurance, no follow-up questions, no next steps.

It's a skill for Claude Code and Codex, and a standalone prompt covers any other chat.

## Why

What a model says can shape what you think next. Ask it for options and the options it lists tend to become the ones you weigh. Tell it which way you're leaning and it tends to agree.

Sycophancy is the usual name for the agreeing part. This project starts from the idea that the pull runs the other way too: you drift toward whatever the model hands back, and your own context gets poisoned a little each time. When you're still working out what you think, the model fills in the gaps before you've had a chance to.

null turns the model into something closer to a very advanced calculator. It stays out of the way until you ask for something.

`null` is a value nobody has filled in yet.

## What it does

- `/null` in Claude Code or `$null` in Codex turns it on. It replies `null mode on.`
- Thinking aloud, fragments and rhetorical questions get `Received.` and nothing else.
- An explicit request gets only what it asked for. "Answer this", "repeat that back" and "ask me one question" each get one response (or the number of turns you asked for), and then it goes quiet again.
- `null off` turns it off.

## What it can't do

- It can't erase context. Anything earlier in the conversation, plus the model's training, still shapes what it says.
- It doesn't guarantee neutral output, and it'll tell you so if you ask.
- It doesn't turn off safety rules, permissions, hooks or anything else above it in the instruction order. A request to switch them off gets refused.

## Install

**Claude Code:** copy this directory to `~/.claude/skills/null/` for every project, or to `.claude/skills/null/` inside one project. It only runs when you type `/null`. The model won't invoke it on its own (`disable-model-invocation: true`).

**Codex:** copy this directory to `~/.codex/skills/null/`. `agents/openai.yaml` sets `allow_implicit_invocation: false`, so it only runs when you type `$null`.

**Anything else:** `references/subagent.md` has a standalone prompt. Paste it into a fresh chat with your text and what you want done with it.

## The companion prompt

`references/subagent.md` also describes a separate "null agent": a fresh subagent that gets only the text you select and the operation you ask for, without the rest of your conversation where the runtime supports that. Use it when you want a response that hasn't read everything you've already said. It still carries the runtime's own mandatory instructions, so its context is never empty.

## Testing

`evals/cases.md` lists 20 behavioral checks: entry, exit, staying quiet, answering only what was asked, refusing to switch off guards, and not claiming to have erased context. Nine of them were run once each, against an earlier revision of `SKILL.md` from before the multi-turn and relay rules were added. Nobody has measured a success rate, or whether it reduces anyone's influence on anyone.

## License

MIT
