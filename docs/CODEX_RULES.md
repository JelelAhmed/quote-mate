# Plumber Quote App — Codex Rules

## 1. Authoritative Specification

Before implementing any milestone:

1. Read `PRODUCT.md`.
2. Read `BUILD_PLAN.md`.
3. Identify the currently assigned milestone.
4. Implement only that milestone.

`PRODUCT.md` is authoritative for product behaviour and scope.

`BUILD_PLAN.md` is authoritative for implementation sequence.

Do not silently reinterpret either file.

---

## 2. Scope Discipline

The V1 exists to support:

`Create Quote → Generate PDF → Send or Print`

Do not add adjacent business-management features merely because they appear useful.

In particular, do not add:

- inventory
- accounting
- payment processing
- payment tracking
- receipts
- CRM
- job scheduling
- customer accounts
- authentication
- cloud sync
- team accounts
- dashboards
- analytics
- subscriptions
- direct WhatsApp integration

unless the product specification is explicitly updated first.

---

## 3. Milestone Discipline

Implement one milestone at a time.

Do not start future milestones early.

When a milestone is complete, stop and report.

The completion report must include:

- summary of implementation
- files created
- files changed
- tests/checks run
- results of those checks
- known limitations
- unresolved issues
- any assumptions made
- any required deviation from the specification

---

## 4. Do Not Redesign Product Behaviour

Do not change:

- workflow
- required fields
- document semantics
- storage strategy
- quote calculations
- navigation model
- feature boundaries

unless there is a genuine implementation blocker or contradiction.

If one exists:

1. explain the conflict,
2. propose the smallest possible resolution,
3. stop before making a product-level change unless explicitly directed.

---

## 5. Mobile-First Requirement

The primary device is an iPhone.

Every screen must be designed and reviewed first at a narrow mobile viewport.

Do not create a desktop-oriented interface and merely make it responsive afterward.

Prefer:

- large touch targets
- single-column forms
- simple actions
- clear hierarchy
- minimal typing
- appropriate input modes
- one-handed usability

---

## 6. Engineering Quality

Prefer straightforward, maintainable code over abstraction-heavy architecture.

Requirements:

- TypeScript throughout application code
- domain calculations separated from UI
- storage logic separated from UI
- reusable components where repetition is real
- avoid premature generalized frameworks
- avoid unnecessary dependencies
- no hidden global mutable state
- deterministic quote calculations

---

## 7. Quote Calculations

All monetary calculations must use shared domain utilities.

Do not implement arithmetic independently inside several components.

At minimum define shared logic for:

- item amount
- subtotal
- additional charges
- discount
- grand total
- Naira formatting

Handle invalid, empty, and negative inputs intentionally.

Do not allow UI parsing quirks to silently produce `NaN` totals.

---

## 8. Persistence

V1 is local-first.

Use IndexedDB or a lightweight IndexedDB abstraction.

Do not introduce:

- Supabase
- Firebase
- custom APIs
- server databases
- authentication

for V1.

Keep the storage layer replaceable so cloud persistence can be introduced later if validated.

---

## 9. PDF Is a Primary Feature

Treat PDF generation as a core product capability, not an afterthought.

The resulting PDF must:

- be professional
- print cleanly on A4
- work as a WhatsApp attachment
- support multiple pages
- preserve totals accurately
- avoid clipping long content
- exclude application controls

The PDF should remain readable when printed in grayscale.

---

## 10. Browser and PWA Constraints

Primary target:

- Safari on iPhone
- installed PWA on iPhone Home Screen

Secondary targets:

- current desktop browsers
- current Android browsers

Do not assume APIs available only in Chromium.

When using browser APIs for sharing, printing, storage, or files:

- check compatibility
- provide graceful fallback behaviour where practical

---

## 11. Testing

Add automated tests where they protect meaningful product behaviour.

Prioritise:

- quote calculations
- quote numbering
- duplicate quote behaviour
- data transformations
- domain validation

Do not create shallow tests solely to increase test count.

Every milestone should run the relevant available checks, including where applicable:

- tests
- lint
- type checking
- production build

Report actual results.

---

## 12. Dependencies

Before adding a dependency, confirm that it solves a real requirement in the current milestone.

Prefer:

- established libraries
- small dependency surface
- browser support compatible with iPhone Safari

Avoid installing packages speculatively for future work.

---

## 13. UI Design Direction

The application should feel:

- simple
- modern
- trustworthy
- practical
- professional

Avoid:

- over-designed dashboards
- excessive cards
- gradients everywhere
- ornamental animations
- tiny controls
- accounting-software density

The quotation document itself should be especially restrained and print-friendly.

---

## 14. Data Preservation

Do not make schema changes casually once local persistence exists.

If a persisted model must change:

- identify the compatibility issue
- provide an intentional migration strategy where necessary
- do not silently discard existing saved quotes

---

## 15. Pending Real-World Validation

The current specification is provisional because a real handwritten quotation sample has not yet been reviewed.

Do not invent complexity to compensate for missing real-world evidence.

When the sample becomes available, product changes should be made in `PRODUCT.md` first and then reflected in the build plan if necessary.

---

## 16. Definition of Done

A milestone is not complete merely because the UI renders.

It is complete only when:

- its required behaviour works
- relevant edge cases are handled
- applicable checks pass
- no unrelated scope was added
- the implementation has been reported clearly

Stop after reporting completion.
