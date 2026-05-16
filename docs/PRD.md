# Numerology Vibe App MVP PRD

## Product Goal

Numerology Vibe App is a small educational web application for practicing a complete Vibe Coding workflow with Codex, Agents, Skills, testing, and deployment.

The product allows a user to enter a name, birth date, and selected numerology method, then receive a deterministic numerology-style result with a method explanation and interpretation.

The app must clearly present numerology as entertainment and self-reflection content only. It must not present numerology as scientific fact or advice.

## Target Users

- Learners practicing AI-assisted web development with Next.js, TypeScript, testing, Codex, Agents, and Skills.
- Instructors, mentors, or content creators demonstrating a small but realistic product lifecycle.
- Curious users who want a lightweight numerology result for entertainment and self-reflection.

## MVP Scope

- A mobile-first web form with accessible labels for:
  - name;
  - birth date;
  - numerology method selected from a list.
- Client-side validation with clear error states.
- A deterministic result for the selected method.
- A result view that includes:
  - calculated number or values;
  - selected method name;
  - explanation of the selected method;
  - text interpretation for the selected method;
  - entertainment and self-reflection disclaimer.
- Three initial numerology methods:
  - Life Path Number;
  - Birthday Number;
  - Expression / Destiny Number.
- Pure, testable numerology algorithms outside React components.
- No registration, authentication, backend, database, or personal data storage.
- Unit tests for all numerology methods.
- E2E tests for the main user flows.

## Non-Goals

- User registration.
- User authentication.
- User profiles or saved history.
- Backend APIs or server-side storage.
- Database integration.
- Storing names, birth dates, or generated results.
- Sending personal data to third-party services.
- Presenting numerology as scientific, psychological, medical, financial, legal, or life advice.
- Payments, subscriptions, analytics, social sharing, or personalization.
- Supporting every numerology system in the MVP.

## User Stories

- As a learner, I want a small realistic project so I can practice product planning, implementation, testing, and review with Codex.
- As a user, I want to enter my name, birth date, and numerology method so I can receive a result based on my selected method.
- As a user, I want the method to be selected from a list so I can understand which calculation is being used.
- As a user, I want each method to show its own explanation and interpretation so the result feels specific to the method I chose.
- As a user, I want clear validation messages so I can fix missing or invalid inputs.
- As a privacy-conscious user, I want the app to avoid registration, login, and data storage.
- As a user, I want to see a disclaimer so I understand the result is only for entertainment and self-reflection.

## Acceptance Criteria

- The app does not require registration or login.
- The app does not store personal data in a backend, database, local storage, session storage, or cookies.
- The form requires name, birth date, and numerology method before calculating a result.
- The numerology method is selected from a predefined list.
- Submitting a valid form shows a deterministic result for the selected method.
- Repeating the same input with the same method produces the same result.
- Each MVP method has its own calculation algorithm.
- Each MVP method has its own method explanation and text interpretation.
- Validation errors are shown for missing or invalid required fields.
- The UI is mobile-first and keyboard navigable.
- All form controls have accessible labels.
- The result view always includes the entertainment and self-reflection disclaimer.
- Numerology is not described as scientific fact or authoritative advice.

## Edge Cases

- Empty name.
- Name containing leading, trailing, or repeated spaces.
- Name containing punctuation, hyphens, apostrophes, or mixed casing.
- Name containing unsupported characters.
- Empty birth date.
- Invalid birth date.
- Future birth date.
- Very old birth date.
- Leap day birth date.
- Missing method selection.
- Switching methods after a result has already been calculated.
- Re-submitting the same input.
- Long names that may affect layout on mobile.
- Browser refresh after entering personal data.

## Privacy Notes

- All MVP calculations should happen locally in the browser.
- The app must not introduce a backend unless explicitly requested later.
- The app must not store names, birth dates, selected methods, or generated results.
- The app must not use analytics unless a later requirement explicitly documents what is collected and why.
- Personal data entered into the form should exist only in current client-side UI state needed for the active calculation.

## Disclaimer Requirements

The disclaimer must be visible in the result experience and easy to find from the main app flow.

The disclaimer must communicate that:

- results are intended only for entertainment and self-reflection;
- numerology is not a scientific method;
- results should not be used as medical, psychological, financial, legal, or life advice.

Suggested wording:

```txt
This result is intended for entertainment and self-reflection only.
Numerology is not a scientific method and should not be used as medical,
psychological, financial, legal, or life advice.
```

## First 3 Numerology Methods

### Life Path Number

- Required input: birth date.
- Calculation: use all digits from the birth date and reduce the sum to the method's final numerology number.
- Interpretation: describe broad life themes for the calculated number in entertainment and self-reflection language.

### Birthday Number

- Required input: birth date.
- Calculation: use the day of birth as the main value and reduce it according to the method rules.
- Interpretation: describe strengths, tendencies, or reflective prompts connected to the birthday number.

### Expression / Destiny Number

- Required input: name.
- Calculation: map letters in the name to numeric values, sum them, and reduce the total according to the method rules.
- Interpretation: describe expressive style, strengths, and reflective prompts connected to the calculated number.

## Testing Requirements

Tests must verify:

- shared number reduction behavior;
- birth date digit extraction and parsing;
- Life Path Number calculation;
- Birthday Number calculation;
- Expression / Destiny Number calculation;
- name normalization and supported letter mapping;
- validation for required name, birth date, and method fields;
- validation for invalid dates and future dates;
- method selection behavior;
- successful calculation flow;
- invalid form flow;
- method switching flow;
- deterministic output for repeated inputs;
- disclaimer visibility in the result experience;
- absence of personal data persistence in local storage, session storage, cookies, or backend calls.
