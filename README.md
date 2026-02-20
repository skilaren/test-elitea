# Quiz CLI

An interactive command-line quiz game for learning JavaScript and Node.js. Run in your terminal to pick a category, answer shuffled questions, see a progress bar and score, and review incorrect answers with explanations. No external dependencies — built with Node.js core modules.

## Project description

quiz-cli is a small, ESM-based Node.js CLI application that presents multiple-choice quizzes grouped by category. It reads question data from `data/questions.json`, shuffles questions each run, and provides a simple, interactive UX using Node's `readline` API.

Key points:
- Entry point: `index.js`
- Main logic: `src/quiz.js`
- Input helpers: `src/input.js`
- ANSI color helpers: `src/colors.js`
- Questions: `data/questions.json` (three sample categories included)
- Package: `package.json` (name: `quiz-cli`, version: `1.0.0`, license: MIT)
- Node requirement: >= 18 (ESM)

## Setup instructions

Prerequisites
- Node.js >= 18.0.0

Get the project
1. Clone the repo:
   - git clone <repo-url>
   - cd quiz-cli

2. (Optional) Install dependencies:
   - npm install
   - Note: there are no runtime dependencies currently; this step is kept for future use.

Data / adding questions
- Questions are stored in `data/questions.json`. Top-level structure:
  {
    "categories": {
      "javascript": {
        "name": "JavaScript",
        "questions": [
          {
            "question": "Example question?",
            "options": ["opt A", "opt B", "opt C"],
            "answer": 1,
            "explanation": "Why option 1 is correct."
          }
        ]
      }
    }
  }
- Important: `answer` is a zero-based index into the `options` array.
- To add a category or question, edit `data/questions.json` and follow the same fields (`name`, `questions`, each question with `question`, `options`, `answer`, optional `explanation`).

Project structure (high level)
- index.js — main CLI entry and control loop
- src/
  - input.js — readline-based input helpers (select, confirm, pressEnter)
  - quiz.js — Quiz class and quiz logic (shuffle, progress, scoring)
  - colors.js — ANSI color helpers
- data/questions.json — question bank
- package.json — metadata and scripts

## How to run the project

From the project root:

- Start the quiz:
  - npm start
  - or: node index.js

Usage walkthrough
1. On start you'll see a banner and a numbered list of categories. Enter the number of a category to choose it.
2. Choose how many questions to attempt (e.g., All / 3 / 5).
3. For each question, type the number of the option you think is correct and press Enter.
4. Between sections you may be prompted to press Enter to continue.
5. After the quiz you will see your score, a performance message, and a review of any incorrect answers including the correct option and any explanation.
6. You can choose to play again or exit.

Notes
- The CLI uses ANSI colors — terminals without ANSI support may not display colors correctly.
- There is a `test` script in `package.json` (`node --test`) but there are no tests included by default.

## Key features

- Interactive category selection (multiple categories in `data/questions.json`)
- Choose the number of questions per run (All / fixed counts)
- Shuffled questions each quiz (Fisher–Yates shuffle)
- Progress bar and per-quiz scoring
- Review of incorrect answers with optional explanations
- Minimal, dependency-free implementation using Node core modules
- Easily extensible: add categories/questions in `data/questions.json` or import `Quiz` class to embed in other scripts

## Development notes & extending

- To change visuals, modify `src/colors.js` or the banner in `index.js`.
- To persist scores, extend `Quiz.showResults()` to write to a file or database.
- To add automated tests, add test files and run `npm test` (package uses Node's built-in test runner).

## License

MIT (see `package.json`)
