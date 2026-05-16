# Numerology Vibe App Architecture

## Overview

Numerology Vibe App is a standalone Next.js web application for deterministic, educational numerology-style calculations. The MVP uses TypeScript, the Next.js App Router, Tailwind CSS, and small focused React components.

All numerology calculations happen locally in the browser. The MVP has no backend, no database, no registration, no authentication, and no personal data storage. User-provided name and birth date are used only in current UI state for the active calculation.

Numerology must be presented as entertainment and self-reflection content, not as science, advice, or authoritative guidance.

## Project Structure

Target directory structure:

```txt
src/
  app/
    page.tsx
    layout.tsx

  components/
    NumerologyForm.tsx
    MethodSelector.tsx
    ResultCard.tsx
    Disclaimer.tsx
    ValidationMessage.tsx

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

skills/
```

Responsibilities:

- `src/app`: App Router entry points, page composition, metadata, and global layout.
- `src/components`: Presentational and interaction components with no numerology business logic.
- `src/domain/numerology`: Pure domain types, method registry, algorithms, and shared calculation utilities.
- `src/domain/numerology/methods`: One file per numerology method.
- `src/domain/numerology/utils`: Shared pure helpers such as number reduction, date digit extraction, and alphabet maps.
- `src/content/interpretations`: Static interpretation content keyed by method and result number.
- `src/lib`: Application-level helpers such as validation and formatting.
- `tests/unit`: Unit and component tests for algorithms, validation, and UI behavior.
- `tests/e2e`: Playwright tests for main user flows.
- `skills`: Project workflow instructions for repeatable Codex-assisted work.

## Domain Model

Core TypeScript types should live in `src/domain/numerology/types.ts`.

```ts
export type NumerologyMethodId =
  | "life-path"
  | "birthday-number"
  | "expression-number";

export interface NumerologyInput {
  name: string;
  birthDate: string;
  methodId: NumerologyMethodId;
}

export interface NumerologyResult {
  methodId: NumerologyMethodId;
  title: string;
  value: number;
  summary: string;
  strengths: string[];
  challenges: string[];
  explanation: string;
  disclaimer: string;
}

export interface NumerologyMethod {
  id: NumerologyMethodId;
  title: string;
  description: string;
  requiredFields: Array<"name" | "birthDate">;
  calculate(input: NumerologyInput): NumerologyResult;
}

export interface InterpretationContent {
  methodId: NumerologyMethodId;
  values: Record<
    string,
    {
      summary: string;
      strengths: string[];
      challenges: string[];
      reflectionPrompts?: string[];
    }
  >;
}
```

`NumerologyMethodId` should be a closed union for MVP methods. When a new method is added, the union, registry, content, and tests should be updated together.

## Numerology Method Architecture

Each numerology method follows the same pattern:

1. Add a dedicated file in `src/domain/numerology/methods/`.
2. Implement a pure calculation function that accepts typed input and returns typed output.
3. Avoid React, browser APIs, storage APIs, network calls, randomness, and time-dependent behavior inside calculation logic.
4. Register the method in `src/domain/numerology/registry.ts`.
5. Add interpretation content in `src/content/interpretations/`.
6. Add unit tests for the algorithm and relevant edge cases.
7. Add or update e2e coverage when the new method changes the main user flow.

The registry is the only place the UI should use to discover available methods. React components should call domain functions through this registry instead of importing individual method files directly.

## MVP Methods

### Life Path Number

- Required input: birth date.
- Calculation: extract all digits from the birth date, sum them, and reduce the total to the final numerology number according to the method rules.
- Interpretation: broad life themes and reflective prompts for the calculated number.

### Birthday Number

- Required input: birth date.
- Calculation: use the day of birth as the main value and reduce it according to the method rules.
- Interpretation: strengths, tendencies, and self-reflection prompts connected to the birthday number.

### Expression / Destiny Number

- Required input: name.
- Calculation: normalize the name, map supported letters to numeric values, sum them, and reduce the total according to the method rules.
- Interpretation: expressive style, strengths, challenges, and reflective prompts connected to the calculated number.
- Validation must reject or clearly report unsupported alphabets or characters when the method cannot calculate them reliably.

## Data And Privacy

The MVP is local-only:

- Names and birth dates are not saved.
- Results are not saved.
- Form data is not written to local storage, session storage, cookies, a database, or a backend.
- Data is not sent to backend APIs or third-party services.
- Calculations happen in the browser.
- Analytics are out of scope for MVP.

Personal data should exist only in transient React state needed for the current interaction.

## UI Architecture

UI components should be small, mobile-first, accessible, and visually calm. Components must not contain numerology algorithms.

- `NumerologyForm`: Owns form state, submit handling, validation display, and result triggering.
- `MethodSelector`: Renders supported methods from the registry and lets the user choose one.
- `ResultCard`: Displays calculated value, method title, explanation, interpretation, strengths, challenges, and disclaimer.
- `Disclaimer`: Provides the required entertainment and self-reflection disclaimer in the main result flow.
- `ValidationMessage`: Renders accessible validation feedback associated with form fields.

Form controls must have accessible labels, visible focus states, keyboard navigation, and clear error states.

## Validation Strategy

Validation should be centralized outside React components, for example in `src/lib/validation.ts`, and covered by unit tests.

Rules:

- Name is required.
- Birth date is required.
- Birth date must be a valid date.
- Future birth dates are invalid.
- Method id is required.
- Method id must be one of the supported registry method ids.
- Method-specific validation can add stricter rules, such as unsupported alphabet handling for Expression / Destiny Number.

Validation should return structured errors that UI components can render next to the relevant field.

## Testing Strategy

The MVP should include:

- Unit tests for shared utilities such as number reduction, date digit extraction, name normalization, and alphabet mapping.
- Unit tests for each numerology algorithm.
- Unit tests for validation rules and method-specific validation.
- Component tests for form rendering, validation messages, method selection, result rendering, and disclaimer visibility.
- E2E tests for the successful calculation flow, invalid form flow, and method switching flow.

Tests should verify deterministic behavior: the same input and same method must produce the same result.

Privacy-sensitive tests should verify that personal data is not persisted to local storage, session storage, cookies, or backend calls.

## Deployment Strategy

The MVP should use a simple Next.js deployment target, such as Vercel or Cloudflare Pages.

Deployment should run CI checks before publishing:

```bash
pnpm lint
pnpm typecheck
pnpm test
pnpm build
```

E2E tests should run in CI when practical, especially before releases or when user flows change.

## Non-Goals

The MVP does not include:

- Backend APIs.
- Database integration.
- User accounts.
- Registration.
- Authentication.
- Payments or subscriptions.
- AI-generated runtime interpretations.
- Stored calculation history.
- Analytics.
- Personalization.
- Social sharing.

## Architecture Decisions

### ADR-001: No Backend For MVP

The MVP does not need server-side calculation, persistence, accounts, or external integrations. Keeping calculations local reduces privacy risk, deployment complexity, and implementation scope.

### ADR-002: Domain Logic Is Separated From React

Numerology algorithms live in `src/domain/numerology` instead of React components. This keeps calculations pure, deterministic, easy to test, and reusable from any UI surface.

### ADR-003: Interpretations Are Content Files

Interpretation text lives in `src/content/interpretations` so content can evolve independently from algorithm code. This keeps method files focused on calculation behavior and makes future review, editing, and localization easier.

### ADR-004: Deterministic Algorithms Are Preferred For MVP

The MVP uses deterministic algorithms because results must be repeatable, testable, and explainable. Runtime AI-generated interpretations, randomness, or external service calls are excluded from MVP scope.
