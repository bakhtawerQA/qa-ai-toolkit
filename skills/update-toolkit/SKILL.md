---
name: update-toolkit
description: Update the QA AI Toolkit to the latest version - pull the repo, switch on any new skills, and say what changed. Use whenever someone says "update my QA toolkit", "update QA skills", "get the latest QA toolkit", or runs /update-toolkit.
---

# update-toolkit - get the latest QA skills

Do this without asking anything, unless a step below says to ask.

1. **Pull the latest version.**
   - `~/.qa-toolkit/repo` is missing → say *"The QA toolkit isn't installed yet. Say: Set up the QA
     toolkit from https://github.com/bakhtawerQA/qa-ai-toolkit"* and stop.
   - Otherwise note the current commit (`git -C ~/.qa-toolkit/repo rev-parse HEAD`), then run
     `git -C ~/.qa-toolkit/repo pull`. If the pull fails (local edits, no network), show the error
     in one line and stop.
2. **Switch on new skills.** For every folder in `~/.qa-toolkit/repo/skills/` that is not yet in
   `~/.claude/skills/`, run `ln -sfn ~/.qa-toolkit/repo/skills/<name> ~/.claude/skills/<name>`.
   Existing links already point at the repo, so they are up to date. If a non-link folder with the
   same name exists, ask before replacing it.
3. **Say what changed.**
   - Nothing new → *"Already up to date."*
   - Otherwise list the changes in plain words from
     `git -C ~/.qa-toolkit/repo log --oneline <old commit>..HEAD`, and name any newly added skills.
     New skills work from the next message.

Never touch `~/.qa-toolkit/projects.yaml`. It holds their own setup.
