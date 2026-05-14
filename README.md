# Numerology Vibe App

Educational web application for practicing AI-assisted software development with Codex, Agents, Skills, Figma, testing, and deployment workflows.

The app calculates numerology-based interpretations from a person's name, birth date, and selected numerology method.

> This project is created for learning purposes. Numerology results are intended for entertainment and self-reflection only. They should not be treated as scientific, psychological, medical, financial, or life advice.

## Project goals

The main goal of this repository is to practice a complete Vibe Coding workflow:

- define product requirements;
- design UI in Figma;
- implement a small but realistic web application;
- use Codex for coding, review, refactoring, and tests;
- use Skills for repeatable workflows;
- keep business logic testable and separated from UI;
- deploy the application as a standalone web app.

## Product overview

The application allows a user to enter:

- name;
- birth date;
- numerology method selected from a list.

The app then calculates a deterministic result and displays:

- calculated number or values;
- strong sides;
- weak sides;
- text interpretation;
- explanation of the selected method;
- disclaimer.

No registration or authentication is required.

## MVP features


- [ ] Name input
- [ ] Birth date input
- [ ] Numerology method selector
- [ ] Life Path Number calculation
- [ ] Birthday Number calculation
- [ ] Expression / Destiny Number calculation
- [ ] Result card with interpretation
- [ ] Validation errors
- [ ] Mobile-first responsive UI
- [ ] Privacy-friendly behavior: no data storage
- [ ] Unit tests for numerology algorithms
- [ ] E2E test for the main calculation flow
- [ ] Deployment-ready build

## Tech stack

Recommended stack:

- Next.js
- React
- TypeScript
- Tailwind CSS
- shadcn/ui
- Vitest
- Testing Library
- Playwright
- pnpm
- GitHub Actions
- Vercel or Cloudflare Pages


## Getting started

### Prerequisites

Install:

- Node.js
- pnpm
- Git
- VS Code
- Codex CLI or Codex IDE extension


### Install dependencies

```bash
pnpm install
````

### Run local development server

```bash
pnpm dev
```

### Run tests

```bash
pnpm test
```

### Run type checking

```bash
pnpm typecheck
```

### Run linting

```bash
pnpm lint
```

### Build production version

```bash
pnpm build
```

## Available scripts

```bash
pnpm dev         # start local development server
pnpm build       # create production build
pnpm start       # start production server
pnpm lint        # run linter
pnpm typecheck   # run TypeScript checks
pnpm test        # run unit tests
pnpm test:e2e    # run Playwright tests
```

## Project structure

```txt
numerology-vibe-app/
  AGENTS.md
  README.md
  package.json

  docs/
    PRD.md
    ARCHITECTURE.md
    DESIGN_BRIEF.md
    DEPLOYMENT.md

  skills/
    product-requirements/
      SKILL.md
    ui-design-review/
      SKILL.md
    frontend-implementation/
      SKILL.md
    numerology-method/
      SKILL.md
    test-engineering/
      SKILL.md
    deployment/
      SKILL.md

  src/
    app/
      page.tsx
      layout.tsx

    components/
      NumerologyForm.tsx
      MethodSelector.tsx
      ResultCard.tsx
      Disclaimer.tsx

    domain/
      numerology/
        types.ts
        registry.ts
        methods/
          lifePath.ts
          birthdayNumber.ts
          expressionNumber.ts
        utils/
          reduceNumber.ts
          dateDigits.ts
          alphabetMaps.ts

    content/
      interpretations/
        life-path.json
        birthday-number.json
        expression-number.json

    lib/
      validation.ts

  tests/
    unit/
    e2e/
```


## Numerology methods

Each numerology method should follow the same interface.

```ts
export interface NumerologyMethod {
  id: string;
  title: string;
  description: string;
  requiredFields: Array<"name" | "birthDate">;
  calculate(input: NumerologyInput): NumerologyResult;
}
```

Current planned methods:

| Method            | Required input | Description                                                   |
| ----------------- | -------------- | ------------------------------------------------------------- |
| Life Path Number  | Birth date     | Calculates a reduced number from all digits of the birth date |
| Birthday Number   | Birth date     | Uses the day of birth as the main number                      |
| Expression Number | Name           | Calculates a number from letters in the person's name         |


## Adding a new numerology method

To add a new method:

1. Create a new file in `src/domain/numerology/methods/`.
2. Implement the `NumerologyMethod` interface.
3. Add pure calculation logic.
4. Add interpretation content in `src/content/interpretations/`.
5. Register the method in `src/domain/numerology/registry.ts`.
6. Add unit tests.
7. Add or update E2E tests if the user flow changes.
8. Update this README if needed.

Example Codex prompt:

```txt
Use the numerology-method skill.

Add a new numerology method called Soul Urge Number.

Constraints:
- keep calculation logic outside React components;
- add unit tests;
- add interpretation content;
- register the method in the method registry;
- update README if needed.
```


## Codex workflow

This repository is designed to be used with Codex.

Recommended workflow:

1. Create or update documentation first.
2. Ask Codex for a small implementation plan.
3. Ask Codex to modify a limited set of files.
4. Review the diff.
5. Run tests.
6. Ask Codex to review its own changes.
7. Commit only after checks pass.

Example prompt:

```txt
Read AGENTS.md and docs/ARCHITECTURE.md.

Implement Life Path Number calculation.

Constraints:
- do not touch UI;
- keep logic pure and testable;
- add unit tests;
- explain changed files after implementation.
```

## Skills

This project uses Skills for repeatable development workflows.

Planned Skills:

| Skill                   | Purpose                                                         |
| ----------------------- | --------------------------------------------------------------- |
| product-requirements    | Create or update PRD and acceptance criteria                    |
| ui-design-review        | Review Figma/UI design, accessibility, layout, visual hierarchy |
| frontend-implementation | Implement React/Next.js UI according to project rules           |
| numerology-method       | Add or modify numerology calculation methods                    |
| test-engineering        | Add unit, component, and E2E tests                              |
| deployment              | Prepare production build, CI, and deployment docs               |


## Figma workflow

Figma is used for UI design and handoff.

Recommended design artifacts:

* mobile frame;
* desktop frame;
* form empty state;
* validation error state;
* successful result state;
* method explanation state;
* design tokens;
* reusable components.

Design tokens should include:

* colors;
* spacing;
* typography;
* border radius;
* shadows;
* form states.


## Testing strategy

The project should include:

### Unit tests

* number reduction;
* date parsing;
* Life Path calculation;
* Birthday Number calculation;
* Expression Number calculation;
* validation logic.

### Component tests

* form rendering;
* validation messages;
* method selector;
* result rendering.

### E2E tests

* successful calculation flow;
* invalid form flow;
* method switching flow.

## Privacy

The application should not:

* require registration;
* require login;
* store user names;
* store birth dates;
* send personal data to a backend;
* use analytics without explicit decision and documentation.

All calculations should happen locally in the browser for the MVP.

## Disclaimer

The application must always display a disclaimer similar to:

```txt
This result is intended for entertainment and self-reflection only.
Numerology is not a scientific method and should not be used as medical,
psychological, financial, legal, or life advice.
```

## Deployment

The app can be deployed to:

* Vercel;
* Cloudflare Pages;
* Netlify.

Before deployment, run:

```bash
pnpm lint
pnpm typecheck
pnpm test
pnpm build
```

## Quality checklist

Before merging a change:

* [ ] TypeScript passes
* [ ] Lint passes
* [ ] Unit tests pass
* [ ] E2E tests pass if user flow changed
* [ ] Business logic is not inside React components
* [ ] No unnecessary dependencies were added
* [ ] No personal data is stored
* [ ] UI is accessible by keyboard
* [ ] Error states are clear
* [ ] Disclaimer is visible
* [ ] README/docs are updated if behavior changed


## Roadmap

### MVP

* Basic web app
* Three numerology methods
* Local-only calculation
* Responsive UI
* Tests
* Deployment

### Later

* More numerology methods
* Cyrillic name support
* Method explanation pages
* Shareable result link without storing personal data
* Print-friendly result page
* Figma MCP integration
* Internal content-generation agent for drafting interpretations
* Optional VS Code extension for editing numerology methods


## License

TBD.


## Windows setup notes

This project was bootstrapped on Windows.

### Recommended filesystem

For Node.js / pnpm / Next.js development on Windows, use an NTFS drive.

Avoid using exFAT drives for this project because pnpm may rely on symlinks or link-like behavior inside `node_modules`, and exFAT can cause installation failures.

Recommended location example:

```powershell
C:\Codex\numerology-vibe-app
````

## Project bootstrap on Windows

The repository already contained:

```txt
README.md
AGENTS.md
```

Because the repository was not empty, the Next.js application was first created in a temporary folder and then copied into the main repository.

### 1. Clone the repository

```powershell
cd C:\Codex
git clone git@github.com:<your-github-username>/numerology-vibe-app.git
cd numerology-vibe-app
```

### 2. Create a working branch

```powershell
git checkout -b chore/bootstrap-next-app
```

### 3. Create a temporary Next.js app

From `C:\Codex`:

```powershell
cd C:\Codex

pnpm create next-app@latest numerology-vibe-app-tmp `
  --typescript `
  --eslint `
  --app `
  --src-dir `
  --tailwind `
  --import-alias "@/*" `
  --use-pnpm
```

If pnpm reports ignored build scripts for packages such as `sharp` or `unrs-resolver`, go into the temporary project and approve only those builds:

```powershell
cd C:\Codex\numerology-vibe-app-tmp

pnpm approve-builds sharp unrs-resolver
pnpm install
```

### 4. Verify the temporary app

```powershell
pnpm dev
```

Open:

```txt
http://localhost:3000
```

Stop the dev server with `Ctrl+C`.

### 5. Copy the generated app into the main repository

```powershell
cd C:\Codex

robocopy .\numerology-vibe-app-tmp .\numerology-vibe-app /E /XD .git node_modules .next /XF README.md AGENTS.md
```

`robocopy` may return exit code `1`. This is usually fine and means that files were copied.

### 6. Remove the temporary app

```powershell
Remove-Item .\numerology-vibe-app-tmp -Recurse -Force
```

### 7. Install dependencies in the main repository

```powershell
cd C:\Codex\numerology-vibe-app

pnpm install
```

If pnpm again reports ignored build scripts:

```powershell
pnpm approve-builds sharp unrs-resolver
pnpm install
```

### 8. Add the typecheck script

If `pnpm typecheck` fails with:

```txt
Command "typecheck" not found
```

add the script to `package.json`:

```powershell
npm pkg set scripts.typecheck="tsc --noEmit"
```

Then run:

```powershell
pnpm typecheck
```

## Local validation

Before committing, run:

```powershell
pnpm dev
pnpm build
pnpm typecheck
```

Optional, if the lint script exists:

```powershell
pnpm lint
```

## Commit bootstrap

```powershell
git status
git add .
git commit -m "chore: bootstrap Next.js application"
git push -u origin chore/bootstrap-next-app
```

