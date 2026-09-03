# Haikufy

An agent instruction file that makes a coding assistant close each answer with a
haiku — one that names the **problem**, the **paradox** at its centre, and the
**solution**.

It is not decoration. The middle line forces the agent to say *why the problem was
hard*, and an agent that cannot name the tension usually has not understood the
bug. The poem is a comprehension check that happens to be three lines long.

## The three lines

| Line | Syllables | Carries |
|------|-----------|---------|
| 1 | 5 | The problem — the symptom as you met it |
| 2 | 7 | The paradox — why it stayed hidden |
| 3 | 5 | The solution — the move that resolves it |

For example, after an answer about a service falling over under load:

    One request times out
    each retry adds to the load
    back off, and add noise

## Install

**As a GitHub Copilot custom agent** — copy the file into the repo you want it in:

```bash
mkdir -p .github/agents
curl -o .github/agents/haikufy.agent.md \
  https://raw.githubusercontent.com/<owner>/haikufy/main/haikufy.agent.md
```

Then select **haikufy** when choosing an agent.

**Always on instead** — if you want every answer in a repo to close this way, paste
the body (everything below the `---` frontmatter) into `.github/copilot-instructions.md`
or `AGENTS.md`. Those load unconditionally, so no agent selection is needed.

The file is plain Markdown with YAML frontmatter and no dependencies, so it also
works as a skill or system prompt fragment for other assistants.

## It knows when to shut up

The instructions tell the agent to skip the haiku for bare facts, and for failures,
refusals and bad news — where a poem reads as flippancy. It stops permanently if
asked. Always-on whimsy is how a feature like this gets switched off.

## A caveat

Language models are unreliable syllable counters. The 5-7-5 rule is stated and the
examples are correct, but expect the occasional six-syllable line. If that matters
to you, add a validator rather than more prose.
