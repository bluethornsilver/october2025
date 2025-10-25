---
owner: Codex Agent – Frontend Generator
status: drafting
last_reviewed: 2024-04-16
---

# Feature PRD 01 — Home Hero with Dual CTAs

## Story
Create a welcoming hero section on the homepage that allows visitors to immediately understand the Rooms & Therapy offering and branch into the appropriate journey (Coliving vs Therapy & Coaching) while surfacing trust-building options and fast contact paths.

## Acceptance Criteria
- Hero copy implements the H1 specified in the master PRD and the approved one-sentence subheading once provided.
- Two primary CTA buttons link to `/coliving` and `/therapy`, and are fully accessible (keyboard focus, aria-labels, 44px min height).
- Secondary CTA group offers WhatsApp deep link and consult booking entry (Calendly modal or `/contact` page) with analytics events configured per GA4 plan.
- Background media is optimized for Core Web Vitals targets (responsive sizing, WebP, lazy loading) while maintaining contrast ratios that meet WCAG 2.1 AA.
- Initial viewport renders the hero without layout shift and maintains responsive composition for mobile (≤360px width) and desktop (≥1280px width).

## Dependencies
- Final hero subheading copy and background image licensing details from Adeline Lee (see inline TODOs in masterPRD.md §2).
- Finalize Calendly modal configuration and accessibility checklist for the "Book a Consult" CTA per approved approach.
- GA4 implementation framework for custom event dispatch utilities in the codebase.

## Open Questions
1. Should the secondary CTAs be grouped as icon buttons or remain text buttons for clarity on mobile? (Propose text buttons with supporting icons if design library permits.)
2. Is there a preferred hero image aspect ratio that aligns with existing photography assets?

## Decisions & Rationale
- **Book a Consult CTA behavior:** Adopt the **Calendly modal overlay** pattern to keep visitors on the homepage while offering immediate slot selection. This aligns with the master PRD emphasis on fast contact paths and ensures a consistent scheduling expectation. The `/contact` page remains available as a secondary option for users who prefer more context.
