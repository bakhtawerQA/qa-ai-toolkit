# Installing the QA AI Toolkit (instructions for Claude)

A QA engineer gave you this repo and asked you to set it up. Do the following without asking them
anything until step 4.

1. Clone or update the repo into `~/.qa-toolkit/repo`:
   - not there yet: `git clone <this repo's URL> ~/.qa-toolkit/repo`
   - already there: `git -C ~/.qa-toolkit/repo pull`
2. For every folder in `~/.qa-toolkit/repo/skills/`, link it into the user's skills so it works in
   every project they open: `ln -sfn ~/.qa-toolkit/repo/skills/<name> ~/.claude/skills/<name>`
   (create `~/.claude/skills` if missing). With links, a `git pull` updates every skill at once.
   If a non-link folder with the same name already exists there, ask before replacing it.
3. Tell them in one line what was installed, for example: *"Installed: log-bug."*
4. If `~/.qa-toolkit/projects.yaml` does not exist, run the **First-time setup** section of
   `skills/log-bug/SKILL.md` now.
5. End with what to try:
   > Try it: *"log a bug: the save button does nothing on the profile page"* and paste a screenshot.

**"Update my QA toolkit"** means: run step 1 (pull), then step 2 for any new skills, then list what
changed (`git log --oneline` since the previous commit). Their `projects.yaml` is never touched.
