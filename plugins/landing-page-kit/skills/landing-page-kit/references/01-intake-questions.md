# Intake Questions Reference

Deep conversation framework to understand the user's business and landing page requirements.

## Core Principles

1. **More questions = more customization** - Don't rush. Go deep.
2. **Branch conversations** - Every answer can spawn follow-up questions.
3. **One inspiration link** - Ask for exactly one website reference.
4. **Scrape all URLs** - Analyze any link they share.
5. **Let them talk** - Their words become the copy.
6. **No repeated questions** - Track what's covered.
7. **Dynamic questions** - Create questions based on their answers.

---

## Question Bank (17 Core Questions)

### Phase 1: Business Basics

**Q0 - Business Type (ASK FIRST)**
```
"First - is this a PRODUCT business or a SERVICE business?"
```
This determines page structure and messaging approach.

**Q1 - Name**

**UI Pattern:** Direct input with AI fallback (no unnecessary clicks)

```
┌─────────────────────────────────────────────────────────────┐
│  What's the name of your service or business?               │
│                                                              │
│  ┌─────────────────────────────────────────────────────┐    │
│  │  Enter your business name here                       │    │
│  └─────────────────────────────────────────────────────┘    │
│                                                              │
│  [ ✨ Generate with AI ]                                     │
│                                                              │
└─────────────────────────────────────────────────────────────┘
```

**Behavior:**
- If user has a name → Type directly, press Enter or proceed
- If user needs help → Click "Generate with AI" which asks context questions and suggests names

**Q2 - What You Offer**
```
"Describe what you offer in detail. What are the main features or deliverables?"
```

Branch if vague:
- "Can you list 3-5 specific things they get?"
- "Walk me through a typical project or engagement"

---

### Phase 2: Target Audience

**Q3 - Who Is It For**
```
"Who is this for? Tell me the industry, role/job title, and company type or size."
```

Branch deeper:
- If job title → "What's their biggest daily frustration?"
- If company size → "What changes at that stage that makes them need you?"
- If revenue mentioned → "What are they trying to achieve next?"

**Q15 - Who Is NOT For**
```
"Who is this NOT for? Describe the bad-fit client you'd turn away."
```

---

### Phase 3: Conversion Goal

**Q4 - Desired Action**
```
"What action should visitors take on the page?
- Book a call
- Request a quote
- Buy
- Sign up
- Download
- Other?"
```

---

### Phase 4: Problem & Trigger

**Q5 - Trigger Moment**
```
"What 'trigger moment' makes them start looking for this? What happened right before they searched?"
```

**Q6 - Top 3 Problems**
```
"What are the TOP 3 problems they want solved? List the practical, specific problems."
```

Branch into:
- "How much is this costing them? Time, money, stress?"
- "How does this show up in their day-to-day?"

---

### Phase 5: Outcome & Results

**Q7 - End Result**
```
"What outcome do they get? What's the end result of working with you?"
```

**Q8 - Timeline**
```
"How fast can they expect results? What's the typical timeframe?"
```

---

### Phase 6: Differentiation

**Q9 - Failed Alternatives**
```
"What have they already tried that didn't work? Competitors, DIY, other approaches?"
```

**Q10 - Why Choose You**
```
"What are the TOP 3 reasons they should choose you? Your advantages, guarantees, or specialization."
```

Branch:
- "What do competitors get wrong?"
- "What do you refuse to do that others do?"

**Competitor Analysis (Optional)**
```
"Drop a competitor link if you have one - I'll analyze how to differentiate."
```
→ Scrape and identify positioning gaps

---

### Phase 7: Social Proof

**Q11 - Proof**
```
"What proof do you have?
- Testimonials
- Case studies
- Numbers/stats
- Portfolio
- Client logos
- Certifications"
```

Get specifics:
- "Can you paste your best 2-3 testimonials?"
- "Any specific results with numbers?"
- "Recognizable client names I can mention?"

If no proof → "What results could you realistically promise?"

---

### Phase 8: Process & Scope

**Q12 - Process**
```
"Do you have a clear process? If yes, list it in 3-5 steps. If no, say 'no clear process'."
```
Example: "Discovery → Strategy → Build → Launch"

**Q13 - Included vs Not Included**
```
"What's INCLUDED vs NOT INCLUDED? Define the boundaries and scope."
```

---

### Phase 9: Objections & Requirements

**Q14 - Friction and Objections**
```
"What's the main friction or hesitation people have? List up to 3 top objections."
```

Follow up:
- "How do you usually handle those?"
- "What do you say that puts their mind at ease?"

**Q16 - Requirements From Customer**
```
"What do you need from the customer to succeed?
(Access, info, approvals, budget, time commitment, etc.)"
```

---

### Phase 10: Design Direction

**Ask for ONE Inspiration Link**
```
"Now for the design direction. I need ONE website that captures the vibe you want.

Find inspiration at:
- awwwards.com
- godly.website
- framer.com/templates
- landingfolio.com
- lapa.ninja

Send me ONE link - the site that makes you think 'I want mine to feel like THIS.'"
```

**When They Share a Link:**
1. Use WebFetch immediately
2. Analyze: colors, typography, layout, hero style, animations, vibe
3. Report back what you see
4. Ask what they specifically like/dislike

```
"I analyzed [site]. I see:
- [color scheme]
- [typography style]
- [layout approach]
- [hero treatment]

Is this the direction? What specifically do you like about it?"
```

---

### Phase 11: Tone & Voice

**Open the Conversation**
```
"How should visitors FEEL when they land on your site?"
```

**Get Specific:**
- "Formal or casual?"
- "Expert authority or friendly approachable?"
- "Bold claims or understated confidence?"
- "Humor - yes or no?"

**Test with Options**
```
"Quick vibe check - which feels more like you?

A) 'We build automation that scales your business.'
B) 'Stop drowning in manual work. Let's fix that.'
C) 'AI automation for founders who'd rather grow than grind.'

Or describe what fits better."
```

---

### Phase 12: Assets

**Guide Them on Sharing Assets**
```
"Do you have existing brand assets? Here's how to share them:

1. Create a folder called 'brand-assets' in your project directory
2. Add any of these:
   - Logo files (PNG, SVG)
   - Brand guidelines (PDF)
   - Team photos
   - Product screenshots
   - Any existing copy docs

Once added, let me know and I'll review them."
```

**If They Have a Current Website**
```
"Share your current site link - I'll analyze what to keep vs change."
```
→ Scrape and note good copy to preserve

---

### Phase 13: Technical & Form

```
"For the contact form - what info do you need to collect?"
```

- Name/email enough, or more?
- Any qualifying questions?
- Where should submissions go? (email, CRM, Calendly link)
- Any integrations needed?

---

## Dynamic Question Rules

**Create Questions Based On:**
1. What they said - Dig into interesting mentions
2. What's missing - Ask about gaps
3. Interesting language - Explore specific words they use
4. Opportunities - If you see a positioning angle, validate it

**When Answers Are Short:**
- Ask for examples
- Offer multiple choice options
- State your assumption and ask if correct

**When Answers Are Long:**
- Summarize to confirm
- Extract key points
- Identify copy gold

---

## Progress Checklist

Track mentally - don't ask what's already covered:

- [ ] Q0: Product or Service
- [ ] Q1: Business name
- [ ] Q2: What they offer
- [ ] Q3: Target audience
- [ ] Q4: CTA/conversion goal
- [ ] Q5: Trigger moment
- [ ] Q6: Top 3 problems
- [ ] Q7: Outcome
- [ ] Q8: Timeline
- [ ] Q9: Failed alternatives
- [ ] Q10: Why choose you
- [ ] Q11: Proof
- [ ] Q12: Process
- [ ] Q13: Scope (included/not)
- [ ] Q14: Objections
- [ ] Q15: Bad fit clients
- [ ] Q16: Requirements
- [ ] Design inspiration
- [ ] Tone & voice
- [ ] Assets
- [ ] Technical/form needs

---

## Summary Template

After gathering all context, present this summary:

```
"Here's what I have:

BUSINESS TYPE: [Product/Service]
NAME: [name]
OFFERING: [what they do, deliverables]

AUDIENCE: [who it's for]
NOT FOR: [bad fit]

CTA: [desired action]

TRIGGER: [what makes them search]
PROBLEMS:
1. [problem 1]
2. [problem 2]
3. [problem 3]

OUTCOME: [end result]
TIMELINE: [how fast]

DIFFERENTIATION:
- Failed alternatives: [what didn't work]
- Why you: [top 3 reasons]

PROOF: [testimonials, numbers, logos]

PROCESS: [steps]
SCOPE: [included vs not]

OBJECTIONS: [top concerns]
REQUIREMENTS: [what you need from them]

DESIGN: [based on inspiration analysis]
TONE: [voice guidelines]

Anything to add or correct?"
```
