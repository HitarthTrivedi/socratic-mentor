# 📦 Socratic Mentor — Installation & Setup Guide

Every command and procedure in one place: installing, enabling/disabling, using it on the Claude website, and deploying your own copy to GitHub.

---

## 1. Claude Code (recommended — full always-on experience)

### Install

Run inside any Claude Code session:

```
/plugin marketplace add HitarthTrivedi/socratic-mentor
/plugin install socratic-mentor@hitarth-plugins
```

Restart your session. From now on, **every** Claude Code session on your machine runs in Socratic mentor mode — no activation needed.

The same works from your terminal (outside a session):

```bash
claude plugin marketplace add HitarthTrivedi/socratic-mentor
claude plugin install socratic-mentor@hitarth-plugins
```

### Disable / Enable (keep it installed, toggle it)

```
/plugin disable socratic-mentor@hitarth-plugins    # turn off (restart session to apply)
/plugin enable socratic-mentor@hitarth-plugins     # turn back on (restart session to apply)
```

Use `disable` when you genuinely need normal Claude for a while — the plugin stays installed.

### Update (get the latest version)

```
/plugin marketplace update hitarth-plugins
/plugin update socratic-mentor@hitarth-plugins
```

### Uninstall (remove completely)

```
/plugin uninstall socratic-mentor@hitarth-plugins
/plugin marketplace remove hitarth-plugins          # optional: also remove the marketplace
```

### Try before installing (developers)

```bash
git clone https://github.com/HitarthTrivedi/socratic-mentor.git
claude --plugin-dir ./socratic-mentor
```

This loads the plugin for one session only, without installing anything.

---

## 2. Claude website / desktop app (claude.ai)

The Claude app doesn't run Claude Code plugins, but the same rules work there as a **skill** or as **preferences**.

### Paid plans (Pro / Max / Team / Enterprise) — upload as a custom skill

1. Download [`socratic-mentor-skill.zip`](./socratic-mentor-skill.zip) from this repository
2. Open **claude.ai → Settings → Capabilities**
3. In the **Skills** section, click **Upload skill** and select the zip
4. Done — Claude activates the tutor whenever your conversation is about learning something

> Note: in the app the skill activates when relevant; it can't be forced always-on the way the Claude Code plugin can. For always-on behavior in the app, use the free-plan method below as well.

### Free plan — copy-paste (zero install)

1. Open [`skills/mentor/SKILL.md`](./skills/mentor/SKILL.md) in this repository
2. Copy everything **below** the `---` frontmatter block
3. Paste it into **claude.ai → Settings → Profile → personal preferences**
   (or simply paste it as the first message of any chat)
4. Every conversation now follows the mentor rules

To stop: remove the text from your preferences.

---

## 3. Deploy your own copy on GitHub

Want to publish your own version (a fork, a translation, stricter/looser rules)? This repo is both a **plugin** and a **marketplace**, so one repo is all you need.

### Step by step

1. **Fork or copy this repository** to your GitHub account (public repo).

2. **Make it yours** — edit these files:
   - `.claude-plugin/plugin.json` → change `author.name`; bump `version` when you change behavior
   - `.claude-plugin/marketplace.json` → change `name` (this becomes your marketplace name, e.g. `yourname-plugins`), `owner`, and the plugin `description`
   - `agents/socratic-mentor.md` and `skills/mentor/SKILL.md` → the actual tutoring rules
   - `README.md` / `install.md` → replace `HitarthTrivedi/socratic-mentor` with your `username/repo`

3. **Validate before publishing** (catches structure mistakes):

   ```bash
   cd your-plugin-folder
   claude plugin validate .
   ```

4. **Push to GitHub:**

   ```bash
   git init -b main
   git add -A
   git commit -m "My Socratic Mentor plugin"
   git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO.git
   git push -u origin main
   ```

5. **Test the full pipeline yourself** (exactly what your users will run):

   ```
   /plugin marketplace add YOUR_USERNAME/YOUR_REPO
   /plugin install socratic-mentor@YOUR_MARKETPLACE_NAME
   ```

6. **Ship updates:** edit files → bump `version` in `plugin.json` → commit → push. Users receive the update when they run `/plugin marketplace update` + `/plugin update`.

### Reach everyone (optional)

Submit your plugin to Anthropic's community marketplace so users can discover it inside Claude Code without knowing your repo URL:

- Submit at: **https://platform.claude.com/plugins/submit**
- Requirement: `claude plugin validate` must pass (the review pipeline runs the same check)
- Once approved, it appears in the [community catalog](https://github.com/anthropics/claude-plugins-community/blob/main/.claude-plugin/marketplace.json) and installs via `@claude-community`

---

## Quick reference card

| I want to… | Command |
|---|---|
| Install | `/plugin marketplace add HitarthTrivedi/socratic-mentor` then `/plugin install socratic-mentor@hitarth-plugins` |
| Turn off temporarily | `/plugin disable socratic-mentor@hitarth-plugins` |
| Turn back on | `/plugin enable socratic-mentor@hitarth-plugins` |
| Update to latest | `/plugin marketplace update hitarth-plugins` then `/plugin update socratic-mentor@hitarth-plugins` |
| Remove completely | `/plugin uninstall socratic-mentor@hitarth-plugins` |
| Use on claude.ai (paid) | Upload `socratic-mentor-skill.zip` at Settings → Capabilities → Skills |
| Use on claude.ai (free) | Copy `skills/mentor/SKILL.md` text into Settings → Profile → personal preferences |

*(Remember: after enable/disable/install, restart your Claude Code session for the change to apply.)*
