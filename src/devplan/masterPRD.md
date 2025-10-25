# masterPRD.md — Rooms & Therapy (MVP)
**Product:** Rooms & Therapy — Coliving + Therapy & Coaching  
**Scope:** MVP (minimal viable product) website focused on discovery, trust, and easy booking/queries  
**Owner:** Adeline Lee  
**Market:** Singapore  
**Doc Type:** Product Requirements Document (PRD) organized by features  
**Non‑Goals (MVP):** No online payments, no resident portal, no automated room allocation, no subsidy claims processing, no complex CRM

---

## 0) Product Overview
### Problem
People in Singapore seeking calm, community‑oriented living and/or gentle therapeutic support struggle to find a single, trustworthy destination that makes it simple to understand the offer, gain confidence, and book a conversation.

### Vision
A serene, nature‑inspired website that clearly separates the two offers — **Coliving** and **Therapy & Coaching** — with trust signals and fast paths to contact/booking.

### Primary Users
- **Students / Working Adults** seeking quiet coliving and gentle accountability.
- **Seniors & Caregivers** seeking occupational therapy and purposeful activities.
- **Referrers** (allied health, social workers) who need clarity and credibility.

### Success Metrics (MVP)
- **Discovery call bookings** (target 10–20/month to start)  
- **Lead volume** via form/WhatsApp (target CR ≥ 2–4% from unique visitors)  
- **CTA CTR** (Hero CTAs ≥ 5–8%)  
- **Page speed (LCP)** ≤ 2.5s on mobile; Core Web Vitals pass  
- **Bounce rate** on Home ≤ 55% (directional; content‑fit dependent)

### Assumptions
- Users prefer WhatsApp and a short discovery call over long forms.
- Manual handling of availability is acceptable in MVP.
- Therapy is non‑emergency, outpatient/community oriented.

### Out of Scope (MVP)
- Payments & invoicing, member portal, automated matching, insurance/subsidy claims, advanced CRM, HIPAA‑grade EMR, event ticketing.

---

## 1) Architecture & Platform (Foundation)
**Goal:** Deliver a simple, fast site that the owner can update easily.

**Decision (provisional):**
- **Stack:** Static site (e.g., Netlify/Cloudflare Pages) + Markdown content  
- **CMS:** Lightweight (Git‑based or Notion-to-static), optional in MVP  
- **Forms:** Netlify Forms / Tally / Typeform (one provider)  
- **Scheduling:** Calendly embeds for discovery calls  
- **Messaging:** WhatsApp click‑to‑chat link  
- **Email list:** Mailerlite embedded form  
- **Analytics:** Google Analytics 4 (GA4) (+ optional Google Tag Manager)  
- **SEO:** Basic metadata & JSON‑LD

**Non‑Functional Requirements**
- Mobile‑first, WCAG AA contrasts, keyboard navigable, alt text on images
- Performance budget: image WebP, lazy‑load, responsive sizes

**Acceptance Criteria**
- [ ] Site builds without errors and deploys to production domain  
- [ ] GA4 fires pageview events; key CTA events recorded  
- [ ] Forms capture and deliver submissions to a single inbox  
- [ ] Calendly and Mailerlite embeds render on mobile and desktop

**Risks/Dependencies**
- Domain/DNS control, embed compatibility, form spam (mitigate with honeypot/reCAPTCHA lightweight).

---

## 2) Feature: Home Hero with Dual CTAs
**Problem:** Users need to quickly self‑select **Coliving** vs **Therapy & Coaching**.

**User Stories**
- As a visitor, I can understand in 5 seconds what the site offers and choose my path.
- As a risk‑averse caregiver, I can see credibility before I click deeper.

**Functional Requirements**
- H1: “Rooms & Therapy — Community Living, Thoughtful Care (Singapore)”  
- Subheading: one‑sentence value prop  
- Two primary CTAs: **Coliving** (/coliving) and **Therapy & Coaching** (/therapy)  
- Tertiary CTAs: **WhatsApp**, **Book a Consult** (Calendly modal or /contact)

**UX Content (MVP)**
- Calm hero image (nature/room), high‑contrast overlay text
- Short tagline + two prominent buttons

**Acceptance Criteria**
- [ ] Hero loads within 1s of LCP (optimized image)  
- [ ] Buttons are 44px min height, keyboard/tab accessible  
- [ ] Screen readers announce H1 and CTAs meaningfully (“Go to Coliving” / “Go to Therapy & Coaching”)

**Tracking**
- GA4 event: `cta_click` with params `{label: "coliving"|"therapy"|"whatsapp"|"consult"}`

**Risks/Dependencies**
- Image licensing; alt text quality.

---

## 3) Feature: Audience Cards (Who We Support)
**Problem:** Visitors need to see themselves reflected.

**User Stories**
- As a student/working adult/senior/caregiver, I see a short description validating my needs.

**Functional Requirements**
- Three cards: **Students**, **Working Adults**, **Seniors & Caregivers**  
- Each card: 1–2 lines benefit text; optional “Learn more” anchors

**Acceptance Criteria**
- [ ] Cards are readable on small screens  
- [ ] Icons/images have alt text or are decorative

**Tracking**
- GA4: `card_click` with `{audience: "students"|"adults"|"seniors_caregivers"}`

---

## 4) Feature: Coliving Listing (Static MVP)
**Problem:** Users want to see spaces and understand how to enquire.

**User Stories**
- As a prospect, I can view representative rooms/common areas and enquire without friction.
- As an owner, I can update availability manually (text label) in Markdown.

**Functional Requirements**
- Page: `/coliving`  
- Components: intro, 3–6 photos (WebP), short highlights, **availability status** (text), **House Rules** link, **Enquire/Discovery Call** CTA  
- No online booking; manual follow‑up.

**Acceptance Criteria**
- [ ] Photos lazy‑load; captions/alt text present  
- [ ] “View Spaces & Availability” CTA links to the enquiry form or Calendly  
- [ ] House Rules link visible above the fold or near CTA

**Tracking**
- GA4 events: `view_coliving`, `cta_click: enquire_coliving`

**Risks/Dependencies**
- Photo quality; expectations management without live inventory.

---

## 5) Feature: Therapy & Coaching Services
**Problem:** Prospects need clarity on OT vs Art & Wellness vs Coaching, and how to start.

**User Stories**
- As a caregiver, I can skim what services exist and book a consult.
- As a referrer, I can verify credentials and scope quickly.

**Functional Requirements**
- Page: `/therapy`  
- Sections: OT (seniors/caregivers), Art & Wellness, Coaching; **Not an emergency service** notice; **Crisis resources** link; **Book Discovery Call** CTA  
- Simple intake link (Tally/Typeform) for pre‑session info (Name, goals, availability, consent checkbox)

**Acceptance Criteria**
- [ ] Clear distinction: clinical OT vs non‑medical coaching  
- [ ] Crisis disclaimer visible; link to resources page  
- [ ] Intake form submits and sends email notification to owner

**Tracking**
- GA4: `view_therapy`, `cta_click: book_therapy`, `form_start/intake`, `form_submit/intake`

**Risks/Dependencies**
- Consent copy accuracy; boundaries between services.

---

## 6) Feature: Contact / Book (Single Page)
**Problem:** Provide multiple, low‑friction contact options.

**User Stories**
- As a visitor, I can choose WhatsApp, Calendly, or form—whichever is easiest.

**Functional Requirements**
- Page: `/contact` with:  
  - WhatsApp click‑to‑chat (phone configurable)  
  - Calendly embed (15‑min discovery)  
  - Short enquiry form (Name, Email/Phone, Interest: Coliving/Therapy/Coaching, Message, PDPA consent checkbox)

**Acceptance Criteria**
- [ ] All three methods function on mobile and desktop  
- [ ] Form stores submissions and emails confirmation to owner inbox  
- [ ] Thank‑you confirmation message is visible after submit

**Tracking**
- GA4: `cta_click: whatsapp`, `cta_click: calendly_open`, `form_submit: enquiry`

**Risks/Dependencies**
- Spam mitigation; Calendly load performance.

---

## 7) Feature: Trust & Credentials Module
**Problem:** Early reassurance for risk‑averse visitors.

**User Stories**
- As a caregiver, I can see relevant credentials and governance signals (house rules/PDPA).

**Functional Requirements**
- Component used on Home and Therapy pages:  
  - Credentials/experience bullets (concise)  
  - Partners/affiliations (if any)  
  - House Rules & PDPA links

**Acceptance Criteria**
- [ ] Module visible without excessive scrolling on both pages  
- [ ] Links work and are readable

**Tracking**
- GA4: `module_view: trust`, `link_click: house_rules`, `link_click: privacy`

---

## 8) Feature: House Rules & PDPA
**Problem:** Clear expectations and lawful data handling.

**User Stories**
- As a resident/client, I can understand rules and how my data is handled.

**Functional Requirements**
- Pages: `/policies` (House Rules), `/privacy` (PDPA notice)  
- House Rules: safety, quiet hours, guests, shared space etiquette, incident escalation  
- PDPA: what data is collected, why, retention, access/withdrawal, contact for queries

**Acceptance Criteria**
- [ ] Pages accessible from footer and relevant CTAs  
- [ ] Plain‑English summaries with anchor links  
- [ ] Checkbox consent on forms references PDPA page

**Risks/Dependencies**
- Jurisdiction changes; legal review recommended.

---

## 9) Feature: FAQ (Light)
**Problem:** Reduce bounce and inbound queries by answering top concerns.

**User Stories**
- As a visitor, I can get quick answers without contacting support.

**Functional Requirements**
- 5–7 Q&As covering: therapy availability for non‑residents, caregiver sessions, space allocation, subsidies eligibility (contact to confirm), emergency disclaimer.

**Acceptance Criteria**
- [ ] Expand/collapse works with keyboard  
- [ ] Links to Contact and Crisis pages present

**Tracking**
- GA4: `faq_expand` with `{question_id}`

---

## 10) Feature: Waitlist / Newsletter (Mailerlite)
**Problem:** Capture interest when spaces or slots aren’t immediately available.

**User Stories**
- As a visitor, I can join a waitlist/newsletter in one field (email).

**Functional Requirements**
- Embedded Mailerlite form; success state; double‑opt‑in

**Acceptance Criteria**
- [ ] Successful signup adds to Mailerlite audience  
- [ ] Visible confirmation copy; error handling for invalid email

**Tracking**
- GA4: `newsletter_subscribe`

**Risks/Dependencies**
- Deliverability; double‑opt‑in configuration.

---

## 11) Feature: Footer & Utility Nav
**Problem:** Ensure navigability and trust site‑wide.

**Functional Requirements**
- Footer with: Contact, WhatsApp, Address/Area served (approx.), Policies, Socials (optional)  
- Utility header links to Coliving, Therapy, Contact

**Acceptance Criteria**
- [ ] Sticky contact on mobile (WhatsApp) optional; must not obstruct content  
- [ ] All footer links tab‑navigable

---

## 12) Feature: Basic SEO & Schema
**Problem:** Be discoverable for branded and local searches.

**Functional Requirements**
- Unique meta title/description per page  
- H1 reflects page intent (e.g., “Coliving in Singapore”)  
- JSON‑LD Organization with two departments (LodgingBusiness, LocalBusiness)  
- Alt text on images; readable URLs; internal links (Home→Coliving→Policies / Home→Therapy→Contact)

**Acceptance Criteria**
- [ ] Metadata present in `<head>` on all pages  
- [ ] JSON‑LD validates in Rich Results Test  
- [ ] Lighthouse SEO score ≥ 90 (guideline)

---

## 13) Feature: Analytics & Reporting
**Problem:** Know what’s working.

**Functional Requirements**
- GA4 base tag on all pages  
- Events: `cta_click`, `form_start`, `form_submit`, `calendly_open`, `newsletter_subscribe`, `faq_expand`, page groups (home/coliving/therapy/contact)  
- Simple monthly report (exported from GA) — traffic, conversions, top pages

**Acceptance Criteria**
- [ ] Events visible in GA4 debug view  
- [ ] Basic dashboard saved in GA4 Library

---

## Content Inventory (MVP)
- Hero heading + subhead (final)  
- Home: 3 audience blurbs, trust module bullets  
- Coliving: 3–6 photos + captions; highlights; availability text; House Rules link  
- Therapy: three service blurbs; crisis disclaimer; intake form link  
- Contact page: WhatsApp number, Calendly link, short form fields & PDPA consent copy  
- Policies: House Rules (short + detailed sections), PDPA notice  
- FAQ: 5–7 entries  
- Footer: address/area, links

---

## Privacy, Safety & Ethics
- PDPA consent on forms; clear purpose, retention, contact for access/withdrawal  
- Crisis resources link (explicit non‑emergency statement)  
- Limit data requested in MVP: name, email/phone, interest, free‑text message; intake form requests only essentials

---

## Dependencies
- Domain control, Netlify/hosting account, GA4 property, Calendly, Mailerlite, Form provider (Tally/Typeform/Netlify Forms), image assets.

---

## Open Questions
1. Final WhatsApp number & preferred hours?
2. Calendly slot rules (buffer, working days)?
3. Chosen form provider and email destination?
4. Neighborhood/area disclosure (how specific)?
5. Any partners/affiliations to list at launch?
6. Are testimonials available for post‑MVP?

---

## Roadmap (Post‑MVP Ideas, not in scope now)
- Testimonials & Reviews module  
- Blog/Journal  
- Photo gallery per room  
- Generic payment link (PayNow/Stripe) for deposits/invoices  
- Member resources page (private)  
- Inventory badges for room availability

---

## Glossary
- **MVP:** Minimum Viable Product  
- **OT:** Occupational Therapy  
- **PDPA:** Personal Data Protection Act (Singapore)  
- **GA4:** Google Analytics 4

