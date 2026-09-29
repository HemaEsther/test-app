# Quiz CLI

An interactive Node.js command-line quiz game for learning JavaScript and related programming fundamentals.

Users select a category and question count, answer multiple-choice questions, receive immediate feedback and explanations, track their progress, review incorrect answers, view their final score, and optionally play again.

## Features

- Interactive terminal-based menus
- Dynamically discovered quiz categories
- Multiple-choice questions with immediate feedback
- Explanations for answers
- Question-count selection:
  - All available questions
  - 3 questions
  - 5 questions
- Fisher–Yates shuffling for each quiz
- Progress bar with percentage display
- Final score and performance summary
- Review of incorrect answers
- Option to play another quiz
- ANSI terminal styling without third-party packages
- Error handling with a process exit status of `1`

## Technology Stack

- JavaScript
- Node.js `>=18.0.0`
- ECMAScript modules
- Terminal CLI
- Node.js built-in modules:
  - `node:readline`
  - `node:fs/promises`
  - `node:url`
  - `node:path`

The project has no third-party dependencies, database, network service, build step, or environment variables.

## Prerequisites

Install Node.js version `18.0.0` or later.

Verify your Node.js version:

```bash
node --version
```

## Installation

Clone the repository and enter the project directory:

```bash
git clone https://github.com/HemaEsther/test-app.git
cd test-app
```

No dependency installation is required because the project uses only Node.js built-in modules.

## Running the Application

Start the quiz with npm:

```bash
npm start
```

The `start` script runs:

```bash
node index.js
```

You can also run the entry point directly:

```bash
node index.js
```

Follow the interactive prompts to:

1. Select a category.
2. Select the number of questions.
3. Answer each multiple-choice question.
4. Review immediate feedback and explanations.
5. View your progress and final score.
6. Review incorrect answers.
7. Choose whether to play again.

## Available Categories

The current question data includes:

- JavaScript Basics
- Node.js Fundamentals
- General Programming

Categories are loaded from `data/questions.json` and discovered dynamically, so the quiz menu is based on the categories present in the data file.

## Scoring

The final score is presented as a percentage with the following performance messages:

| Score | Message |
| --- | --- |
| 100% | Perfect score |
| 80–99% | Great job |
| 60–79% | Good effort |
| 40–59% | Not bad |
| Below 40% | Keep practicing |

The quiz displays a 30-character progress bar and the current completion percentage while questions are being answered.

## Question Data

Quiz content is stored in:

```text
data/questions.json
```

The file contains a top-level categories object. Each category includes a display name and a list of questions. Each question contains:

- `question` — The question text
- `options` — The available multiple-choice answers
- `answer` — The zero-based index of the correct option
- `explanation` — The explanation shown after answering

A question has the following general shape:

```json
{
  "question": "Question text",
  "options": [
    "First option",
    "Second option",
    "Third option"
  ],
  "answer": 1,
  "explanation": "Explanation of the correct answer."
}
```

The `answer` value is zero-based. For example, `0` identifies the first option and `1` identifies the second option.

### Customizing Questions

To customize the quiz, edit `data/questions.json` while preserving its existing category and question structure.

The current content covers topics including:

- JavaScript declarations, arrays, equality, types, and `typeof null`
- Node.js filesystem APIs, the event loop, npm initialization, `process.argv`, and ES imports
- APIs, recursion, JSON, callbacks, and version control

Questions selected for a quiz are shuffled without mutating the original category question array.

## Project Structure

```text
.
├── data/
│   └── questions.json
├── src/
│   ├── colors.js
│   ├── input.js
│   └── quiz.js
├── index.js
└── package.json
```

### Important Files

#### `index.js`

Application entry point. It handles:

- Loading the question data
- Displaying the category and question-count menus
- Starting quizzes
- Managing the play-again loop
- Handling application errors
- Closing the readline interface during cleanup

#### `src/input.js`

Provides readline-based input helpers, including:

- Creating the readline interface
- Prompting for input
- Selecting menu options
- Confirming choices
- Waiting for the user to press Enter

#### `src/quiz.js`

Contains the main `Quiz` class and quiz behavior, including:

- Question selection and shuffling
- Answer evaluation
- Score calculation
- Progress display
- Answer feedback
- Final results
- Incorrect-answer review

#### `src/colors.js`

Contains local ANSI color and style helpers used to format terminal output.

#### `data/questions.json`

Contains the categories, questions, answer indexes, options, and explanations used by the quiz.

#### `package.json`

Defines the project metadata, ECMAScript module configuration, and npm scripts.

## Technical Details

### ECMAScript Modules

The project uses ECMAScript modules through the `type` configuration in `package.json`. Source files use the modern module system rather than CommonJS.

### Asynchronous File Loading

Question data is loaded asynchronously from `data/questions.json` using Node.js filesystem APIs and parsed as JSON before the quiz begins.

### Question Shuffling

Questions are selected and shuffled using the Fisher–Yates algorithm. The original question data is not mutated during shuffling.

### Input and Cleanup

Interactive input is handled with Node.js `readline`. The readline interface is closed in a `finally` block so that resources are cleaned up even when an error occurs.

### Error Handling

Application errors are formatted before being displayed, and the process exits with status `1` when an unrecoverable error occurs.

## Testing

The project defines the following test script:

```bash
npm test
```

This runs:

```bash
node --test
```

There are currently no test files in the repository.

## Configuration

No environment variables or additional configuration files are required.

The project also has:

- No command-line argument parsing
- No score persistence
- No database
- No network service
- No web or graphical user interface
- No build step

## License

The project declares the MIT license in `package.json`.

There is no separate `LICENSE` file in the repository.
