# AGENTS.md

## Project goal

Build a small educational numerology web application using Next.js, TypeScript, Tailwind, shadcn/ui, and strong testing practices.

## Product constraints

- No registration.
- No authentication.
- Required inputs: name, birth date, numerology method.
- Results are deterministic.
- Do not present numerology as scientific fact.
- Always include an entertainment/self-reflection disclaimer.

## Engineering constraints

- TypeScript strict mode.
- Keep numerology algorithms pure and testable.
- No business logic inside React components.
- Add unit tests for every method.
- Add e2e tests for main user flows.
- Prefer small, focused components.
- Do not introduce backend unless explicitly requested.
- Do not store personal data.

## UI constraints

- Mobile-first.
- Accessible form labels.
- Keyboard navigation.
- Clear error states.
- Calm, trustworthy visual style.
- Avoid mystical clutter.

## Review checklist

Before finishing any coding task:
- Run typecheck.
- Run unit tests.
- Run lint.
- Explain changed files.
- Mention remaining risks.