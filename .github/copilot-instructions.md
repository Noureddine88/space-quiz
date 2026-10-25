# Copilot instructions

## Build, test, and lint

There are no configured build, test, or lint commands. The app runs directly from `index.html` in a browser without a server or dependencies. For a browser smoke test, open that file and check answer selection, correct and incorrect feedback, score and progress updates, the results screen, and replay.

## Architecture

`index.html` contains the complete application: semantic page markup, all styles in one `<style>` block, the question bank, and vanilla JavaScript in one `<script>` block. Keep it self-contained; there is no package manager, bundler, framework, or separate asset pipeline.

The quiz data is the `questions` array. `renderQuestion()` builds the current question's answer buttons, `selectAnswer()` tracks a choice, and `lockAnswer()` scores it and advances progress. `showResults()` replaces the quiz view with the final score and reaction; `restart()` resets quiz state. Keep the question data, progress maximum, displayed question count, and result score in sync when changing the quiz length.

## Codebase conventions

- Question entries use `question`, `answers`, zero-based `correct`, and `fact`; the answer order is significant. Update the correct index whenever answer choices are reordered.
- JavaScript is plain browser JavaScript with DOM queries against stable element IDs. Keep dynamic question and feedback copy assigned as text, and preserve the existing control flow for selecting, locking, advancing, finishing, and replaying.
- CSS is colocated with the markup. Shared colors and surfaces are custom properties in `:root`; light-theme overrides belong in `@media (prefers-color-scheme: light)`. Preserve both themes when adding or changing colors.
- Keep the responsive narrow-column layout, visible keyboard focus, semantic buttons, screen-reader announcements, and `prefers-reduced-motion` handling when adjusting the UI. The progress bar exposes its value through `aria-valuenow`, so update it alongside the visual fill.
