# 🧠 Socratic Mentor — a Claude Code plugin

**Make Claude teach you instead of doing your thinking for you.**

Socratic Mentor is a plugin for [Claude Code](https://claude.com/claude-code) that flips Claude from an answer machine into a Socratic tutor. While it is active, Claude will **never hand you the finished answer**. Instead it:

- 🧭 Guides you with hints, first steps, and guiding questions
- 🗣️ Explains concepts in simple terms — just enough for you to make the next move yourself
- 🔎 Uses Claude's built-in web search to find **real, current learning resources**
- 🎥 Recommends **YouTube videos and full courses** (freeCodeCamp, MIT OCW, university lectures) with exact links — never invented URLs
- ❓ Ends every reply with one question that makes you think or try something
- 🪜 Gradually reveals more **only if you're genuinely stuck** after multiple real attempts

## Why

We've all gotten used to pasting a problem into an AI and copying out the solution. It's fast — and it quietly erodes the ability to solve problems on our own. Socratic Mentor exists to reverse that: it makes you work for the answer, the way a good human tutor would, while still pointing you to the best resources on the internet to learn from.

## Installation

Inside any Claude Code session, run:

```
/plugin marketplace add HitarthTrivedi/socratic-mentor
/plugin install socratic-mentor@hitarth-plugins
```

That's it. The plugin is now available in every project on your machine.

> Replace `HitarthTrivedi/socratic-mentor` with the actual GitHub `owner/repo` if you forked this.

## Usage

**Nothing to activate — it's always on.** Once installed, the plugin replaces Claude Code's default behavior: *every* response becomes Socratic, whether you ask "teach me X" or just "fix this bug". You cannot take the shortcut, even when you want to — that's the point.

Every response follows this shape:

| Section | What you get |
|---|---|
| **Nudge** | A hint, first step, or reframing — in simple terms |
| **Learn from** | 2–3 real links from a live web search, always including a YouTube video/course when one exists |
| **Your move** | One question or small task to do before coming back |

## Deactivating

Since it's always-on, you turn it off at the plugin level (then start a new session):

```
/plugin disable socratic-mentor@hitarth-plugins   # keep it installed, turn it off
/plugin enable socratic-mentor@hitarth-plugins    # turn it back on
/plugin uninstall socratic-mentor@hitarth-plugins # remove it entirely
```

## Example

> **You:** How do I reverse a linked list in Python?
>
> **Claude (Socratic Mentor):**
> **Nudge:** Think about what "reversing" means at the pointer level: every node's `next` must end up pointing at the node that came *before* it. You only need three variables to walk the list and flip those pointers one at a time. What would you call them?
>
> **Learn from:**
> - *Reverse a Linked List — visual walkthrough* (YouTube) — animates exactly the pointer flip you need
> - *NeetCode: Linked List course* (YouTube) — covers this and the 5 patterns built on it
> - *GeeksforGeeks: Reverse a linked list* — diagrams + practice problems
>
> **Your move:** Draw three boxes on paper for nodes A→B→C and manually flip the arrows step by step. What state do your three variables need to be in *before* you flip B's pointer?

## How it works

The plugin ships a **custom agent** (`agents/socratic-mentor.md`) containing the tutoring rules — never answer directly, search before recommending, always include video resources, one question per reply, gradual escape hatch for genuinely stuck learners — plus a `settings.json` with `{"agent": "socratic-mentor"}`, which tells Claude Code to run that agent as the **main thread** whenever the plugin is enabled. That's what makes it always-on rather than opt-in. A standalone copy of the rules also ships as a skill (`skills/mentor/SKILL.md`) for anyone who prefers session-by-session activation. It leans on Claude Code's built-in `WebSearch`/`WebFetch` tools for live resource discovery — **no API keys, no external services, nothing to configure**.

## Repository structure

```
socratic-mentor/
├── .claude-plugin/
│   ├── plugin.json          # plugin manifest
│   └── marketplace.json     # lets people add this repo as a marketplace
├── agents/
│   └── socratic-mentor.md   # the always-on tutor agent (main thread)
├── settings.json            # activates the agent by default
├── skills/
│   └── mentor/
│       └── SKILL.md         # opt-in variant of the same rules
└── README.md
```

## License

MIT — copy it, remix it, share it.
