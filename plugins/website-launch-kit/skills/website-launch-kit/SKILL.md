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

## ⚠️ CRITICAL RULES — READ FIRST

### Rule 1: ONE Question Per Message

**NEVER combine multiple questions. NEVER ask 2+ things at once.**

❌ WRONG (combining questions):
```
Do you have social proof? What's your CTA? Do you have an inspiration website?
```

✅ RIGHT (one at a time):
```
Do you have social proof we can use?
```
→ Wait for answer →
```
What action should visitors take when they're ready?
```
→ Wait for answer →
```
Time to find your design inspiration... [show links]
```

### Rule 2: Use AskUserQuestion Tool

**Every question MUST use the `AskUserQuestion` tool for modal UI.**

### Rule 3: Design Inspiration is a SEPARATE STEP

**Never ask for inspiration URL together with other questions.**

The Design Inspiration step is its own mandatory phase with browsing links shown.

---

## Workflow Overview

```
PHASE 1A: Business Intake    → Questions about the business (Q1-17)
PHASE 1B: Design Inspiration → SEPARATE STEP with browsing links
PHASE 2:  Research           → Analyze inspiration site
PHASE 3:  Sections           → Propose page structure
PHASE 4:  Copywriting        → Write content
PHASE 5:  Copy Review        → Show 3 options
PHASE 6:  Development        → Build with React + Tailwind
PHASE 7:  Preview            → Run dev server
PHASE 8:  Iteration          → Make edits
PHASE 9:  Deploy             → Ship to Vercel
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

## PHASE 1A: Business Intake

**Goal:** Understand the business. Ask ONE question at a time.

### Starting Message

```
I'll help you create a landing page that actually converts.

This isn't a template — we'll build something custom based on your business.

Let's start with one question at a time.
```

### Question Flow (ONE AT A TIME)

Ask each question separately. Wait for answer before next question.

| # | Question | Options |
|---|----------|---------|
| 1 | Is this for a product or service? | Product / Service |
| 2 | What type specifically? | Consulting / Agency / Coaching / Freelance |
| 3 | What's the name of your business? | [text input] |
| 4 | What do customers get from you? | [text input] |
| 5 | Who is your ideal customer? | [text input] |
| 6 | What's their role? | Founder / Manager / Individual / Other |
| 7 | Company size? | Solo / Small / Growing / Large |
| 8 | What makes them start looking? | [text input] |
| 9 | Problem #1 to solve? | [text input] |
| 10 | Problem #2? | [text input] |
| 11 | Problem #3? | [text input] |
| 12 | What does success look like? | [text input] |
| 13 | How fast do they see results? | Days / 2-4 weeks / 1-3 months / Varies |
| 14 | Do you have a process? | Yes / No |
| 15 | Why should they choose you? | [text input] |
| 16 | What proof do you have? | Testimonials / Numbers / Logos / None |
| 17 | Why do people hesitate? | [text input] |
| 18 | What action should visitors take? | Book call / Sign up / Buy / Quote |
| 19 | What form fields do you need? | [text input] |

**After Q19, proceed to PHASE 1B — Design Inspiration.**

---

## PHASE 1B: Design Inspiration (MANDATORY SEPARATE STEP)

⚠️ **THIS IS A STANDALONE STEP. NEVER COMBINE WITH OTHER QUESTIONS.**

### Step 1: Show This EXACT Message

After completing business questions, show this:

```
Now for the fun part — let's find your design direction!

I need ONE website that captures the vibe you want for your landing page.

Here's where to browse:

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

Take your time browsing. When you find ONE site that makes you think "I want my site to feel like THIS", paste the URL here.
```

### Step 2: Wait for URL

Do not proceed until user provides a URL.

### Step 3: Ask Follow-up

After they share the URL:

```
AskUserQuestion(
  question: "How closely should we match this site?",
  options: [
    { label: "Close match", description: "Match the feel closely, make it mine" },
    { label: "Just inspiration", description: "Use general direction, be more unique" }
  ]
)
```

### Step 4: Ask Animation Preference

```
AskUserQuestion(
  question: "How much animation do you want?",
  options: [
    { label: "Subtle", description: "Smooth scroll reveals, gentle hover effects" },
    { label: "Dynamic", description: "Bold entrance animations, interactive elements" }
  ]
)
```

### Step 5: Proceed to Summary

Now compile everything and show summary.

---

## Intake Summary Template

After BOTH Phase 1A and 1B are complete:

```
Here's everything I gathered:

BUSINESS
- Name: [name]
- Type: [product/service]
- Offering: [what they provide]

AUDIENCE
- Who: [ideal customer]
- Role: [title]
- Size: [company size]

PROBLEMS
1. [problem 1]
2. [problem 2]
3. [problem 3]

SOLUTION
- Outcome: [transformation]
- Timeline: [how fast]
- Process: [steps if any]

WHY YOU
- Differentiator: [why choose them]
- Proof: [type]

CTA
- Action: [what visitors do]
- Form: [fields needed]

DESIGN DIRECTION
- Inspiration: [URL they shared]
- Match level: [close/inspiration]
- Animation: [subtle/dynamic]

Anything to add or correct before I analyze the inspiration site?
```

---

## PHASE 2: Research & Design Extraction

**Goal:** Analyze the inspiration site.

**Read:** `references/02-research-guide.md`

Try WebFetch first. If blocked, use browser_subagent:

```
browser_subagent(
  Task: "Navigate to [URL]. Take full-page screenshot.
         Analyze: colors, typography, layout, spacing, animations.",
  RecordingName: "inspiration_analysis"
)
```

Report findings and get confirmation before proceeding.

---

## PHASE 3-5: Sections, Copy, Review

**Read:**
- `references/03-section-blueprints.md`
- `references/04-copywriting-formulas.md`
- `references/05-copy-review.md`

Propose sections → Write copy → Show 3 options per element → Get approval.

---

## PHASE 6: Development

**Read:**
- `references/06-code-architecture.md`
- `references/07-design-system.md`
- `references/08-component-patterns.md`
- `references/12-visual-assets.md`

Build with Next.js + Tailwind + lucide-react icons.

---

## PHASE 7-8: Preview & Iteration

**Read:**
- `references/09-local-preview.md`
- `references/10-iteration-guide.md`

Run dev server, gather feedback, iterate.

---

## PHASE 9: Deploy

**Read:** `references/11-deployment.md`

Deploy to Vercel, provide live URL.

---

## Core Principles

1. **ONE question per message** — Never combine
2. **Design inspiration is SEPARATE** — Always show browsing links
3. **Use AskUserQuestion tool** — For clean modal UI
4. **Their words become copy** — Extract language from intake
5. **Customize everything** — No generic templates
6. **Validate each phase** — Get approval before proceeding
7. **3 options for copy** — Give choices, let them pick

---

## Quality Checks

Before deployment:
- `references/13-web-design-guidelines.md` — UI/UX checklist
- Accessibility (focus states, labels, alt text)
- Mobile responsiveness
- Performance (image optimization)
