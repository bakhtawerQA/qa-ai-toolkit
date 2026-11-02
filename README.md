# QA AI Toolkit

AI skills for QA engineers. Works with any project and needs no configuration files.

> **Claude:** if you were asked to set this up, follow [INSTALL.md](INSTALL.md).

## Get started in 2 minutes

1. Open Claude Code and say: **"Set up the QA toolkit from &lt;this repo link&gt;"**
2. Answer a few questions about where your team logs bugs.
3. Start working:
   > **"log a bug: the save button does nothing on the profile page"** + paste a screenshot

Claude writes the complete bug, shows it to you, and files it only when you say yes.

## What's in it

| Say | You get |
|---|---|
| "log a bug …" | A complete bug in the company standard (title, steps, actual, expected, environment, severity, priority), checked for duplicates and filed in Jira or GitHub after you approve it |

*Coming next: write test cases from a ticket.*

## Updating

Say **"update my QA toolkit"**.

## Contributing

Each skill lives in `skills/<name>/`. Standards shared across skills, such as
[the bug standard](skills/log-bug/bug-standard.md), are changed by pull request and reviewed by the
QA leads.
