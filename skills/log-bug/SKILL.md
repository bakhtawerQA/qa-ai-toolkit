---
name: log-bug
description: Turn a QA engineer's quick bug note - a one-liner, rough steps, a screenshot or a video link - into a complete, standard bug ticket and file it in their project's tracker (Jira, GitHub Issues) after they approve the draft. Use whenever someone says "log a bug", "file a bug", "raise a defect", "report this issue", pastes a screenshot saying something is broken, or runs /log-bug.
---

# log-bug - from a quick note to a standard bug ticket

The QA engineer gives you as little as one line and a screenshot. You give back a complete bug in the
company standard, show it to them, and file it only once they say yes.

Keep the experience effortless: never make them fill a form, never ask what you can see in the
evidence or work out yourself, and never ask more than one question at a time.

---

## Step 0 - Know the project (first run only)

Read `~/.qa-toolkit/projects.yaml`.

- **It has one project** → use it.
- **It has several** → pick the one the note obviously belongs to (a ticket key like `ABC-12`, a
  product name). If it is not obvious, ask *"Which project is this for: A, B or C?"*
- **It is missing, or this project is not in it** → run [First-time setup](#first-time-setup), then
  continue with the bug they gave you. Do not make them repeat it.

---

## Step 1 - Read the report

Pull out everything present in the note and the evidence. Look at a screenshot carefully: the URL bar,
the page title, error text, the browser, the device frame and the environment banner are all evidence.

| Field | Where it comes from |
|---|---|
| What is broken, and where | the note, the screenshot |
| Steps to reproduce | the note; otherwise the shortest likely path, marked **(assumed)** |
| Actual result | the note, the evidence |
| Expected result | the note; otherwise what the product clearly should do, marked **(assumed)** |
| Environment | the URL (dev/stage/prod), the browser and device seen or named, the app version |
| Evidence | a pasted link, or "screenshot attached in chat" |
| Severity, Priority | the words used ("crash", "blocker", "typo") and the user impact, per [bug-standard.md](bug-standard.md) |

**Never block on missing detail.** Fill what you can and mark the rest **(assumed)** or
**(not provided)**. Ask a question only when the bug cannot be understood without the answer.

---

## Step 2 - Check for a duplicate

Search the tracker for open bugs with the same key words (Jira: JQL
`project = KEY AND issuetype = Bug AND statusCategory != Done AND text ~ "words"`; GitHub:
`gh issue list --repo OWNER/REPO --state open --label bug --search "words"`).

If something looks like the same bug, show it in one line with its link and ask:
*"This looks like ABC-123. Add a comment there instead, or log a new bug?"* Otherwise say nothing
about it.

---

## Step 3 - Draft and confirm

Write the bug exactly in the format in [bug-standard.md](bug-standard.md), applying the project's
`overrides` from the config. Show the whole draft in chat, then on its own line:

> **Post this to <tracker> <project>?** Reply *yes*, or tell me what to change.

**Do not create anything until they say yes.** Apply their changes and show the draft again if
anything beyond a word changed.

---

## Step 4 - File it

| `tracker.type` | How |
|---|---|
| `jira` | Atlassian MCP `createJiraIssue`: the configured `cloud_id` and `project`, issue type `tracker.bug_type`, the Title as the summary, the rest as the description with `contentFormat: "markdown"`. Set priority through `additional_fields` `{"priority": {"name": "<mapped name>"}}`. If Jira refuses the priority, create without it; the priority is already in the description. If `tracker.start_status` is set, move the new issue there with `getTransitionsForJiraIssue` + `transitionJiraIssue`. |
| `github` | `gh issue create --repo <repo> --title "<Title>" --body-file <draft file> --label bug`. Write the draft to a temp file first so the markdown arrives intact. |
| `other` | Do not post. Give them the finished bug as one block, ready to paste. |

Then reply with **the link** and, if they pasted an image or video file, one line: *"Drag the
screenshot into the ticket. The tracker connection can't upload files."*

If filing fails, show the error in plain words, keep the draft, and offer to retry. Never report a
bug as filed when it was not.

---

## First-time setup

Ask these **one at a time**, in plain words. Skip any you can answer yourself.

1. **"Where does your team log bugs: Jira, GitHub Issues, or somewhere else?"**
2. Depending on the answer:
   - **Jira**: call `getAccessibleAtlassianResources`. If the Atlassian tools are missing or not
     signed in, tell them: *"Run `/mcp`, choose Atlassian and sign in, then say 'continue'."* With
     several sites, ask which one. Then ask **"What's the project key? (the letters before the
     number, like ABC in ABC-123)"**, confirm it exists with `getVisibleJiraProjects`, and read its
     issue types with `getJiraProjectIssueTypesMetadata` to find the bug type's exact name.
   - **GitHub**: check `gh auth status` (if signed out: *"Run `gh auth login` and say 'continue'"*).
     Ask **"Which repo? (owner/name)"** and confirm it with `gh repo view`.
   - **Anything else**: set `type: other`. They get copy-ready bugs.
3. **"Does your team do anything differently from the standard bug format?"** Show the field list from
   [bug-standard.md](bug-standard.md) in one line. Most people say no. Record anything they say under
   `overrides`.

Write `~/.qa-toolkit/projects.yaml`, adding to the file if it already exists:

```yaml
projects:
  - name: Gumdrop                     # what the QA calls it
    tracker:
      type: jira                      # jira | github | other
      cloud_id: example.atlassian.net # jira only
      project: GUM                    # jira project key
      repo: owner/name                # github only
      bug_type: Bug                   # the exact issue type name the project uses
      start_status: Ready For Dev     # optional: where new bugs should land
    overrides:                        # optional, only what the team does differently
      default_priority: Medium
      extra_fields: []                # e.g. ["Build number", "Customer"]
      routing: []                     # e.g. [{when: "billing pages", project: BILL}]
```

Finish with one line: *"All set. Bugs for <name> go to <tracker> <project>."* Then carry on with
their bug if they gave one, or offer: *"Try it: tell me about a bug and paste a screenshot."*

---

## Rules

- Plain, user-facing language: what the user did and saw, never code or guesses about the cause.
- One bug per ticket. If the note describes two problems, say so and offer to draft two.
- Everything you inferred is visibly marked **(assumed)**, so the reporter can catch it.
- Nothing is posted without an explicit yes.
