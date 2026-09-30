# creative-in-code

An agent skill that makes images and motion graphics in code, in a chosen art or design style. A script draws every pixel and frame. The skill never calls an image or video model.

It is written for Claude Code, but any agent that reads a `SKILL.md` file and can run code can use it.

## How it works

The skill works in two stages.

### 1. Build a style from references

A style comes before the first piece. To add a style, the agent does these steps:

1. It agrees on the scope with you: the movement, the period, the key designers and the sub-styles.
2. It reads the references: encyclopedia articles, museum and archive sites, essays and primary texts. It also collects reference images and measures them: the grid, the type sizes, the colors.
3. It saves the texts in a private corpus in the style folder. It saves the images in your work folder, outside the skill.
4. It writes `STYLE.md`: a summary of the corpus as rules that a script can apply. The rules cover the grid, the type, the color, the image treatments and a review checklist for each sub-style.
5. It shows you `STYLE.md`. It does not build anything until you approve it.

The full procedure is in `references/new-style.md`.

### 2. Make work in that style

For each brief, the agent does these steps:

1. It asks which style and sub-style to use.
2. It asks for the content: the subject, the copy and your photos.
3. It asks for the format: still or motion, size, print or screen, and the number of pieces.
4. It shows a plan of the set. It writes no code until you approve the plan.
5. It writes one script for the project. The script makes all the outputs again with one command.
6. It renders each piece and checks it against the style checklist before it shows you.
7. It applies your feedback. Then it records each new lesson in the style's `lessons.md` or in `references/craft-notes.md`.

The skill learns from each project. The next project starts from these lessons.

## The Swiss style: a reference guide

`styles/swiss/` is a complete style. Use it as a model of a finished style, or use it as it is.

- `STYLE.md` covers the International Typographic Style of 1950s–60s Switzerland, with its two schools: Basel and Zürich.
- `examples.md` lists image and motion treatments that worked in earlier projects.
- `corpus/SOURCES.md` lists the six sources that `STYLE.md` is built from. It also says where to find the reference images.

The source texts are not in this repo. The first time your agent needs more detail than `STYLE.md` gives, it reads `SOURCES.md` and builds its own local corpus.

## What is not in this repo

- **Source texts and reference images.** They are copyright of their owners. `corpus/SOURCES.md` gives the links. The `.gitignore` keeps every corpus folder out of git, except `SOURCES.md`.
- **Style lessons from earlier projects.** `lessons.md` starts empty. Your agent adds your own lessons as you work. The general craft lessons stay in `references/craft-notes.md`.
- **Fonts.** `references/font-sources.md` lists sources of free, licensed fonts.

## Install

For Claude Code, clone the repo into your skills folder:

```bash
git clone https://github.com/videodromejockey/creative-in-code ~/.claude/skills/creative-in-code
```

For another agent, copy the folder to the place where the agent loads skills.

The agent writes new styles and lessons into this folder, so install it where the agent can write.

Then ask your agent for a poster, or ask it to build a new style. The first time, it asks for your work folder: the folder for your projects and research. It saves the path in `work-folder.txt`, which git ignores.

## Update

As you work, your agent edits some files that git tracks: each style's `lessons.md` and `examples.md`, and `references/craft-notes.md`. A plain `git pull` can then stop on a conflict. You do not have to fix it yourself. Ask your agent to update the skill.

**Agent:** to update the skill, do these steps in the skill folder.

1. Commit the user's local changes: `git add -A` and `git commit -m "Local lessons"`. If git has no user name or email, set them for this repo only.
2. Run `git pull --no-rebase`.
3. If a file conflicts, keep both sides: the user's lines and the new lines from the repo. Do not ask the user to resolve it.
4. Commit the merge. Tell the user what changed.

## Tools

The skill prescribes no library. For each project, the agent makes a fresh environment with current versions and records them. Earlier projects used Python with skia-python, NumPy and fontTools, ffmpeg for video, and Blender for 3D characters.

## Files

```
SKILL.md                      the process and the hard rules
references/
  new-style.md                how to build a new style
  craft-notes.md              lessons for each medium, in all styles
  font-sources.md             where to get licensed fonts
styles/
  _template/STYLE.md          the skeleton of a new style
  swiss/
    STYLE.md                  principles, sub-styles, grid, type, color, treatments, checklists
    lessons.md                your lessons, dated
    examples.md               treatments from earlier projects
    corpus/SOURCES.md         the sources, with links and rights
```

## License

MIT. See `LICENSE`. The license covers the files in this repo. It does not cover the sources in `SOURCES.md`, which belong to their owners.
