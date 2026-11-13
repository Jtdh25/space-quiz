# Copilot instructions

## Project shape

This is a dependency-free, browser-only quiz. The entire application is in
`space-quiz.html`; it contains the semantic HTML shell, theme-aware CSS, quiz
data, and the JavaScript state machine. There is no server, package manager,
build pipeline, test runner, or lint configuration.

The page is structured as one centered card:

- The header contains the mission-control title and light/dark theme toggle.
- The `#quiz` section renders the current question, score, progress bar,
  answer buttons, feedback, and next button.
- The `#result` section is hidden until all questions are answered, then shows
  the final score, message, and restart control.
- The `questions` array is the source of truth for all ten questions,
  answer indexes, and explanatory facts. `current`, `score`, and `answered`
  are the only mutable quiz state.

## Commands and validation

There are no repository-defined build, test, or lint commands. Open the file
directly in a browser:

```text
file:///C:/RP/AY2026%20Sem%202/C334%20Agentic%20AI%20Systems/space%20quiz/space-quiz.html
```

For a browser smoke test, verify that:

1. Native buttons can be reached in logical keyboard focus order.
2. Selecting the correct answer increments `#score`, marks the answer
   `.correct`, and produces `.feedback.good`.
3. Selecting an incorrect answer leaves the score unchanged, marks the
   selected answer `.wrong`, highlights the correct option, and produces
   `.feedback.bad`.
4. The next button advances through all ten questions.
5. The final action hides `#quiz`, shows `#result`, and displays the final
   score and restart button.
6. The theme toggle works in both light and dark modes.

When changing quiz behavior, use the integrated browser against the local
`file://` URL rather than introducing a server or build tool.

## Implementation conventions

- Keep the project self-contained in the single HTML file unless the user
  explicitly requests a different structure.
- Preserve the existing DOM IDs (`quiz`, `result`, `question`, `options`,
  `feedback`, `nextButton`, `score`, and related IDs); the JavaScript updates
  the UI through these hooks.
- Add or edit quiz content in the `questions` array. `answer` is a zero-based
  index into that question's `options` array.
- Render answer choices as native `<button type="button">` elements so they
  remain keyboard accessible. Disable all choices after an answer is selected.
- Keep answer selection guarded by the `answered` flag so a question can only
  affect the score once.
- Use the existing CSS custom properties for colors and provide matching
  values in both `:root` and `[data-theme="dark"]`.
- Preserve the visual language: centered narrow layout, mission-control
  typography, subtle hex-grid background, animated feedback, and restrained
  space-themed decoration.
- Respect `prefers-reduced-motion` when adding animations or transitions.
- Keep feedback text in the existing live region (`#feedback`) and preserve
  the `.good`/`.bad` class distinction for styling and smoke tests.
