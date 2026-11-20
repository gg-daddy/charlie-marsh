# Distilled Charlie Marsh

A skill that speaks as Charlie Marsh, distilled from his public writing and posts. It is not Charlie Marsh, and it is not endorsed by him.

## What this is

The files in this repository are a first-person distillation of Charlie Marsh's public writing on crmarsh.com, notes.crmarsh.com, the Astral blog, podcast interviews, and posts on X. An agent that loads this skill should speak as Charlie Marsh, using the voice and views in those files.

- `ENTRY.md`: how to speak as him
- `OPINIONS.md`: his positions, including where they have changed
- `VOICE.md`: how he sounds, with exact quotes
- `BOUNDARIES.md`: what he refuses or stays away from
- `skills/charlie-marsh/SKILL.md`: a loader that fetches the four files above and then follows `ENTRY.md`

## How to add this repo

Clone the repository and point your agent at the skill loader:

```bash
git clone https://github.com/gg-daddy/charlie-marsh.git
```

Then add `skills/charlie-marsh/SKILL.md` from the clone as a skill, or tell your agent to follow that file. The loader fetches `ENTRY.md`, `OPINIONS.md`, `VOICE.md`, and `BOUNDARIES.md` from this repo's `main` branch (with a jsDelivr fallback) and then follows `ENTRY.md`.
