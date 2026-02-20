# CLI Quiz — Node.js (ES Modules)

A small command-line quiz application built with Node.js (ES modules). Run quizzes in your terminal, add your own questions via a JSON file, and extend or package the app as a global CLI tool.

- Language: JavaScript (ES modules)
- Runtime: Node.js (>= 18)
- Intended use: Local CLI quiz sessions and lightweight customization

## Table of Contents

- [Features](#features)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Usage](#usage)
  - [Run via npm](#run-via-npm)
  - [Run via node](#run-via-node)
  - [Install as global binary](#install-as-global-binary)
- [Data format (questions)](#data-format-questions)
  - [Example schema](#example-schema)
  - [Adding questions](#adding-questions)
- [Development](#development)
  - [Run tests](#run-tests)
  - [Run locally & debug tips](#run-locally--debug-tips)
- [Contributing](#contributing)
- [Troubleshooting](#troubleshooting)
- [Suggested next steps](#suggested-next-steps)
- [License](#license)

## Features

- Run interactive multiple-choice quizzes in the terminal.
- JSON-driven question store (easy to edit and extend).
- Lightweight and modular ES module codebase.
- Intended to be packaged as a global CLI tool (optional).
- Basic scoring and feedback after each quiz.

## Prerequisites

- Node.js >= 18.x (ES modules support and stable runtime)
- npm (bundled with Node.js) or yarn

Verify your Node version:

```bash
node --version
# should be v18.x or newer
```

## Installation

Clone the repository and install dependencies:

```bash
git clone <repository-url>
cd <repository-directory>
npm install
```

Optionally, install globally to use the app as a CLI command (example binary name: `cli-quiz`):

```bash
npm install -g .
# or using yarn
# yarn global add .
```

Installing globally makes the command available system-wide (see "Usage" below).

## Usage

There are multiple ways to run the quiz.

Run via npm (recommended for development):

```bash
npm start
```

Run directly with node:

```bash
node index.js
# or, if the entry point is in src/
node ./src/index.js
```

If you installed the package globally (see Installation) and the package `package.json` includes a `bin` field, run:

```bash
cli-quiz
# or the command name you set for the bin
```

Common CLI flags the app may support (if implemented):

- `--help` — show usage/help
- `--shuffle` — randomize question order
- `--limit <n>` — limit to n questions
- `--category <name>` — filter questions by category
- `--difficulty <level>` — filter by difficulty

(Adjust based on available CLI options in your code.)

## Data format (questions)

Questions are stored in a JSON file — typically `data/questions.json`. The app reads this file to present quizzes. Keep a backup before making bulk edits.

### Example schema

Each question object should follow this shape:

```json
[
  {
    "id": "q1",
    "question": "What is the capital of France?",
    "choices": ["Paris", "London", "Berlin", "Rome"],
    "answer": 0,
    "category": "Geography",
    "difficulty": "easy",
    "explanation": "Paris is the capital and largest city of France."
  },
  {
    "id": "q2",
    "question": "Which language runs in a web browser?",
    "choices": ["Java", "C", "Python", "JavaScript"],
    "answer": 3,
    "category": "Programming",
    "difficulty": "easy"
  }
]
```

Field details:

- id (string, optional but recommended): unique identifier.
- question (string, required): the question text.
- choices (array of strings, required): list of possible answers.
- answer (number or string, required): index of the correct choice (0-based) or the text of the correct answer. Prefer index for reliability.
- category (string, optional): group questions by category/topic.
- difficulty (string, optional): e.g. "easy", "medium", "hard".
- explanation (string, optional): extra info shown after answering.

### Adding questions

1. Open `data/questions.json`.
2. Append a new object following the schema above.
3. Save the file.
4. Run the app to verify the new question appears and works.

Tip: Keep IDs unique and validate JSON structure with an online linter or a quick Node script before running.

## Development

Run tests (if any) and linting:

```bash
npm test
# or, if tests not yet present, add them and then run
```

Run the app locally for development:

```bash
npm start
# or
node index.js
```

Debug tips:

- Use `NODE_OPTIONS='--inspect-brk' node index.js` to attach a debugger.
- Add console.log statements or use a debugger (VS Code supports Node debugging).
- If the app uses ESM and you get "Cannot use import statement outside a module", ensure `"type": "module"` is set in package.json.
- Validate JSON with `node -e "console.log(require('./data/questions.json'))"` (CommonJS) or `node -e "import q from './data/questions.json' assert { type: 'json' }; console.log(q)"` depending on environment.

## Contributing

Thanks for thinking about contributing! Suggested workflow:

1. Fork the repository.
2. Create a feature branch: `git checkout -b feat/my-feature`.
3. Make changes and add tests where appropriate.
4. Run tests: `npm test`.
5. Commit and push: `git push origin feat/my-feature`.
6. Open a pull request describing changes and rationale.

Guidelines:

- Keep functions small and focused.
- Add or update tests for new behavior.
- Follow existing coding style and use ES modules.
- Update README if you add new CLI flags or change data format.

## Troubleshooting

- "Unexpected token" or JSON parse errors:
  - Ensure `data/questions.json` is valid JSON (no trailing commas).
- "Cannot find module" or import errors:
  - Make sure `type: "module"` is in package.json for ESM usage, and paths are correct.
- CLI not available after global install:
  - Ensure `package.json` includes a `bin` field mapping a command name to your entry file, e.g.:
    {
      "bin": { "cli-quiz": "./index.js" }
    }
  - Reinstall globally after updating package.json: `npm install -g .`
- Permission errors on global install:
  - Use `npm prefix -g` to check global prefix. Consider using a Node version manager (nvm) or configure npm global directory rather than sudo.

If you encounter other issues, check Node version, file paths, and JSON formatting first.

## Suggested next steps

Ideas to improve the project:

- Add a `bin` field to package.json so users can install and run the CLI globally.
- Add a test suite (Jest, Tap, or Mocha) and CI (GitHub Actions) to run tests on push/PR.
- Add more CLI options and robust argument parsing (yargs, commander).
- Add persistence for user scores or a high-score table.
- Add question import/export tooling (CSV <-> JSON).
- Add automatic JSON schema validation for question files.

Example of bin entry to add to package.json:

```json
"bin": {
  "cli-quiz": "./index.js"
},
"type": "module"
```

## License

MIT License — see the LICENSE file for details. (Replace this placeholder with your chosen license text.)
