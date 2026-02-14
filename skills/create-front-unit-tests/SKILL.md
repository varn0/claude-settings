---
name: create-front-unit-tests
description: Set up comprehensive testing for a React component.
user-invocable: true
argument-hint: [component name or path]
---

Create a complete test suite for the component: $ARGUMENTS

Include:
1. **Rendering tests** — verify the component renders correctly with various props and states (default, loading, error, empty, populated)
2. **User interaction tests** — test clicks, form inputs, keyboard events, and callbacks
3. **Error state and edge case tests** — empty strings, null values, boundary numbers, very long text, missing optional props
4. **Accessibility tests** — ARIA attributes, keyboard navigation, focus management, screen reader compatibility
5. **Visual regression tests** — use Playwright if available for screenshot comparisons

Before writing tests, read the component source and existing test files to match the project's testing conventions (test framework, assertion style, mocking patterns, file structure).
