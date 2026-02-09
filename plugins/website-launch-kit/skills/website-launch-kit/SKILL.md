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

### Question Flow (ONE AT A TIME — use AskUserQuestion for EVERY question)

Ask each question using `AskUserQuestion()`. Wait for answer before next question.

**Read `references/01-intake-questions.md` for the full question bank with branching logic.**

#### Q1: Business Type

```
AskUserQuestion(
  question: "Is this for a product or a service?",
  options: [
    { label: "Product", description: "SaaS, app, digital or physical product" },
    { label: "Service", description: "Agency, consulting, freelance, coaching" }
  ]
)
```

#### Q2: Specific Type (branch based on Q1)

If Service:
```
AskUserQuestion(
  question: "What type of service do you provide?",
  options: [
    { label: "Consulting", description: "Strategy and expert advice" },
    { label: "Agency / Done-for-you", description: "You deliver finished work" },
    { label: "Coaching / Training", description: "You teach or guide people" },
    { label: "Freelance / Creative", description: "Design, writing, dev, etc." }
  ]
)
```

If Product:
```
AskUserQuestion(
  question: "What type of product is this?",
  options: [
    { label: "SaaS / Software", description: "Online tool or app" },
    { label: "Digital Product", description: "Course, template, ebook" },
    { label: "Physical Product", description: "Tangible item you ship" },
    { label: "Membership / Community", description: "Recurring access" }
  ]
)
```

#### Q3: Business Name

```
AskUserQuestion(
  question: "What's the name of your business?",
  options: [
    { label: "I have a name", description: "Type it in the text field" },
    { label: "I need help naming it", description: "I'll suggest options later" }
  ]
)
```

#### Q4: Main Offering

```
AskUserQuestion(
  question: "What's the main thing your customers get from you?",
  options: [
    { label: "I'll describe it", description: "Type your answer" },
    { label: "Help me articulate it", description: "I'll ask follow-up questions" }
  ]
)
```

#### Q5: Ideal Customer

```
AskUserQuestion(
  question: "Do you have a clear picture of your ideal customer?",
  options: [
    { label: "Yes, I know exactly who", description: "I'll describe them" },
    { label: "Somewhat, but not specific", description: "Help me define them" },
    { label: "Not really", description: "We'll figure it out together" }
  ]
)
```

#### Q6: Customer Role

```
AskUserQuestion(
  question: "What's your ideal customer's role?",
  options: [
    { label: "Founder / CEO", description: "Business owners and decision makers" },
    { label: "Manager / Director", description: "Mid-level decision makers" },
    { label: "Individual / Consumer", description: "B2C customers" },
    { label: "Other", description: "Describe in text field" }
  ]
)
```

#### Q7: Company Size

```
AskUserQuestion(
  question: "What size company do they work at?",
  options: [
    { label: "Solo / Freelancer", description: "Just themselves" },
    { label: "Small team (2-10)", description: "Early stage" },
    { label: "Growing (11-50)", description: "Scaling up" },
    { label: "Larger (50+)", description: "Established company" }
  ]
)
```

#### Q8: Trigger Moment

```
AskUserQuestion(
  question: "Do you know what makes customers start looking for your solution?",
  options: [
    { label: "Yes, there's a specific moment", description: "I'll describe the trigger" },
    { label: "It varies", description: "I'll describe a few scenarios" },
    { label: "Not sure", description: "We'll explore together" }
  ]
)
```

#### Q9: Problem #1

```
AskUserQuestion(
  question: "Can you name the #1 problem your customers want solved?",
  options: [
    { label: "Yes, I can describe it", description: "Type it" },
    { label: "I have a few problems", description: "We'll go through them one by one" },
    { label: "Need help articulating", description: "I'll ask questions to uncover it" }
  ]
)
```

#### Q10: Problem Impact

```
AskUserQuestion(
  question: "How does this problem affect them most?",
  options: [
    { label: "Costs them money", description: "Financial impact" },
    { label: "Wastes their time", description: "Efficiency impact" },
    { label: "Causes stress/frustration", description: "Emotional impact" },
    { label: "All of the above", description: "Multiple impacts" }
  ]
)
```

#### Q11: Success Outcome

```
AskUserQuestion(
  question: "What does success look like after working with you?",
  options: [
    { label: "I can describe the transformation", description: "Type it" },
    { label: "Help me articulate it", description: "I'll ask specific questions" }
  ]
)
```

#### Q12: Timeline

```
AskUserQuestion(
  question: "How quickly can customers expect results?",
  options: [
    { label: "Within days", description: "Very fast turnaround" },
    { label: "Within 2-4 weeks", description: "Reasonable timeframe" },
    { label: "Within 1-3 months", description: "Longer engagement" },
    { label: "It varies significantly", description: "Depends on scope" }
  ]
)
```

#### Q13: Process

```
AskUserQuestion(
  question: "Do you have a defined process for how you work?",
  options: [
    { label: "Yes, I have clear steps", description: "I'll list them" },
    { label: "Somewhat defined", description: "We can refine it" },
    { label: "Not really", description: "I can help create one or skip" }
  ]
)
```

#### Q14: Differentiator

```
AskUserQuestion(
  question: "What's the #1 reason someone should choose you?",
  options: [
    { label: "I can explain it", description: "Type your answer" },
    { label: "Help me figure it out", description: "I'll ask comparison questions" }
  ]
)
```

#### Q15: Social Proof

```
AskUserQuestion(
  question: "What kind of proof do you have that this works?",
  options: [
    { label: "Testimonials or reviews", description: "I'll ask for 2-3 best ones" },
    { label: "Results with specific numbers", description: "I'll ask for the stats" },
    { label: "Client logos or case studies", description: "I'll ask which names" },
    { label: "None yet", description: "We'll work without this section" }
  ]
)
```

#### Q16: Objections

```
AskUserQuestion(
  question: "Do you know why people hesitate to buy?",
  options: [
    { label: "Yes, I hear common objections", description: "I'll ask you to describe them" },
    { label: "Not specifically", description: "We'll skip the FAQ section" }
  ]
)
```

#### Q17: CTA Action

```
AskUserQuestion(
  question: "What's the ONE action visitors should take?",
  options: [
    { label: "Book a call", description: "Schedule a meeting" },
    { label: "Sign up", description: "Create an account or free trial" },
    { label: "Buy directly", description: "Make a purchase" },
    { label: "Request a quote", description: "Get pricing" }
  ]
)
```

#### Q18: Form Fields

```
AskUserQuestion(
  question: "How much info do you need to collect?",
  options: [
    { label: "Just name and email", description: "Minimal friction" },
    { label: "Add company name", description: "B2B qualification" },
    { label: "Add phone number", description: "Direct contact" },
    { label: "Custom fields needed", description: "I'll ask what" }
  ]
)
```

#### Q19: Form Destination

```
AskUserQuestion(
  question: "Where should form submissions go?",
  options: [
    { label: "Email me directly", description: "To your inbox" },
    { label: "My CRM", description: "HubSpot, Salesforce, etc." },
    { label: "Calendly or booking link", description: "Direct scheduling" },
    { label: "I'm not sure", description: "We'll figure it out" }
  ]
)
```

**After Q19, proceed to PHASE 1B — Design Inspiration.**

---

## PHASE 1B: Design Inspiration (MANDATORY SEPARATE STEP)

⚠️ **THIS IS A STANDALONE STEP. NEVER COMBINE WITH OTHER QUESTIONS.**

### Step 1: Browser Extension (SHOW FIRST)

Show this EXACT message first:

```
Before we find your design inspiration, let's set you up for the best experience.

🔌 INSTALL CLAUDE BROWSER EXTENSION

This lets me analyze websites directly when you share them.

Install here:
https://chromewebstore.google.com/detail/claude/kosogfohbhkplgacdjfidlmbkdbalgbi

Once installed, click the extension icon and sign in with your Claude account.

Let me know when you're ready, or skip if you prefer not to install it.
```

Wait for user to confirm they installed it OR they want to skip.

### Step 2: Show Browsing Links

After extension step, show this:

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

Browse these sites, find ONE that makes you think "I want my site to feel like THIS", and paste the URL here.
```

### Step 3: Wait for URL

Do not proceed until user provides a URL.

### Step 4: Ask Follow-up

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

### Step 5: Ask Animation Preference

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
