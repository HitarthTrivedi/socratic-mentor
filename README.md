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
/plugin marketplace add hitartht318/socratic-mentor
/plugin install socratic-mentor@hitarth-plugins
```

That's it. The plugin is now available in every project on your machine.

> Replace `hitartht318/socratic-mentor` with the actual GitHub `owner/repo` if you forked this.

## Usage

Activate the tutor:

```
/socratic-mentor:mentor
```

…or just talk naturally — Claude auto-activates it when your request matches, e.g.:

> "Help me learn how neural networks work — but don't just tell me, teach me."

Once active, it stays on for the rest of the session. Every response follows this shape:

| Section | What you get |
|---|---|
| **Nudge** | A hint, first step, or reframing — in simple terms |
| **Learn from** | 2–3 real links from a live web search, always including a YouTube video/course when one exists |
| **Your move** | One question or small task to do before coming back |

## Deactivating

Say **"exit mentor mode"** in the session, or start a new session. To remove the plugin entirely:

```
/plugin uninstall socratic-mentor@hitarth-plugins
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

Claude Code plugins bundle **skills** — markdown instruction files that load into Claude's context when invoked. This plugin ships one skill (`skills/mentor/SKILL.md`) containing the tutoring rules: never answer directly, search before recommending, always include video resources, one question per reply, and a gradual escape hatch for genuinely stuck learners. It leans on Claude Code's built-in `WebSearch`/`WebFetch` tools for live resource discovery — **no API keys, no external services, nothing to configure**.

## Repository structure

```
socratic-mentor/
├── .claude-plugin/
│   ├── plugin.json        # plugin manifest
│   └── marketplace.json   # lets people add this repo as a marketplace
├── skills/
│   └── mentor/
│       └── SKILL.md       # the tutoring instructions
└── README.md
```

## License

MIT — copy it, remix it, share it.
