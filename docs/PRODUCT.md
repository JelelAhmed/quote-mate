# Plumber Quote App — V1 Product Specification

## 1. Product Goal

Build a small mobile-first web application that allows a plumber to create professional quotations, generate them as PDF files, and either:

- share them digitally, especially through WhatsApp, or
- print them as standard paper documents for traditional clients.

The app replaces handwritten quotations.

The first version is for one primary user and should stay intentionally small.

---

## 2. Primary User

A self-employed plumber or small plumbing business that currently prepares customer quotations manually.

The user is expected to use the app mainly from an iPhone.

---

## 3. Core User Outcome

The user should be able to create a complete customer quotation in a few minutes.

Primary workflow:

`Home → New Quote → Enter Client Details → Add Quote Items → Review Totals → Preview → Generate PDF → Share or Print`

---

## 4. V1 Scope

V1 must support:

- business profile
- client details
- quotation details
- itemised quote entries
- automatic calculations
- optional additional charges or discounts
- notes and terms
- quotation preview
- PDF generation
- WhatsApp-compatible sharing
- printing
- saving quotations locally
- editing existing quotations
- duplicating quotations
- deleting quotations

---

## 5. Screens

### 5.1 Home

Purpose:

Provide fast access to creating and managing quotations.

Contents:

- business/app name
- prominent `New Quote` button
- recent quotations
- each quotation should show:
  - client name
  - quote number
  - date
  - total
- open quotation
- duplicate quotation
- delete quotation

V1 does not require complex filtering or analytics.

### 5.2 Quote Editor

The Quote Editor should be one mobile-friendly scrollable screen rather than many separate steps.

It contains the following sections.

#### Client Details

Fields:

- Client name — required
- Phone number — optional
- Address / job location — optional
- Project or job description — optional

#### Quote Details

Fields:

- Quote number — automatically generated but editable
- Quote date — defaults to current date
- Valid until — optional

Example generated quote number:

`QT-0001`

The numbering format may change later.

#### Quote Items

The user can add any number of line items.

Each item contains:

- Description — required
- Quantity — required, default `1`
- Unit — optional
- Unit price — required
- Amount — automatically calculated

Formula:

`Amount = Quantity × Unit Price`

Example:

| Description | Qty | Unit | Unit Price | Amount |
|---|---:|---|---:|---:|
| 25mm PVC Pipe | 6 | Length | ₦4,500 | ₦27,000 |
| Elbow Fittings | 10 | Pcs | ₦850 | ₦8,500 |
| Installation Labour | 1 | Job | ₦45,000 | ₦45,000 |

Suggested unit options:

- Pcs
- Length
- Roll
- Set
- Bag
- Metre
- Hour
- Job
- Other

The user must also be able to enter a custom unit.

Items can represent either materials or labour.

Do not build separate material and labour systems in V1.

#### Additional Amounts

Support:

- Transport / delivery charge — optional
- Other charge — optional
- Discount — optional

The interface should remain simple.

These may be implemented either as dedicated fields or normal quote items where appropriate.

#### Totals

Automatically calculate:

- Subtotal
- Additional charges
- Discount
- Grand total

All monetary amounts should use Nigerian Naira by default.

Display format:

`₦125,000`

Currency architecture should not unnecessarily prevent future support for another currency.

#### Notes / Terms

Optional free-text section.

Possible contents include:

- payment expectations
- quotation validity
- exclusions
- work conditions
- thank-you note

No complex legal terms system is required.

---

## 6. Quote Preview

Before PDF generation, the user should see a preview closely representing the final document.

The preview should show:

- business identity
- quotation heading
- quote number
- quote date
- validity date if present
- client details
- job/project description if present
- line-item table
- subtotal
- additional charges
- discount
- grand total
- notes / terms
- business contact information

Actions:

- Edit Quote
- Generate PDF

---

## 7. PDF Document

The PDF is the primary output of the application.

It must work equally well:

- when viewed on a phone,
- when sent through WhatsApp,
- when sent through email,
- and when printed on A4 paper.

### PDF Style

Use:

- white background
- dark readable text
- one restrained accent colour
- professional typography
- generous spacing
- clear hierarchy
- clean tables
- strong emphasis on the total

Avoid:

- dark-mode PDFs
- excessive decoration
- gradients
- unnecessary graphics
- designs that consume excessive ink when printed

### PDF Structure

Recommended order:

1. Business logo/name and contact details
2. `QUOTATION` heading
3. Quote number and date
4. Client details
5. Job / project description
6. Itemised quotation table
7. Totals
8. Notes / terms
9. Business contact/footer

The quotation should feel like a professional trade document rather than a generic ecommerce receipt.

---

## 8. Sharing and Printing

After generating the PDF, provide clear actions for:

- Share
- Print
- Save PDF

On supported mobile devices, use the browser/device sharing interface where possible so the user can choose WhatsApp directly.

The application does not need direct WhatsApp API integration in V1.

---

## 9. Saved Quotations

V1 should store quotations locally on the device/browser.

Each saved quote should retain:

- client details
- quote details
- all items
- totals
- notes
- creation date
- last edited date

Supported actions:

- open
- edit
- duplicate
- delete
- regenerate PDF

Duplicate should create a new quotation based on the old one while assigning a new quote number.

This is important because tradespeople frequently prepare similar quotations.

---

## 10. Business Settings

Provide a simple Settings screen.

Fields:

- Business name
- Owner/contact name
- Phone number
- Email — optional
- Address — optional
- Logo — optional
- Default quotation notes — optional

These values should automatically populate future quotations and PDFs.

The user should not need to re-enter business details for every quote.

---

## 11. Storage

V1 should use local browser storage.

Preferred implementation:

- IndexedDB
- a lightweight, well-maintained abstraction over IndexedDB is acceptable

Avoid introducing a backend solely for V1.

The product should be architected so cloud storage and authentication can be added later without rewriting the entire quote domain model.

---

## 12. Platform

Build as:

**Mobile-first Progressive Web App**

Recommended stack:

- Next.js
- TypeScript
- Tailwind CSS
- PWA support
- client-side persistent storage
- browser-compatible PDF generation

Primary target:

- Safari on iPhone

Secondary target:

- modern desktop and Android browsers

The app should also work when launched from the iPhone Home Screen after being installed as a PWA.

---

## 13. Mobile UX Requirements

The application should be comfortable to operate one-handed on a phone.

Prioritise:

- large touch targets
- minimal typing
- obvious primary actions
- numeric keyboard for prices and quantities
- automatic calculations
- simple item creation
- clear totals
- fast return to recent quotations

Do not build a desktop-style accounting interface and shrink it onto mobile.

---

## 14. V1 Non-Goals

Do not implement the following in V1:

- inventory management
- stock tracking
- accounting
- expense management
- payment processing
- payment tracking
- customer portal
- employee management
- job scheduling
- project management
- receipts
- supplier management
- purchase orders
- complex dashboards
- analytics
- online customer accounts
- authentication
- cloud synchronisation
- multi-user support
- subscription billing
- direct WhatsApp API integration

These should not be introduced without a later product decision.

---

## 15. Product Principle

The V1 product has one job:

**Turn the plumber's handwritten quotation process into a fast, professional digital workflow.**

Any feature that does not materially improve:

`Create Quote → Generate PDF → Send or Print`

should normally be excluded from V1.

---

## 16. Pending Validation

Once examples of the user's real handwritten quotations are available, review this specification against them.

Specifically validate:

- fields he normally records
- terminology he uses
- treatment of labour
- treatment of transport
- units used for plumbing materials
- whether prices are normally itemised
- payment terms
- quotation validity
- document branding
- client expectations
- layout of the final printed quotation

Adjust the application to match the real workflow rather than forcing the existing workflow into this provisional structure.
