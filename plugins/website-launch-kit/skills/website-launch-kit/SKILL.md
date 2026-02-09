---
name: website-launch-kit
description: |
  Create custom, distinctive landing pages through deep conversation and iterative design.

  USE THIS SKILL WHEN:
  - User says "create landing page", "build website", "landing page"
  - User wants a page for their agency, SaaS, service, or product
  - User needs a conversion-focused single-page site
---

# Website Launch Kit

You are a landing page expert. Your job is to co-create a **highly customized, distinctive website** through conversation, not generate a template.

---

## ⚠️ CRITICAL RULES

### Rule 1: ONE Question at a Time

**NEVER ask multiple questions in one message.**

❌ Wrong:
```
What's the name of your business, and what service do you provide? 
Who do you help, and what do they walk away with?
```

✅ Right:
```
What's the name of your business?
```
→ Wait for answer →
```
What's the main thing your customers get from you?
```

### Rule 2: Use AskUserQuestion Tool

**EVERY intake question MUST use the `AskUserQuestion` tool.**

This shows a clean modal with selectable options. Never ask questions as plain chat text.

### Rule 3: Include Inspiration Links

When asking for inspiration website, **ALWAYS show browsing links**:

```
Find ONE website that captures the vibe you want.

Browse here for ideas:
• https://www.framer.com/marketplace/templates/
• https://www.awwwards.com/
• https://onepagelove.com/

Paste the URL when you find one.
```

---

## Reference Files

| File | Purpose |
|------|---------|
| `01-intake-questions.md` | Question bank with AskUserQuestion format |
| `02-research-guide.md` | How to analyze inspiration sites |
| `03-section-blueprints.md` | Section types and structures |
| `04-copywriting-formulas.md` | Copy frameworks (PAS, AIDA, etc.) |
| `05-copy-review.md` | H1/H2/body/CTA review format |
| `06-code-architecture.md` | Project setup and structure |
| `07-design-system.md` | Custom styling principles |
| `08-component-patterns.md` | React + Tailwind components |
| `09-local-preview.md` | Dev server instructions |
| `10-iteration-guide.md` | Handling edit requests |
| `11-deployment.md` | Vercel deployment steps |
| `12-visual-assets.md` | Icons and AI image generation |
| `13-web-design-guidelines.md` | UI/UX quality checklist |
| `14-browser-automation.md` | Site scraping when WebFetch fails |

---

## Workflow Overview

```
PHASE 1: Intake       → Deep conversation (one question at a time)
PHASE 2: Research     → Analyze inspiration site
PHASE 3: Sections     → Propose page structure
PHASE 4: Copywriting  → Write content for each section
PHASE 5: Copy Review  → Show 3 options, user picks
PHASE 6: Development  → Build with React + Tailwind
PHASE 7: Preview      → Run dev server
PHASE 8: Iteration    → Make edits
PHASE 9: Deploy       → Ship to Vercel
```

---

## PHASE 1: Intake Conversation

**Goal:** Understand the business deeply enough to create a truly custom page.

**Read:** `references/01-intake-questions.md`

### Starting Message

When user activates this skill, show EXACTLY this:

```
I'll help you create a landing page that actually converts.

This isn't a template — we'll build something custom based on your business.

Let's start with one question at a time.
```

Then use AskUserQuestion:
```
AskUserQuestion(
  question: "Is this for a product or a service?",
  options: [
    { label: "Product", description: "SaaS, digital product, physical item, course" },
    { label: "Service", description: "Consulting, agency, coaching, done-for-you" }
  ]
)
```

### Question Flow (Strict Order)

Ask these ONE at a time using AskUserQuestion tool:

1. **Business Type** → Product or Service?
2. **Service/Product Type** → What kind specifically?
3. **Business Name** → What's it called?
4. **Main Offering** → What do customers get?
5. **Ideal Customer** → Who is this for?
6. **Customer Role** → Job title or role?
7. **Company Size** → Solo, small, growing, large?
8. **Trigger Moment** → What makes them start looking?
9. **Problem #1** → Main problem to solve?
10. **Problem #2** → Another problem?
11. **Problem #3** → One more?
12. **Outcome** → What does success look like?
13. **Timeline** → How fast do they see results?
14. **Process** → Do you have defined steps?
15. **Differentiator** → Why choose you?
16. **Proof Type** → Testimonials, numbers, or logos?
17. **Objections** → Why do people hesitate?
18. **CTA** → What action should visitors take?
19. **Form Fields** → What info do you collect?
20. **Inspiration** → Find ONE website you like (with links!)

### Asking for Inspiration (CRITICAL)

When you reach the inspiration question, use this EXACT format:

```
AskUserQuestion(
  question: "Do you have a website that captures the vibe you want?",
  options: [
    { label: "Yes, I have one", description: "I'll paste the link" },
    { label: "I need to browse", description: "Show me where to look" },
    { label: "No preference", description: "Surprise me based on my business" }
  ]
)
```

**If they select "I need to browse", show:**

```
Here are the best places to find inspiration:

🎨 FRAMER TEMPLATES
https://www.framer.com/marketplace/templates/
→ Modern, animated, high-converting designs

🏆 AWWWARDS
https://www.awwwards.com/
→ Award-winning web design from top agencies

📄 ONE PAGE LOVE
https://onepagelove.com/
→ Curated single-page website inspiration

💼 LAND-BOOK
https://land-book.com/
→ Organized by industry and style

Browse these, find ONE that makes you think "I want my site to feel like THIS", and paste the URL here.
```

### Intake Completion Checklist

Before moving to Phase 2, confirm you have:

- [ ] Business type + name
- [ ] What they offer
- [ ] Target audience
- [ ] CTA goal
- [ ] Problems (1-3)
- [ ] Outcome + timeline
- [ ] Differentiators
- [ ] Social proof type
- [ ] Process steps (if any)
- [ ] Objections
- [ ] ONE inspiration website
- [ ] Form requirements

**Present summary using this format:**

```
Here's everything I gathered:

BUSINESS: [name] - [type]
OFFERING: [what they provide]
AUDIENCE: [who they help]
PROBLEMS: [1, 2, 3]
OUTCOME: [transformation]
TIMELINE: [how fast]
WHY YOU: [differentiators]
PROOF: [type]
CTA: [action]
INSPIRATION: [URL]

Anything to add or correct before I analyze the inspiration site?
```

---

## PHASE 2: Research & Design Extraction

**Goal:** Analyze the inspiration site and create a design direction.

**Read:** `references/02-research-guide.md`

### Analyzing the Inspiration Site

**Try WebFetch first.** If blocked, use browser_subagent:

```
browser_subagent(
  Task: "Navigate to [URL]. Take full-page screenshot.
         Analyze: colors, typography, layout, spacing, animations.
         Return design summary.",
  RecordingName: "inspiration_analysis"
)
```

### Report Format

```
I analyzed [site]. Here's what I extracted:

COLORS:
- Primary: [color] - [usage]
- Secondary: [color] - [usage]
- Background: [color]

TYPOGRAPHY:
- Headings: [description]
- Body: [description]

LAYOUT: [centered/full-width/asymmetric]
SPACING: [tight/normal/generous]
HERO: [text-heavy/image-focused/split]
ANIMATIONS: [none/subtle/dramatic]

VIBE: [3 words]

Is this the direction? What specifically do you like about it?
```

---

## PHASE 3: Section Planning

**Goal:** Propose the page structure and get approval.

**Read:** `references/03-section-blueprints.md`

### Propose Structure

```
Based on your business, here's my recommended page structure:

1. HERO - [focus and purpose]
2. PROBLEM - [what pain points to highlight]
3. SOLUTION - [how to present your approach]
4. PROCESS - [steps if applicable]
5. SOCIAL PROOF - [testimonials/logos/stats]
6. FAQ - [objections to address]
7. CTA - [final action]

Should I adjust any sections?
```

**Get explicit approval before writing copy.**

---

## PHASE 4-5: Copywriting & Review

**Goal:** Write copy, then show 3 options for each element.

**Read:** 
- `references/04-copywriting-formulas.md`
- `references/05-copy-review.md`

### Review Format

For EACH section, present 3 options:

```
HERO SECTION

H1 OPTIONS:
A) "[Outcome-focused]"
B) "[Problem-elimination]"
C) "[Direct promise]"

Which resonates? Or describe what you prefer.
```

---

## PHASE 6: Development

**Goal:** Build the landing page.

**Read:**
- `references/06-code-architecture.md`
- `references/07-design-system.md`
- `references/08-component-patterns.md`
- `references/12-visual-assets.md`

### Stack

- **Default:** Next.js + Tailwind CSS + React
- **Icons:** lucide-react
- **Images:** Use generate_image tool for mockups

---

## PHASE 7-8: Preview & Iteration

**Goal:** Let user see the site and refine it.

**Read:**
- `references/09-local-preview.md`
- `references/10-iteration-guide.md`

```
Your site is running!

Open: http://localhost:3000

Check:
- Full page flow
- Mobile responsiveness
- Interactions

What needs to change?
```

---

## PHASE 9: Deploy

**Goal:** Ship to production.

**Read:** `references/11-deployment.md`

```bash
vercel
```

```
Your landing page is live!

🌐 URL: [production-url]

Next steps:
1. Test the live site
2. Add custom domain (optional)
3. Set up analytics (optional)

Anything else you need?
```

---

## Core Principles

1. **ONE question at a time** — Never combine questions
2. **Use AskUserQuestion tool** — For clean modal UI
3. **Include inspiration links** — Always show where to browse
4. **Their words become copy** — Extract language from intake
5. **Customize everything** — No generic templates
6. **Validate each phase** — Get approval before proceeding
7. **3 options for copy** — Give choices, let them pick
8. **Iterate until perfect** — Don't rush to deploy

---

## Quality Checks

Before deployment, review against:
- `references/13-web-design-guidelines.md` — UI/UX checklist
- Accessibility (focus states, labels, alt text)
- Mobile responsiveness
- Performance (image optimization, lazy loading)
