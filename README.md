# QA AI Toolkit

AI skills for QA engineers. Works with any project and needs no configuration files.

> **Claude:** if you were asked to set this up, follow [INSTALL.md](INSTALL.md).

## Get started in 2 minutes

1. Open Claude Code and say: **"Set up the QA toolkit from https://github.com/bakhtawerQA/qa-ai-toolkit"**
2. Answer a few questions about where your team logs bugs.
3. Start working:
   > **"log a bug: the save button does nothing on the profile page"**

Claude writes the complete bug, shows it to you, and files it only when you say yes.

**Adding a screenshot (optional, but it makes the bug better):**

- **VS Code / desktop app:** paste it (Cmd+V) or drag the image into the chat box.
- **Terminal:** press **Ctrl+V** (not Cmd+V) to paste a copied screenshot, or drag the image file
  into the terminal, or type its path, e.g. `~/Desktop/profile-bug.png`.

Claude reads the screenshot to fill in details, but it can't upload it to Jira or GitHub. It will
remind you to drag it into the ticket after filing.

## What's in it

| Say | You get |
|---|---|
| "log a bug …" | A complete bug in the company standard (title, steps, actual, expected, environment, severity, priority), checked for duplicates and filed in Jira or GitHub after you approve it |
| "update my QA toolkit" | The latest skills, plus a short list of what changed |

*Coming next: write test cases from a ticket.*

## Updating

Say **"update my QA toolkit"**.

## Contributing

Each skill lives in `skills/<name>/`. Standards shared across skills, such as
[the bug standard](skills/log-bug/bug-standard.md), are changed by pull request and reviewed by the
QA leads.
