---
name: creative-in-code
description: Make visual creative work in code, in a chosen art or design style. Use it for images and motion graphics (for example posters, motion posters and reels) that a script draws or animates. The style library starts with Swiss style (Basel and Zürich). It can also build a new style from references, such as essays, articles and images, before it makes the first piece. Do not use it for sound or music. Do not use it to generate images or video with an AI model.
---

# creative-in-code

This skill makes creative work in code. A script draws every pixel and frame. The skill holds the process. The style knowledge lives in `styles/<name>/`.

The **work folder** is the folder where the user keeps creative projects and research. Its path is in `work-folder.txt` in the skill folder. If that file does not exist, ask the user for the path before you save a file. Then save the path in `work-folder.txt`.

## Hard rules

1. **Code is the medium.** Never call a generative image, video or music model or API. Examples are DALL·E, Midjourney, Stable Diffusion, Sora, Runway, Suno and Udio. Do not ask the user for an API key for one of these services. You can trace, filter, mask and transform a photo that the user supplies.
2. **No library is prescribed.** Use the tools that give the best result. You can install libraries and tools from reputable sources: PyPI, npm, Homebrew or an official project release. Tell the user what you installed and why. Install code tools only. Never install a generative model.
3. **Keep libraries current.** This skill names no versions, so it cannot go stale. For each project:
   1. Make a fresh environment in the project folder (for example `.venv`) with current stable versions.
   2. Read the current docs of a library (through Context7 if it is available) before you use its API.
   3. Record the exact versions in the project (`requirements.txt` or a lockfile). The script must run again as built.
   4. If you find a library bug or a workaround, record it in the style's `lessons.md` as **perishable**, with the date.
4. **Respect the rights on sources.** Use photos, fonts and logos only as the user allows. If the user marks an item private or not royalty-free, keep each output that uses it private. Put `PRIVATE` in its file name. Do not send it anywhere. To get a font that is not installed, follow `references/font-sources.md`.
5. **Ask, do not assume.** If the brief is unclear, ask before you write code. If you invent a subject, a title or copy, say so.

## Process

Do the steps in this order. Do not write code before the user approves step 4.

### 1. Style

1. List the folders in `styles/`. Do not list `_template`.
2. For each style, read the first lines of its `STYLE.md`. Show its one-line summary and its sub-styles (for example, Swiss: Basel, Zürich).
3. Ask the user which style to use. Also ask which sub-style, or which mix of sub-styles.
4. If the user wants a new style, do the procedure in `references/new-style.md`. Stop after the new `STYLE.md` and wait for the user to approve it.
5. Read the chosen `STYLE.md` and `lessons.md` in full. Read `examples.md` if you need a reference for how a treatment was built.
6. If the style's `corpus/` folder has only `SOURCES.md`, the source texts are not saved yet. When you need more detail than `STYLE.md` gives, get the sources in `SOURCES.md`. Use steps 4–7 of `references/new-style.md`.

Before you rely on a **perishable** lesson, check that it is still true.

### 2. Content

Ask for these items:

- The subject: an event, a brand, a product, an exhibition or something else.
- The copy: title, dates, times, place, URL and any other text.
- The assets: photos, logos, fonts, a brand profile or a design system.
- A website or document to read for content.

If the user lets you choose the subject or copy, invent it and say what you invented. Avoid a title that only names what the photo shows. For a brand, read its brand profile or design system. If there is none, write a short brand profile in the project folder.

Save each asset in the project `source/` folder. An image pasted into the chat is not always saved as a file. If you cannot find the file, ask the user for a path.

### 3. Format

Ask about these items. Do not assume a default for them.

- The medium: still, motion, or both.
- The size and the aspect ratio. For motion, also the length, the frame rate and the platform.
- For a still, the print size (for example A2). The default output for a still is print quality: 300 dpi at the print size. Make a lower resolution only when the user asks for screen output.
- How many pieces to make: one, a pair, a set, or any other number.
- How the pieces split across the sub-styles.
- The rules for the photo: for example, "one piece uses the photo unedited, all others derive from it".

When the medium is known, read `references/craft-notes.md`.

### 4. Plan the set

Before you write code, show the plan. Give one line per piece: its file name, its sub-style, its treatment and its layout. When there are several pieces, give each piece a different treatment. Wait for the user to agree, or apply the changes that the user asks for.

### 5. Build in code

1. Make a project folder at `<work folder>/<project>/`, for all styles. Put inputs in `source/` and outputs in their own folder (for example `posters/` or `motion/`). Do not put style research in a project folder. The text corpus goes in the skill (`styles/<name>/corpus/`). Reference images go in `<work folder>/_research/<name>/`.
2. Make the environment and record the versions (hard rule 3).
3. Write one script per project. The script is the recipe. It must make all the outputs again from `source/` with one command.
4. Use the grid, type, color and treatments in `STYLE.md`. The lists in `STYLE.md` are starting points. You can invent a new treatment if it is rooted in the style.
5. Measure the photo before you use it. Trace the subject, or make a mask of it, when the brief says the background is not relevant.
6. Do not use a photo from a reference website in the final output. Make your own images.

### 6. Review before you show

1. Render each piece and look at it at full size.
2. Make a contact sheet of the set and look at it.
3. Check each piece against the review checklist in `STYLE.md` and against its sub-style checklist.
4. Check the brief: the copy is complete and correct, and the text is legible.
5. Look for text that collides, text that runs past its column, clipped letters, unintended marks and a layout that is too heavy at one end.
6. For motion, look at sampled frames, the first 3 seconds and the last frame.
7. Fix the problems, then do the review again.

### 7. Deliver

1. Send the files to the user, with the contact sheet first.
2. Say what you invented (subject, title, copy, venue, dates).
3. Say what is uncertain and which pieces are weakest.
4. Mark each private output as private.

### 8. Iterate and record

1. Apply the user's feedback. Keep the old version in a `v1/` folder when you replace a piece.
2. At the end, add each new lesson to the style's `lessons.md`. Give it a date and a kind:
   - **durable**: a lasting preference or rule.
   - **situational**: true for that brief only.
   - **perishable**: true for now only, for example a library bug or a missing font.
3. Add each lesson about the medium (not about the style) to `references/craft-notes.md`.
4. Add the project to the style's `examples.md`.

## Files

- `references/new-style.md`: how to build a corpus and a `STYLE.md` for a new style.
- `references/craft-notes.md`: lessons that apply to a medium in all styles.
- `references/font-sources.md`: where to get licensed fonts.
- `styles/_template/STYLE.md`: the skeleton for a new style.
- `styles/<name>/STYLE.md`: principles, sub-styles, grid, type, color, treatments and the review checklist.
- `styles/<name>/lessons.md`: dated feedback and what fixed it.
- `styles/<name>/examples.md`: earlier projects, as reference only.
- `styles/<name>/corpus/`: the source texts and `SOURCES.md`.
