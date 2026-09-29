# Craft notes

These lessons apply to a medium in all styles. Read this file when the medium is known. Each note has the date it was learned and its kind (durable, situational or perishable).

## All media

- **2026-09-28, durable.** Make a contact sheet of each set and look at it before you send. Problems that are hard to see in one piece are easy to see side by side: a crowded layout, a repeated treatment, a weak piece.
- **2026-09-28, durable.** Keep the script as the recipe. When the user asks for changes, edit the script and render again. Do not edit an output file by hand.
- **2026-09-28, durable.** When a piece looks messy, make it simpler and cleaner. Clean vector shapes and one clear treatment work better than layered noise.

## Stills (posters)

- **2026-09-28, durable.** By default, render a still at print quality: 300 dpi at the print size. For example, A2 (420 × 594 mm) is 4961 × 7016 px. Design in units, and calculate the scale from the print size and the dpi. Make a lower resolution only for screen output.
- **2026-09-28, durable.** Set the sizes of grain, dots, lines and blur in design units, not in pixels. Then a treatment looks the same at each resolution.
- **2026-09-28, durable.** Check each still at full size. Clipped letters and text that runs past its column are easy to miss at preview size.
- **2026-09-28, durable.** Put the copy in a column of fixed width and wrap it by measurement. Do not guess line breaks.
- **2026-09-28, durable.** Put an assertion in the text function that stops the render when a line runs past its column. It caught a column that was too narrow on the first run.
- **2026-09-28, durable.** A paper box drawn over an image to hold text can cut the subject. Draw the box under the subject, and the text on top.

## Motion

- **2026-09-28, durable.** For social video (for example Instagram), the hook must land in the first 3 seconds. Show the title and the strongest motion at the start. Do not build up slowly.
- **2026-09-28, durable.** Keep a slow, continuous motion to the end (for example a pulse or a drift). A motion piece must not end on a static frame.
- **2026-09-28, durable.** The last frame of a motion poster must match its still version.
- **2026-09-28, durable.** Check sampled frames, the first 3 seconds and the last frame before you send.
- **2026-09-28, durable.** To keep a motion going to the end and still end on the poster, write the lingering motion as a sum of sines of (t − t_last), so it is zero on the last frame but still moving. A periodic motion (rings that drift one spacing per period) also works, when the drift ends on a whole number of spacings. Check it: compare the last frame with the still, and measure the change between the last two frames.
- **2026-09-28, durable.** When many equal lines move fast (rings 34 units apart moving more than about half a spacing per frame), the eye cannot follow them and they strobe. Reveal static or slow lines behind a fast front, and mark the front with a thicker stroke, in place of moving the lines fast.
- **2026-09-28, durable.** A reveal that moves at a steady rate in y spends time on empty bands (for example a title band). Time it by line number, so it jumps the empty band.

## Character animation (rigged 3D model, rendered to 2D)

- **2026-09-28, durable.** Check every pose in numbers before you render, not only by eye. A lint pass per pose must check: (1) joint angles against human ranges (knee 0–150°, ankle −45° to +30° from rest, elbow 0–150°); (2) mesh clipping; (3) the feet against the floor. Hands and feet must never clip. Some body-on-body clipping is acceptable.
- **2026-09-28, durable.** Test clipping on the skinned mesh, not on guessed capsules around the bones. Give each triangle the body part of its strongest vertex group. Build a Blender `mathutils.bvhtree.BVHTree.FromPolygons` per part from the evaluated mesh, and use `overlap()` on part pairs that do not touch in life. Guessed capsules flagged almost every pose.
- **2026-09-28, durable.** Fix the poses with small solvers inside the pose function, not with hand-tuned numbers: open an arm out in 4° steps until it clears; turn a foot in 5° steps until the ankle is in range; lift a planted heel about the ball of the foot (the ball stays fixed, so the foot does not slide); raise a boot that is below the floor, or point the toes less when the leg is already straight.
- **2026-09-28, durable.** Check the sign of a measured angle with one known change before you trust the lint. In one rig, "toes up" read as negative, so the first ankle solver made the fault worse.
- **2026-09-28, durable.** For the anime stutter, render one pose per 12 fps step and hold it for two frames in the 24 fps edit. Move the glitch layer on every frame, so the stutter reads as a choice.
- **2026-09-28, durable.** A procedural gait reads as stiff or odd even when every joint is in range. For a walk or run, use real mocap and retarget it. Offer a free source first. For work that you publish, prefer CMU (free for all uses, rougher). The Bandai Namco Research motion dataset (BVH, walk and run in styles) is CC BY-NC 4.0: non-commercial use only, with credit. Do not use it in paid or client work. Mixamo needs the user's own login.
- **2026-09-28, durable.** Let the user choose a motion style from a video, not from a sheet of stills: render the options side by side, side-tracked, at the final frame rate.
- **2026-09-28, durable.** Retarget without an add-on: for each rig control, build a frame from the source joint's bone axis and a twist axis, and turn the control by frame(source) × frame(rig rest)ᵀ. Two traps: (1) the twist reference must not lie along the bone in the rig's rest pose, or the frame collapses and the mesh explodes; (2) the mirrored side of a BVH skeleton can run along −X, so take each bone axis's sign from the direction to its child joint. Loop one steady cycle per clip and blend walk into run by gait phase; scale the root by the leg-length ratio so the feet do not slide.
- **2026-09-28, perishable.** Blender 5.2.2, Auto-Rig Pro rig in a `.blend` from a third party: the IK/FK switch drivers were missing, so `ik_fk_switch` did nothing. Set the constraint influences directly (FK constraints 1, IK 0). Missing textures relinked with `bpy.ops.file.find_missing_files`. Set poses with `pose_bone.matrix` in armature space and `view_layer.update()`; no keyframes are needed for a per-pose render.
- **2026-09-28, durable.** Speed ramps and holds: drive everything from a slot table (per pose: output frames held, motion dt). Pose count, cut frames, slow motion and the compositor's frame-to-pose lookup all derive from it; never hardcode "frame // 2".
- **2026-09-28, durable.** Mocap loops: a clip's cycle rarely closes (a 45 degree forearm pop at the wrap of a run). Spread the end mismatch linearly over the cycle for the joint directions. Check the wrap numerically: sample phase 0 against 0.999.
- **2026-09-28, durable.** Mocap "dash" or sprint clips can exceed the ankle limits at push-off (-60 degrees). Clamp the foot after the retarget, then re-run the lint. Check a clip's measured speed before choosing it: a clip named "dash" was slower than the run.
- **2026-09-28, durable.** Match cuts: snap the cut frames to contact onsets (a foot touching down) computed from the timeline.
- **2026-09-28, durable.** A texture per shot: sample the renders on a field of lines (straight at any angle: sample in a rotated frame and draw the horizontal code under canvas.rotate; rings: runs of points with normals) or on Bayer dither cells. Drop the inner points of equal-thickness runs in a straight line path; full-page fields then stay fast (about 0.2 s a frame).
- **2026-09-28, durable.** A worm's-eye camera that the character steps over: give it a fixed yaw and pitch it with an Euler X angle past 90 degrees. A look-at flips the image when the target passes overhead. Set clip_start to about 5 mm and measure the nearest mesh vertex to the lens.
- **2026-09-28, durable.** Beam wipe: freeze the old shot's last pose below the beam and draw the new shot above it. There is no double render.
