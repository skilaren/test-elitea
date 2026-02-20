# Quiz CLI — An interactive command-line quiz game for learning JavaScript

An interactive command-line quiz game written in modern Node.js (ESM). Load question banks from data/questions.json, select categories, answer multiple-choice questions, and review your score and explanations.

Badges
- Version: 1.0.0
- License: MIT
- Node engine: >= 18.0.0

Prerequisites
- Node.js >= 18.0.0 (ES modules and modern Node APIs are used)
- Git (optional, for cloning)

Quick setup and install
1. Clone the repo:
   git clone <repo-url>
2. Enter project folder:
   cd <repo-folder>
3. Install dependencies:
   npm install
   (There are currently no external dependencies, but run this to populate node_modules if/when added.)

How to run
- Start the app:
  npm start
  or
  node index.js

- Run tests (script is present but this repository currently has no test files):
  npm test
  (Runs `node --test` which will look for test files if you add them.)

Project structure (short)
- index.js — CLI entrypoint and main loop. Loads data/questions.json and starts the interactive quiz. Use Node >= 18 to run.
- package.json — metadata, scripts (start/test), engine requirement, license.
- data/questions.json — question bank organized by categories. See "Data format" section below.
- src/colors.js — ANSI color helpers and convenience functions used to style terminal output (no external deps).
- src/input.js — CLI input helpers (readline wrapper). Exposes:
  - createInterface(...) — create custom readline interface
  - prompt(...) — ask a free-text question
  - select(...) — show a list and return a selection as { index, value }
  - confirm(...) — yes/no prompt returning a boolean
  - pressEnter(...) — wait for Enter key
- src/quiz.js — core Quiz class: shuffling, asking questions, tracking score, rendering progress, and showing results. Primary extension point for features like timed quizzes, alternate scoring, or persisting results.

Data format (data/questions.json)
- Top-level: an object mapping category IDs to category objects.
- Category object:
  - name: string
  - questions: array of question objects
- Question object fields:
  - question: string
  - options: array of strings (choices)
  - answer: number — index of the correct option in the options array (zero-based)
  - explanation: string (optional) — shown on review or after answering

Minimal example to add a category/question
{
  "javascript_basics": {
    "name": "JavaScript Basics",
    "questions": [
      {
        "question": "What does === check in JavaScript?",
        "options": ["Value equality only", "Type and value equality", "Reference equality"],
        "answer": 1,
        "explanation": "=== checks both type and value equality."
      }
    ]
  }
}
Place new entries into data/questions.json under a new key (category id). Keep the answer field as the zero-based index of the correct option.

Key features
- Interactive CLI flow: choose category, number of questions, and run through quiz rounds.
- Multiple-choice questions with colorized terminal output (via src/colors.js).
- Progress display while taking the quiz and a final results summary.
- Explanations for answers and a review of incorrect responses.
- Input helpers: select (returns { index, value }), confirm (returns boolean), prompt, and pressEnter to make writing new prompts easy.
- Extensible: src/quiz.js and src/input.js are clear extension points for timed quizzes, different scoring, or persistence.

Contributing
- Add or edit questions in data/questions.json. Follow the schema above.
- Coding conventions:
  - Project uses ES modules (type: "module" in package.json). Use import/export and Node >= 18 APIs.
  - Keep code simple and dependency-free where possible.
- To run locally:
  - npm start
- To contribute:
  - Fork → make changes → open a pull request with a clear description of changes and any sample questions added.
- Consider adding tests (there is a test script but no tests yet). Use Node's built-in test runner (node --test).

Notes & troubleshooting
- Make sure your Node version is >= 18. Older Node versions may fail due to ESM and node: prefixed imports.
- package.json includes a "test" script that runs node --test. If you add tests, place them in the repository (e.g., *.test.js) so the test runner picks them up.

License
- MIT — see LICENSE file or the license field in package.json.

Future ideas
- Timed mode and per-question time limits
- Persisting high scores to a file or remote store
- Support loading custom question files via CLI flags
- Add unit/integration tests and CI
- Export results or progress tracking for learners

If you want, I can:
- Create the README.md file in the repo for you, or
- Generate a CONTRIBUTING.md template and a small example test file to get started with tests. Which would you like next?
