# Add a new style

Use this procedure when the user asks for a style that is not in `styles/`. The Swiss style folder is the model for the result.

## Procedure

1. **Agree the scope.** Ask the user for the movement or style, the period, the key designers or artists, and the sub-styles if any. Example: Swiss style has the Basel and Zürich schools. Also ask for any sources that the user already has.
2. **Make the folder.** Copy `styles/_template/` to `styles/<name>/`. Use a short lowercase name.
3. **Gather the sources.** Read encyclopedia articles, museum and archive pages, essays and primary texts. Prefer museum, archive and designer sources to blogs.
4. **Save the text.** Save each source as one markdown file in `styles/<name>/corpus/`. Keep the headings and the image captions. Remove the site navigation and the ads.
5. **Keep images out of the skill.** Save reference images in `<work folder>/_research/<name>/images/`, not in the skill folder. Images are large, and their rights can forbid sharing them with the skill. Record the path in `STYLE.md` and in `corpus/SOURCES.md`. Put other large research files for the style (for example a session archive) in `_research/<name>/` too.
6. **Write `corpus/SOURCES.md`.** For each item, give the file name, the URL, the date you read it and its license or rights status.
7. **Respect copyright.** The corpus is for private reference only. Do not save paywalled text. Do not publish or send the corpus. The repo `.gitignore` keeps each corpus out of git, except `SOURCES.md`.
8. **Write `STYLE.md`.** Use the template sections. Distill the corpus. Do not copy long passages. For each principle, give a rule that a script can apply, for example a grid, a type size ratio or a colour count.
9. **Write the sub-styles.** Give each sub-style its own traits and its own checklist.
10. **Start `lessons.md` and `examples.md`.** They can be empty at the start.
11. **Get approval.** Show `STYLE.md` to the user. Do not start a build before the user approves it.

## What makes a good STYLE.md

- It says what is essential to the style and what is open to experiment.
- It lists treatments as starting points, never as a closed list.
- It gives measurable rules where the style has them: a grid, proportions, type sizes, colour counts.
- It names typefaces and gives substitutes that are free or installed.
- Its review checklist has items that you can check on a rendered image.
