# Bug standard

Every bug the toolkit writes has this shape, whatever the project. A team adds to it through
`overrides` in its config. It does not remove anything.

## Format

```markdown
**Title:** <what is broken> - <where> [<platform, if it only happens there>]

**Severity:** <Critical | Major | Minor | Trivial>  ·  **Priority:** <High | Medium | Low>

## Description
<One or two sentences: what is broken, where, and who it affects.>

## Steps to reproduce
1. <step>
2. <step>
3. <step>

## Actual result
<What happens.>

## Expected result
<What should happen.>

## Environment
- **Env:** <dev | stage | prod | not provided>
- **URL / screen:** <...>
- **Browser / device:** <...>
- **Build / version:** <... or not provided>

## Evidence
<Link, or "screenshot attached in chat - attach to this ticket">
```

## Title

Short and searchable: the broken behaviour first, then where. No cause, no code.

- Good: `Save button does nothing - Profile settings [Safari]`
- Bad: `Bug in profile`, `onClick handler not firing in ProfileForm.tsx`

## Severity: how bad is it for the user

| Severity | Meaning | Examples |
|---|---|---|
| **Critical** | Blocks a core flow for everyone, loses data, or is a security issue; no workaround | can't log in, payment charged twice, data deleted |
| **Major** | A main feature is broken or wrong; a workaround is painful or missing | filter returns wrong results, email never arrives |
| **Minor** | Works, but wrongly or awkwardly; an easy workaround exists | wrong error message, layout broken on one screen size |
| **Trivial** | Cosmetic only | typo, misaligned icon, wrong colour |

## Priority: how soon to fix it

Default to **Medium** unless the report says otherwise or the severity makes it obvious. Critical
almost always means **High**. Priority is the team's call, so state the guess and let them change it.

| Priority | Meaning |
|---|---|
| **High** | Fix now or in the current release |
| **Medium** | Fix in an upcoming release |
| **Low** | Fix when convenient |

If the tracker names priorities differently (Jira's `Highest`, `P1`), map these three onto its names
and say which names were used.

## Marking guesses

Anything not stated in the report or visible in the evidence is marked **(assumed)**. Anything
unknown is **(not provided)**. A reviewer should be able to tell at a glance what was observed and
what was inferred.
