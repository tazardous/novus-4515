# Novus 4515 Mathematician PR

Emulator of the 1976 programmable Novus. Same three-level RPN engine as the 4510,
plus 100 steps of learn-mode programming. One self-contained HTML file, no
dependencies, no build step, no network calls at runtime.

## Deploy

```bash
gh repo create novus-4515 --public --source=. --remote=origin --push
```

Settings -> Pages -> Deploy from a branch -> main -> / (root). Then open the URL in
Chrome on the phone and use the menu to Add to Home screen.

Everything is relative-pathed, so a project subdirectory works.

## Behaviour

The register model is the 4510's, verbatim from Appendix A: three levels, nothing
replicated downward, four distinct classes depending on the operation. Appendix C's
error conditions are implemented exactly. Registers truncate to eight positions
after every operation.

Programming is a keystroke recorder with no branching, labels or subroutines:

- **LOAD** — `start` wipes storage and arms recording. Keys are recorded and executed
  as you press them. `halt` records a pause for a variable; digits keyed straight
  after one are not stored. Digits without a preceding `halt` are constants.
  `skip` ends one program and begins the next. `del` erases the last step.
- **STEP** — `start` executes one step per touch.
- **RUN** — `start` runs to the next `halt` or resumes from one. `skip` abandons the
  rest of the current program; n-1 touches reach the nth program.

An F-shifted key is one step. Over 100 steps, or deleting a `skip`, shows all
decimal points.

## Updating

Edit, bump `CACHE` in `sw.js`, push. Without the version bump the phone keeps
serving the cached copy.
