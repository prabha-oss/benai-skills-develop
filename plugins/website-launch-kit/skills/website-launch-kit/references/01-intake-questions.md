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

1. **ONE question per message** - Never combine questions. Each message = 1 question only.
2. **Branch from answers** - Every answer can spawn follow-up questions for more context
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
What type of business is this?

Option 1: "I'm selling a service"
   → Consulting, agency, freelance, coaching, done-for-you

Option 2: "I'm selling a product"
   → SaaS, digital product, physical product, course
```

---

#### Q1.2 - Business Name

**Question (Plain text chat - single question):**
```
What's the name of your business?
```

**If they don't have one, follow up:**
```
No problem! What do you do in one sentence?
```

**Then:**
```
Based on that, here are 3 name options:
1. [Option A]
2. [Option B]
3. [Option C]

Which feels right?
```

---

#### Q1.3 - What You Offer

**Question (Plain text chat - single question):**
```
What's the main thing your customers get from you?
```

**If vague, follow up:**
```
Can you give me a specific example of what a customer walks away with?
```

---

#### Q1.4 - Deliverables

**Question (Plain text chat - single question):**
```
List the specific deliverables or features included.
```

---

### PHASE 2: Target Audience

---

#### Q2.1 - Who Is It For

**Question (Plain text chat - single question):**
```
Who is your ideal customer?
```

**Follow-up if vague:**
```
What's their job title or role?
```

**Then:**
```
What industry are they in?
```

**Then:**
```
What size is their company?
```

---

#### Q2.2 - Their Frustration

**Question (Plain text chat - single question):**
```
What's the biggest frustration they deal with daily?
```

---

#### Q2.3 - Who Is NOT For

**Question (Widget - 2 options):**
```
Do you know who you'd turn away?

Option 1: "Yes, I know who's not a fit"
Option 2: "Not really"
```

**If Option 1, follow up:**
```
Describe your worst-fit customer.
```

---

### PHASE 3: The Problem

---

#### Q3.1 - Trigger Moment

**Question (Plain text chat - single question):**
```
What moment makes your customers start looking for a solution like yours?
```

**Provide example only if they're stuck:**
```
For example: "They just lost a deal because their proposal looked unprofessional"
```

---

#### Q3.2 - Problem #1

**Question (Plain text chat - single question):**
```
What's the #1 specific problem they want solved?
```

---

#### Q3.3 - Problem #1 Impact

**Question (Plain text chat - single question):**
```
How does that problem affect them? (Time, money, stress?)
```

---

#### Q3.4 - Problem #2

**Question (Plain text chat - single question):**
```
What's another big problem they face?
```

---

#### Q3.5 - Problem #3

**Question (Plain text chat - single question):**
```
One more problem they deal with?
```

---

### PHASE 4: Your Solution

---

#### Q4.1 - The Outcome

**Question (Plain text chat - single question):**
```
What does their life or business look like after working with you?
```

---

#### Q4.2 - Timeline

**Question (Widget - 4 options):**
```
How quickly can they expect results?

Option 1: "Within days"
Option 2: "Within 2-4 weeks"
Option 3: "Within 1-3 months"
Option 4: "It varies"
```

---

#### Q4.3 - Process Exists?

**Question (Widget - 2 options):**
```
Do you have a defined process for how you work?

Option 1: "Yes, I have clear steps"
Option 2: "Not formally defined"
```

---

#### Q4.4 - Process Steps

**If yes to Q4.3 (Plain text chat - single question):**
```
List your process in 3-5 short steps.
```

---

### PHASE 5: Why You

---

#### Q5.1 - Failed Alternatives

**Question (Plain text chat - single question):**
```
What have your customers tried before that didn't work?
```

---

#### Q5.2 - Differentiator #1

**Question (Plain text chat - single question):**
```
What's the #1 reason someone should choose you?
```

---

#### Q5.3 - Differentiator #2

**Question (Plain text chat - single question):**
```
What's another reason?
```

---

#### Q5.4 - Differentiator #3

**Question (Plain text chat - single question):**
```
One more reason?
```

---

### PHASE 6: Social Proof

---

#### Q6.1 - Proof Type

**Question (Widget - 3 options):**
```
What kind of proof do you have?

Option 1: "Testimonials or reviews"
Option 2: "Results with specific numbers"
Option 3: "Client logos or case studies"
```

---

#### Q6.2 - Testimonials

**If Option 1 (Plain text chat - single question):**
```
Share your best testimonial. Copy and paste it exactly.
```

**Then:**
```
Got another good one?
```

---

#### Q6.3 - Numbers

**If Option 2 (Plain text chat - single question):**
```
What specific result can you claim with numbers?
```

---

### PHASE 7: Objections & Scope

---

#### Q7.1 - Top Objection

**Question (Plain text chat - single question):**
```
What's the #1 reason people hesitate to buy from you?
```

---

#### Q7.2 - How You Handle It

**Question (Plain text chat - single question):**
```
How do you usually respond to that?
```

---

#### Q7.3 - Other Objections

**Question (Plain text chat - single question):**
```
Any other common concerns they have?
```

---

#### Q7.4 - What's Included

**Question (Plain text chat - single question):**
```
What's explicitly included in your offering?
```

---

#### Q7.5 - What's NOT Included

**Question (Plain text chat - single question):**
```
What's NOT included?
```

---

### PHASE 8: Design Direction

**Maximum 5 design questions. Base them on their business context.**

---

#### Q8.1 - Inspiration Website

**Question (Plain text chat - single question):**
```
Find ONE website that captures the vibe you want.

Browse here for ideas:
• https://www.framer.com/marketplace/templates/
• https://www.awwwards.com/

Paste the link when you find one.
```

---

#### Q8.2 - What They Like

**After they share (Plain text chat - single question):**
```
What specifically drew you to that site?
```

---

#### Q8.3 - Match or Inspire

**Question (Widget - 2 options):**
```
How closely should we match it?

Option 1: "Use it as a close reference"
Option 2: "Just take inspiration"
```

---

#### Q8.4 - Design Feel (Dynamic - based on business type)

**For SERVICE businesses:**
```
Should the design feel premium and exclusive, or approachable and trustworthy?

Option 1: "Premium and exclusive"
Option 2: "Approachable and trustworthy"
```

**For PRODUCT businesses:**
```
Should the design feel modern and cutting-edge, or simple and focused?

Option 1: "Modern and cutting-edge"
Option 2: "Simple and focused"
```

---

#### Q8.5 - Animation Level

**Question (Widget - 2 options):**
```
How much animation do you want?

Option 1: "Keep it subtle"
Option 2: "Make it dynamic"
```

---

### PHASE 9: Call to Action

---

#### Q9.1 - Desired Action

**Question (Widget - 4 options):**
```
What's the ONE action visitors should take?

Option 1: "Book a call"
Option 2: "Sign up"
Option 3: "Buy directly"
Option 4: "Request a quote"
```

---

#### Q9.2 - Form Fields

**Question (Plain text chat - single question):**
```
What info do you need to collect? (Name, email, phone, company, etc.)
```

---

#### Q9.3 - Form Destination

**Question (Plain text chat - single question):**
```
Where should form submissions go?
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
- Trigger: [moment]
- Problems: [1, 2, 3]

**SOLUTION**
- Outcome: [transformation]
- Timeline: [how fast]
- Process: [steps]

**WHY YOU**
- Failed alternatives: [what didn't work]
- Differentiators: [1, 2, 3]

**PROOF**
- [summary]

**OBJECTIONS**
- [concerns + responses]

**DESIGN**
- Inspiration: [URL]
- Feel: [premium/approachable/modern/simple]
- Animation: [subtle/dynamic]

**CTA**
- Action: [book/signup/buy/quote]
- Form: [fields]

---

Anything to add or correct?
```

---

## Key Rule Reminder

**NEVER ask multiple questions in one message.**

❌ Wrong:
```
What's the name of your business, and what service do you provide? 
Give me the full picture: who do you help, what do you actually do for them, 
and what do they walk away with?
```

✅ Right:
```
What's the name of your business?
```

Then after they answer:
```
What's the main thing your customers get from you?
```

Then after they answer:
```
Who is your ideal customer?
```

**One question. Wait for answer. Then next question.**
