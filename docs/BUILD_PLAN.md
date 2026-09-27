# Plumber Quote App — Build Plan

## Purpose

This file converts the V1 product specification into small, reviewable Codex milestones.

Codex should implement only one milestone at a time and stop after completing and reporting that milestone.

`PRODUCT.md` is authoritative for product behaviour and scope.

---

# Milestone 0 — Project Setup

## Goal

Create the application foundation without implementing product features.

## Work

- Create a Next.js application with TypeScript.
- Configure Tailwind CSS.
- Configure linting and formatting.
- Add PWA support suitable for iPhone Home Screen installation.
- Create the initial application shell.
- Establish a clean source-folder structure.
- Add basic responsive viewport configuration.
- Add placeholder routes/pages for:
  - Home
  - Quote Editor
  - Quote Preview
  - Settings
- Confirm the project runs successfully in development.
- Confirm a production build succeeds.

## Do Not Implement Yet

- quote persistence
- quote calculations
- PDF generation
- full UI styling
- business logic

## Acceptance Criteria

- app starts successfully
- production build succeeds
- routes exist
- layout works on narrow mobile viewport
- PWA manifest/configuration exists
- no product scope beyond setup has been added

---

# Milestone 1 — Domain Model and Storage

## Goal

Create a stable quote data model and local persistence layer.

## Work

Define TypeScript types/interfaces for:

### Business Profile

- business name
- owner/contact name
- phone
- email
- address
- logo reference
- default quote notes

### Client

- name
- phone
- address/job location
- project description

### Quote Item

- id
- description
- quantity
- unit
- unit price
- calculated amount

### Quote

- id
- quote number
- quote date
- valid-until date
- client details
- items
- transport/delivery charge
- other charge
- discount
- notes
- subtotal
- grand total
- created-at timestamp
- updated-at timestamp

Implement:

- quote calculation helpers
- currency formatting helpers
- quote-number generation
- IndexedDB persistence
- create quote
- read quote
- update quote
- delete quote
- list quotes
- duplicate quote
- save/load business profile

Use a lightweight abstraction over IndexedDB if useful.

## Requirements

- calculations must not be duplicated across UI components
- persisted objects should be versionable/migratable later
- storage code must be isolated from presentation components

## Acceptance Criteria

- quotes can be saved and loaded locally
- quote totals calculate correctly
- duplicate creates a new ID and quote number
- business profile persists
- automated tests cover calculation helpers and quote duplication

---

# Milestone 2 — Home Screen

## Goal

Provide fast access to new and existing quotations.

## Work

Implement the Home screen with:

- app/business identity
- prominent `New Quote` button
- recent/saved quotation list
- client name
- quote number
- date
- total
- open action
- duplicate action
- delete action
- appropriate empty state

## Behaviour

`New Quote` creates a new unsaved/draft quotation and opens the Quote Editor.

Deleting a quote must require confirmation.

Duplicating a quote:

- copies its editable content
- generates a new ID
- generates a new quote number
- resets created/updated timestamps appropriately

## Acceptance Criteria

- saved quotes appear after reload
- new quote flow works
- open works
- duplicate works
- delete works
- empty state is clear
- screen is usable on iPhone-width viewport

---

# Milestone 3 — Quote Editor

## Goal

Allow the plumber to create and edit a complete quotation from one mobile-friendly screen.

## Sections

### Client Details

- Client name
- Phone
- Address / job location
- Project description

### Quote Details

- Quote number
- Quote date
- Valid until

### Items

Each line item must support:

- description
- quantity
- unit
- unit price
- calculated amount
- remove item

Add-item action must be obvious.

Suggested unit choices:

- Pcs
- Length
- Roll
- Set
- Bag
- Metre
- Hour
- Job
- Other

Support custom units.

### Additional Amounts

- Transport/delivery
- Other charge
- Discount

### Notes

- quote notes / terms

### Totals

Display:

- subtotal
- additional charges
- discount
- grand total

## UX Requirements

- use appropriate mobile keyboard/input modes
- quantity defaults to `1`
- calculations update immediately
- totals remain easy to find
- touch targets are comfortably sized
- avoid modal-heavy editing
- do not split the editor into a long wizard unless usability testing later proves necessary

## Actions

- Save
- Preview

## Acceptance Criteria

- quote can be created entirely from iPhone-width layout
- line items can be added and removed
- invalid values do not corrupt totals
- calculations update correctly
- saved data survives reload
- editing an existing quote updates rather than duplicates it

---

# Milestone 4 — Business Settings

## Goal

Allow the plumber to configure business information once and reuse it automatically.

## Fields

- Business name
- Owner/contact name
- Phone
- Email
- Address
- Logo
- Default quotation notes

## Behaviour

- settings persist locally
- new quotations use default notes when appropriate
- business information appears in quote preview
- logo upload should use a browser-compatible local representation suitable for later PDF rendering

## Acceptance Criteria

- profile survives reload
- profile changes appear in preview
- logo can be added, replaced, and removed
- no login/backend is introduced

---

# Milestone 5 — Quote Preview

## Goal

Show a faithful document preview before export.

## Work

Create a clean quotation document view containing:

1. Business identity
2. `QUOTATION` heading
3. Quote number
4. Quote date
5. Valid-until date if present
6. Client details
7. Project description if present
8. Itemised table
9. Subtotal
10. Additional charges
11. Discount
12. Grand total
13. Notes/terms
14. Business contact footer

## Design Requirements

- white document background
- dark readable typography
- restrained accent colour
- A4-oriented composition
- strong total emphasis
- printer-friendly
- no dark-mode dependency
- no gradients or decorative effects that reduce print quality

## Actions

- Edit Quote
- Generate PDF

## Acceptance Criteria

- preview contains all quote information
- optional empty fields do not leave awkward gaps
- long descriptions wrap correctly
- preview remains readable on phone
- document structure translates naturally to A4

---

# Milestone 6 — PDF Generation

## Goal

Generate a professional PDF matching the preview closely.

## Work

- select a browser-compatible PDF-generation approach
- render quotations to A4
- support multiple pages when items overflow
- keep headers/tables/totals readable across page breaks
- preserve the business logo
- use Nigerian Naira formatting
- create a sensible file name

Example:

`QT-0007-John-Adeyemi.pdf`

## Requirements

The PDF must work for:

- WhatsApp attachment
- email attachment
- local saving
- A4 printing

## Acceptance Criteria

- PDF generates on primary target browser
- PDF opens correctly
- PDF prints correctly on A4
- long quotations do not clip content
- totals remain correct
- no screen-only UI controls appear in PDF

---

# Milestone 7 — Share, Save and Print

## Goal

Complete the output workflow.

## Work

Provide:

- Share
- Save PDF
- Print

Use native/browser share capabilities where supported.

On iPhone, the share action should allow the user to pass the generated document into the system share sheet, from which WhatsApp can be selected when installed.

Do not implement direct WhatsApp API integration.

## Fallbacks

Where native file sharing is unavailable:

- provide PDF download/save
- provide print support

## Acceptance Criteria

- generated quote can be shared from supported mobile browsers
- generated quote can be saved
- generated quote can be printed
- workflow remains understandable when native share is unsupported

---

# Milestone 8 — PWA and iPhone Validation

## Goal

Make the product comfortable to use as an installed mobile web app.

## Work

Validate:

- Safari
- iPhone-sized viewport
- Add to Home Screen behaviour
- standalone display
- PWA icons
- app metadata
- safe-area handling
- input focus/keyboard behaviour
- form scrolling
- file/logo handling
- IndexedDB persistence
- PDF generation
- share sheet behaviour
- print workflow

## Acceptance Criteria

- app can be added to iPhone Home Screen
- installed app launches correctly
- no UI is hidden behind notches/home indicator
- forms remain usable with keyboard open
- quote data survives closing/reopening the app
- primary quote-to-PDF workflow succeeds

---

# Milestone 9 — V1 Polish and Regression Review

## Goal

Prepare the app for real use by the plumber.

## Work

Review the entire core workflow:

`Create Quote → Save → Preview → Generate PDF → Share/Print`

Polish:

- empty states
- loading states
- confirmation states
- deletion confirmation
- form validation
- error handling
- long text
- large quote totals
- many line items
- missing optional fields
- duplicated quotes
- settings changes

Add or complete automated tests for:

- calculation helpers
- quote numbering
- duplicate behaviour
- persistence logic where practical
- important form/domain validation

## Acceptance Criteria

- production build succeeds
- linting succeeds
- automated tests succeed
- no V1 non-goals have been introduced
- main workflow is usable without developer assistance

---

# Post-V1 Validation

Do not automatically implement post-V1 features.

After the plumber has used the application with real customers, gather evidence about:

- what information he repeatedly enters
- common materials
- common labour descriptions
- whether quote duplication is useful
- whether clients request invoices afterward
- whether deposits need tracking
- whether cloud backup is necessary
- whether he uses more than one device
- whether other tradespeople want the product

Future scope must be driven by observed usage rather than assumptions.

---

# Build Sequence

Implement milestones strictly in this order:

1. Project Setup
2. Domain Model and Storage
3. Home Screen
4. Quote Editor
5. Business Settings
6. Quote Preview
7. PDF Generation
8. Share, Save and Print
9. PWA and iPhone Validation
10. V1 Polish and Regression Review

Codex must stop after each milestone and report:

- files created/changed
- behaviour implemented
- tests/checks run
- unresolved issues
- any deviation required from `PRODUCT.md`

No subsequent milestone should begin until explicitly instructed.
