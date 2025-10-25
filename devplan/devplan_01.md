---
owner: Codex Agent – Frontend Generator
status: drafting
last_reviewed: 2024-04-16
---

# Dev Plan 01 — Home Hero with Dual CTAs

## Design / Architecture
- Implement hero as a dedicated React component `HeroSection` under `src/components/home/HeroSection.tsx`, leveraging existing design system primitives (Shadcn/UI `Button`, typography utilities, and layout containers).
- Structure layout with a responsive split stack that centers content within a max-width container and applies Tailwind background overlay for readability over the hero image.
- Configure CTA buttons using shared button variants (`primary`, `secondary`) to ensure consistent styling; include icon adornments (e.g., `MessageCircle`, `Calendar`) from Lucide icons set already available in project dependencies.
- Provide responsive spacing and text scaling via Tailwind breakpoints (`sm`, `md`, `lg`); ensure hero height adapts to viewport while respecting content-first layout.

## Data / Content Strategy
- Store hero copy (H1 and subheading) and CTA metadata in a dedicated configuration file `src/content/homeHero.ts` exporting typed constants so marketing adjustments require minimal code changes.
- Include placeholder values for subheading and image alt text until final copy/assets arrive, with comments referencing masterPRD TODO owners.
- Centralize URLs (WhatsApp link, Calendly/contact path) within the content file to facilitate analytics instrumentation and future localization.

## Integrations & Analytics
- Extend `src/lib/analytics.ts` (or create if absent) with a `trackEvent` helper to encapsulate GA4 `cta_click` dispatching; ensure hero buttons invoke this helper with appropriate labels (`coliving`, `therapy`, `whatsapp`, `consult`).
- Implement the Calendly modal overlay via a lazy-loaded component to protect initial load performance and wire analytics hooks
  for open/close events; provide `/contact` navigation as a fallback link within the modal description.

## Testing Strategy
- Add unit tests in `src/__tests__/home/HeroSection.test.tsx` verifying:
  - Required headings and CTA buttons render with accessible labels.
  - CTA href targets align with configuration values.
  - Analytics helper is called with correct payloads upon simulated clicks.
- Implement visual regression coverage via Storybook snapshot or Chromatic if pipeline exists; otherwise prepare manual QA checklist capturing responsive behavior (mobile/desktop) and keyboard navigation.

## Risks & Mitigations
- **Risk:** Final assets arrive late, delaying polish. **Mitigation:** Ship with placeholder imagery plus TODO markers and swap once assets approved.
- **Risk:** Overly heavy hero image harms LCP. **Mitigation:** Enforce responsive `Image` component with `loading="lazy"` and provide WebP plus fallback.
- **Risk:** Event tracking drifts from GA4 schema. **Mitigation:** Document event names in analytics helper and add unit tests verifying payload shape.

## Open Dependencies / Follow-ups
- Await responses to copy and imagery TODOs from Adeline Lee (masterPRD.md §2).
- Implement Calendly modal overlay for the consult CTA per stakeholder alignment; include an accessibility review of modal cont
  rols before launch.
