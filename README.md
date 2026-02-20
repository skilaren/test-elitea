# Quiz CLI — interactive command-line quiz game for learning JavaScript

An interactive command-line quiz game written in plain Node.js (ESM). Pick a category, choose how many questions to attempt, answer multiple-choice questions, and get a results summary with explanations for incorrect answers.

Badges
- Node: >= 18.0.0
- License: MIT

(Note: No external dependencies — the app uses Node built-ins and ANSI escape codes for styling.)

## Features

- Interactive CLI with category selection and configurable question count
- Shuffles questions and tracks score
- Progress bar and per-question prompts
- Results summary with incorrect answers and optional explanations
- No external dependencies — uses built-in readline and ANSI color codes
- ESM (type: "module") ready

## Requirements

- Node.js >= 18.0.0 (project uses ES Modules and modern Node features)
- Works on macOS, Linux, and Windows terminals that support ANSI colors

## Installation

1. Clone the repository:
   git clone <repo-url>
   cd quiz-cli

2. (Optional) Install dependencies:
   npm install
   Note: There are no runtime dependencies; running npm install is safe but not required.

## Running the app

- Start the CLI:
  npm start
  or
  node index.js

- Run tests (if you add tests later):
  npm test
  (Currently `npm test` runs `node --test` — add tests under a `test/` folder.)

The app is an interactive loop:
- Pick a category from the list
- Choose how many questions to answer
- Answer questions by typing the option number and pressing Enter
- Press Enter between questions when prompted
- At the end you get a score and can review incorrect answers, then choose to replay or exit

## Data format / Adding questions

Quiz content is stored in `data/questions.json`. Structure:

{
  "categories": {
    "<category-id>": {
      "name": "Display Name",
      "questions": [
        {
          "question": "Question text",
          "options": ["option A", "option B", "option C"],
          "answer": 0,
          "explanation": "Optional explanation shown on review"
        }
        // more questions...
      ]
    }
    // more categories...
  }
}

Notes:
- `answer` is a 0-based index corresponding to the correct option in `options`.
- To add a new category or question, edit `data/questions.json`. Follow the structure above.
- Example question object:

{
  "question": "Which method converts a JSON string into a JavaScript object?",
  "options": ["JSON.stringify()", "JSON.parse()", "JSON.toObject()"],
  "answer": 1,
  "explanation": "JSON.parse() parses a JSON string and returns the corresponding JavaScript value or object."
}

## Key files

- package.json — project metadata and scripts (name: `quiz-cli`, version: `1.0.0`, scripts: `start`, `test`, engines: `node >= 18.0.0`, license: MIT)
- index.js — CLI entrypoint and main app loop (loads data, prompts for category/count, instantiates Quiz)
- data/questions.json — categories and question data
- src/quiz.js — core Quiz class: shuffle, ask questions, track score, render progress and results
- src/input.js — readline-based helpers: createInterface, prompt, select, confirm, pressEnter
- src/colors.js — small ANSI color helper utilities (no external deps)

## Scripts

- npm start — run the app (node index.js)
- npm test — run Node's test runner (`node --test`) — add tests later under `test/`

## Development / Contributing notes

- Project uses ES Modules (package.json includes "type": "module").
- To modify prompts or the UI, edit `src/input.js`. Core quiz logic is in `src/quiz.js`.
- To add categories/questions: edit `data/questions.json`.
- Suggested improvements:
  - Add automated tests for Quiz class behavior (shuffle determinism, scoring, progress rendering)
  - Add CLI flags (e.g., `--category`, `--count`) for non-interactive or scripted runs
  - Publish as an npm CLI package (add `bin` field in package.json)
  - Add CONTRIBUTING.md and PR/issue templates

## Example terminal transcript

$ npm start
Select a category:
  1) JavaScript
  2) General
Choose number of questions (1-10): 3

Question 1/3:
Which method converts a JSON string into a JavaScript object?
  0) JSON.stringify()
  1) JSON.parse()
  2) JSON.toObject()
Your answer: 1
Correct!

Press Enter to continue...

--- Results ---
Score: 3 / 3
Great job! Replay? (y/n)

## License

MIT (see package.json)

---

If you'd like, I can:
- Generate a CONTRIBUTING.md
- Scaffold tests for the Quiz class
- Add CLI flags for non-interactive use

Which would you like next?
