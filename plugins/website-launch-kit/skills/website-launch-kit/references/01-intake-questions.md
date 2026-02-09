# Intake Questions Reference

Deep conversation framework to understand the user's business and landing page requirements.

---

## Cowork UI Constraints

When using the Cowork question widget, these are the technical constraints:

| What I CAN Control | What I CANNOT Control |
|--------------------|-----------------------|
| Question text | Layout order (options first, text field last) |
| Option labels (2-4 required) | "Something else" placeholder text |
| Option descriptions | Visual styling of the widget |
| Number of options (min 2, max 4) | Adding custom text input fields |

**Minimum setup:** 2 radio options + automatic "Something else" field at bottom.

**Best practice:** When the answer is likely to be typed (like a name), use plain text chat instead of the widget.

---

## Core Principles

1. **One question at a time** - Never overwhelm with multiple questions
2. **Branch from answers** - Every answer spawns follow-up questions for more context
3. **More questions = more context** - Don't rush. Go deep.
4. **Their words = their copy** - Extract exact language for the landing page
5. **Design questions from context** - No generic "pick a vibe" - base on their business
6. **Keep design questions ≤ 5** - Minimal, specific, derived from their answers

---

## Question Flow

### PHASE 1: Business Foundation

---

#### Q1.1 - Business Type

**Question (Widget - 2 options required):**
```
Let's start with the basics. What type of business is this?

Option 1: "I'm selling a service"
   → Consulting, agency, freelance, coaching, done-for-you

Option 2: "I'm selling a product"
   → SaaS, digital product, physical product, course

[Something else field for edge cases]
```

**Why this matters:** Determines page structure, messaging approach, and which sections to include.

---

#### Q1.2 - Business Name

**Question (Plain text chat - NOT widget):**
```
What's the name of your business or service?

Just type it below. If you don't have a name yet, I can help you brainstorm one.
```

**If they don't have a name:**
```
No problem! Tell me briefly what you do and who you help.
I'll suggest 3 name options based on that.
```

---

#### Q1.3 - What You Offer

**Question (Plain text chat):**
```
Now describe what you actually offer.

Be specific - list the main things your customer gets. For example:
- "A 6-week coaching program with weekly calls and a private community"
- "Custom website design, copywriting, and 30 days of revisions"
- "An AI tool that writes email sequences automatically"

What do they actually walk away with?
```

**Branch if vague:**
```
Let me dig deeper. Can you walk me through what a typical project or engagement looks like from start to finish?
```

---

### PHASE 2: Target Audience

---

#### Q2.1 - Who Is It For

**Question (Plain text chat):**
```
Who is your ideal customer?

Tell me about them:
- What's their job title or role?
- What industry are they in?
- What size is their company (solo, small team, enterprise)?

The more specific, the better. "Marketing managers at B2B SaaS companies with 10-50 employees" is much better than "business owners."
```

**Branch from their answer:**
```
Got it - [repeat their audience back].

What's the biggest frustration they deal with on a daily basis? What keeps them up at night?
```

---

#### Q2.2 - Who Is NOT For

**Question (Widget - 2 options):**
```
Every business has bad-fit customers. Do you have a clear picture of who you'd turn away?

Option 1: "Yes, I know who's not a fit"
   → I'll ask you to describe them

Option 2: "Not really, I work with anyone"
   → I'll help you define this based on your answers
```

**If they select Option 1, follow up:**
```
Describe your worst-fit customer. The type of person or company you'd politely decline. What makes them a bad fit?
```

---

### PHASE 3: The Problem

---

#### Q3.1 - Trigger Moment

**Question (Plain text chat):**
```
Think about your best customers. What was the specific moment that made them start looking for a solution like yours?

What happened right before they searched? Examples:
- "They just lost a big deal because their proposal looked unprofessional"
- "They got feedback from their boss that their marketing isn't working"
- "They hired their 5th employee and realized they can't manage everything manually"

What's that trigger moment for your customers?
```

---

#### Q3.2 - Top 3 Problems

**Question (Plain text chat):**
```
Now list the TOP 3 specific problems your customers want solved.

Not vague things like "save time" - the actual, practical problems. Examples:
- "I'm sending 100 cold emails a day manually and it's eating my entire morning"
- "My website looks dated and I'm embarrassed to share it with prospects"
- "I have no idea which marketing channels are actually working"

What are their top 3?
```

**Branch for each problem:**
```
For problem #1 ("[their problem]"):
- How is this affecting them financially?
- How much time are they losing to this?
- What's the emotional toll - frustration, stress, embarrassment?
```

---

### PHASE 4: Your Solution

---

#### Q4.1 - The Outcome

**Question (Plain text chat):**
```
When someone works with you (or uses your product), what's the end result?

Paint the picture. What does their life or business look like after? Be specific:
- "They have a fully automated sales pipeline generating 30+ qualified leads per month"
- "They launch their new brand website in 2 weeks and start getting compliments from prospects"

What's the transformation?
```

---

#### Q4.2 - Timeline

**Question (Widget - 2-4 options based on context):**
```
How quickly can customers expect to see results?

Option 1: "Within days"
Option 2: "Within 2-4 weeks"  
Option 3: "Within 1-3 months"
Option 4: "It varies significantly"

[Something else for custom timelines]
```

---

#### Q4.3 - Your Process

**Question (Widget - 2 options):**
```
Do you have a defined process or methodology for how you work?

Option 1: "Yes, I have clear steps"
   → I'll ask you to list them

Option 2: "Not formally defined"
   → I'll skip this section or help you create one
```

**If they have steps, follow up:**
```
Great! List your process in 3-5 steps. Keep each step to a short title. Example:
1. Discovery
2. Strategy
3. Design
4. Build
5. Launch

What are your steps?
```

---

### PHASE 5: Why You

---

#### Q5.1 - Failed Alternatives

**Question (Plain text chat):**
```
Before finding you, what have your customers typically tried that didn't work?

Think about:
- Competitors they used
- DIY approaches they attempted
- Other solutions they explored

What failed for them before you?
```

---

#### Q5.2 - Your Differentiator

**Question (Plain text chat):**
```
Based on what you've told me, why should someone choose YOU over alternatives?

Give me your top 3 reasons. Think about:
- What do you do differently?
- What guarantees or commitments do you offer?
- What unique experience or approach do you bring?

What makes you the obvious choice?
```

---

### PHASE 6: Social Proof

---

#### Q6.1 - What Proof Do You Have

**Question (Widget - 3 options):**
```
What kind of proof do you have that this works?

Option 1: "I have testimonials or reviews"
   → I'll ask you to share your best 2-3

Option 2: "I have results with specific numbers"
   → I'll ask for the stats

Option 3: "I have client logos or case studies"
   → I'll ask which names I can feature
```

**Branch based on selection:**

If testimonials:
```
Share your 2-3 best testimonials. Copy and paste them exactly as written.
Include the person's name and title if you have it.
```

If numbers:
```
What specific results can you claim? Examples:
- "47 leads generated in 60 days"
- "3x increase in conversion rate"
- "$150K in new revenue"

What are your numbers?
```

---

### PHASE 7: Objections & Scope

---

#### Q7.1 - Top Objections

**Question (Plain text chat):**
```
What are the top 2-3 reasons people hesitate to buy from you?

Common objections include:
- "It's too expensive"
- "I've been burned before"
- "I don't have time for this right now"
- "I can do this myself"

What do you hear most often?
```

**Branch for each objection:**
```
How do you usually respond when someone says "[their objection]"? 
What puts their mind at ease?
```

---

#### Q7.2 - What's Included vs Not

**Question (Plain text chat):**
```
Let's clarify scope. What's explicitly INCLUDED in your offering?

And equally important - what's NOT included? 
This helps set expectations and reduces friction later.
```

---

### PHASE 8: Design Direction

**Important:** Design questions should be derived from their business context, not generic "pick a vibe" questions. Maximum 5 design questions.

---

#### Q8.1 - Inspiration Website

**Question (Plain text chat with helpful links):**
```
I need ONE website that captures the vibe you want for your landing page.

Browse these for inspiration:
• [Framer Templates](https://www.framer.com/marketplace/templates/) - Modern, animated templates
• [Awwwards](https://www.awwwards.com/) - Award-winning web design

**How to share:**
1. Browse the sites above
2. Find ONE that makes you think "I want my site to feel like THIS"
3. Copy the URL from your browser's address bar
4. Paste it here

What's your inspiration link?
```

**After they share:**
```
I'll analyze [their URL] and extract the design direction.

[Analyze and report: colors, typography, layout, animations, vibe]

What specifically do you like about this site? 
- Is it the colors?
- The typography style?
- The layout/structure?
- The animations?

Tell me what drew you to it.
```

---

#### Q8.2 - Match or Inspire (Context-Based)

**Question (Widget - 2 options):**
```
Based on [their chosen site], how closely should we match it?

Option 1: "Use it as a close reference"
   → I'll match the feel closely while making it yours

Option 2: "Just take inspiration from it"
   → I'll use the general direction but make it more unique
```

---

#### Q8.3 - Dynamic Design Question (Based on Business Type)

**For SERVICE businesses:**
```
Your service is about [their offering]. Should the design feel:

Option 1: "Premium and exclusive"
   → Dark theme, elegant typography, refined details

Option 2: "Approachable and trustworthy"
   → Clean, bright, professional with warmth
```

**For PRODUCT businesses:**
```
Your product helps [their outcome]. Should the design feel:

Option 1: "Modern and cutting-edge"
   → Bold animations, gradient accents, tech-forward

Option 2: "Simple and focused"
   → Minimal, clean, let the product speak
```

---

#### Q8.4 - Animation Level

**Question (Widget - 2 options):**
```
How much motion and animation do you want?

Option 1: "Keep it subtle"
   → Smooth scroll reveals, gentle hover effects

Option 2: "Make it dynamic"
   → Bold entrance animations, interactive elements
```

---

### PHASE 9: Call to Action

---

#### Q9.1 - Desired Action

**Question (Widget - 4 options):**
```
What's the ONE action you want visitors to take on this page?

Option 1: "Book a call or meeting"
Option 2: "Sign up or create an account"
Option 3: "Buy or purchase directly"
Option 4: "Request a quote or proposal"
```

---

#### Q9.2 - Form Requirements

**Question (Plain text chat):**
```
For the contact form, what information do you need to collect?

At minimum: Name and email.

Do you also need:
- Company name?
- Phone number?
- A qualifying question (like "What's your budget?")?
- Where should form submissions go? (Email, CRM, Calendly link?)

Tell me what you need.
```

---

## Summary Template

After gathering all context, present this back to the user:

```
Here's everything I've gathered:

**BUSINESS**
- Type: [Service/Product]
- Name: [name]
- Offering: [what they provide]

**AUDIENCE**
- Ideal customer: [who]
- Bad fit: [who to avoid]

**PROBLEM**
- Trigger moment: [what makes them search]
- Top problems:
  1. [problem 1]
  2. [problem 2]
  3. [problem 3]

**SOLUTION**
- Outcome: [transformation]
- Timeline: [how fast]
- Process: [steps]

**DIFFERENTIATION**
- Failed alternatives: [what didn't work]
- Why you: [top 3 reasons]

**PROOF**
- [testimonials/stats/logos summary]

**OBJECTIONS**
- [top concerns + how to handle]

**DESIGN**
- Inspiration: [their URL]
- Direction: [extracted from analysis]
- Animation: [subtle/dynamic]

**CTA**
- Action: [book/signup/buy/quote]
- Form fields: [requirements]

---

Anything to add or correct before I move to the next phase?
```

---

## Branching Decision Tree

```
Q1 (Business Type)
├── SERVICE → Ask about deliverables, process, timeline
│   └── Branch: "Walk me through a typical engagement"
└── PRODUCT → Ask about features, use cases, results
    └── Branch: "What problem does this solve?"

Q2 (Audience)
├── Clear answer → Branch: "What frustrates them daily?"
└── Vague answer → Branch: "Give me a specific example of your best customer"

Q3 (Problems)
├── For each problem → Branch: "How does this affect them financially/emotionally?"

Q6 (Proof)
├── Has testimonials → "Share your 2-3 best, copy-paste exactly"
├── Has numbers → "What specific results can you claim?"
└── Has logos → "Which names can I feature?"

Q7 (Objections)
├── For each objection → "How do you respond to this?"
```
