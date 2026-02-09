# Intake Questions Reference

Deep conversation framework to understand the user's business and landing page requirements.

---

## How to Ask Questions

**IMPORTANT:** Always use the `AskUserQuestion` tool for intake questions. This shows a clean modal with selectable options.

### Rules

1. Ask **ONE question at a time** — never combine multiple questions
2. Every question **MUST** use the `AskUserQuestion` tool
3. Provide **2-4 clear options** per question
4. **Wait** for the user's answer before asking the next question
5. Do **NOT** ask questions as plain text in the chat

### Tool Format

```
AskUserQuestion(
  question: "Your single question here",
  options: [
    { label: "Option 1", description: "Brief explanation" },
    { label: "Option 2", description: "Brief explanation" },
  ]
)
```

---

## Question Flow

### PHASE 1: Business Foundation

---

**Q1.1 - Business Type**
- Question: `"Is this for a product or a service?"`
- Options:
  - `"Product"` → A physical or digital product people buy
  - `"Service"` → You do work for clients (consulting, agency, freelance, etc.)

---

**Q1.2 - Service Type** *(if Service selected)*
- Question: `"What type of service do you provide?"`
- Options:
  - `"Consulting"` → Strategy and expert advice
  - `"Agency / Done-for-you"` → You deliver finished work
  - `"Coaching / Training"` → You teach or guide people
  - `"Freelance / Creative"` → Design, writing, dev, etc.

---

**Q1.3 - Product Type** *(if Product selected)*
- Question: `"What type of product is this?"`
- Options:
  - `"SaaS / Software"` → Online tool or app
  - `"Digital Product"` → Course, template, ebook
  - `"Physical Product"` → Tangible item you ship
  - `"Membership / Community"` → Recurring access

---

**Q1.4 - Business Name**
- Question: `"What's the name of your business?"`
- Options:
  - `"I have a name"` → Type it in the text field
  - `"I need help naming it"` → I'll suggest options based on your answers

---

**Q1.5 - Main Offering**
- Question: `"What's the main thing your customers get from you?"`
- Options:
  - `"I'll describe it"` → Type your answer
  - `"Help me articulate it"` → I'll ask follow-up questions

---

### PHASE 2: Target Audience

---

**Q2.1 - Audience Clarity**
- Question: `"Do you have a clear picture of your ideal customer?"`
- Options:
  - `"Yes, I know exactly who"` → I'll ask you to describe them
  - `"Somewhat, but not specific"` → I'll help you define them
  - `"Not really"` → We'll figure it out together

---

**Q2.2 - Audience Role** *(if they know their audience)*
- Question: `"What's your ideal customer's role?"`
- Options:
  - `"Founder / CEO"` → Business owners
  - `"Manager / Director"` → Mid-level decision makers
  - `"Individual / Consumer"` → B2C customers
  - `"Other"` → Describe in text field

---

**Q2.3 - Company Size**
- Question: `"What size company do they work at?"`
- Options:
  - `"Solo / Freelancer"` → Just themselves
  - `"Small team (2-10)"` → Early stage
  - `"Growing (11-50)"` → Scaling up
  - `"Larger (50+)"` → Established company

---

**Q2.4 - Bad Fit**
- Question: `"Do you know who you'd turn away?"`
- Options:
  - `"Yes, I know who's not a fit"` → I'll ask you to describe
  - `"Not really"` → We'll skip this

---

### PHASE 3: The Problem

---

**Q3.1 - Trigger Awareness**
- Question: `"Do you know what makes customers start looking for your solution?"`
- Options:
  - `"Yes, there's a specific moment"` → Describe it
  - `"It varies"` → I'll ask follow-up questions
  - `"Not sure"` → We'll explore together

---

**Q3.2 - Problem Clarity**
- Question: `"Can you name the #1 problem your customers want solved?"`
- Options:
  - `"Yes, I can describe it"` → Type it
  - `"I have a few problems"` → We'll go through them one by one
  - `"Need help articulating"` → I'll ask questions to uncover it

---

**Q3.3 - Problem Impact**
- Question: `"How does this problem affect them most?"`
- Options:
  - `"Costs them money"` → Financial impact
  - `"Wastes their time"` → Efficiency impact
  - `"Causes stress/frustration"` → Emotional impact
  - `"All of the above"` → Multiple impacts

---

### PHASE 4: Your Solution

---

**Q4.1 - Outcome Clarity**
- Question: `"What does success look like after working with you?"`
- Options:
  - `"I can describe the transformation"` → Type it
  - `"Help me articulate it"` → I'll ask specific questions

---

**Q4.2 - Timeline**
- Question: `"How quickly can customers expect results?"`
- Options:
  - `"Within days"` → Very fast
  - `"Within 2-4 weeks"` → Reasonable timeframe
  - `"Within 1-3 months"` → Longer engagement
  - `"It varies significantly"` → Depends on scope

---

**Q4.3 - Process Exists**
- Question: `"Do you have a defined process for how you work?"`
- Options:
  - `"Yes, I have clear steps"` → I'll ask you to list them
  - `"Somewhat defined"` → We can refine it
  - `"Not really"` → I can help create one or skip this section

---

### PHASE 5: Why You

---

**Q5.1 - Competitive Awareness**
- Question: `"Do you know what customers have tried before finding you?"`
- Options:
  - `"Yes, I know their failed attempts"` → Describe them
  - `"Not specifically"` → We'll skip this

---

**Q5.2 - Differentiator**
- Question: `"What's the #1 reason someone should choose you?"`
- Options:
  - `"I can explain it"` → Type your answer
  - `"Help me figure it out"` → I'll ask comparison questions

---

### PHASE 6: Social Proof

---

**Q6.1 - Proof Type**
- Question: `"What kind of proof do you have that this works?"`
- Options:
  - `"Testimonials or reviews"` → I'll ask for 2-3 best ones
  - `"Results with specific numbers"` → I'll ask for the stats
  - `"Client logos or case studies"` → I'll ask which names
  - `"None yet"` → We'll work without this section

---

### PHASE 7: Objections

---

**Q7.1 - Common Objections**
- Question: `"Do you know why people hesitate to buy?"`
- Options:
  - `"Yes, I hear common objections"` → Describe them
  - `"Not specifically"` → We'll skip this

---

**Q7.2 - Scope Clarity**
- Question: `"Is it clear what's included vs not included?"`
- Options:
  - `"Yes, I can list both"` → I'll ask separately
  - `"Included is clear, exclusions not"` → I'll help define
  - `"Needs work"` → We'll figure it out

---

### PHASE 8: Design Direction

---

**Q8.1 - Inspiration**
- Question: `"Do you have a website that captures the vibe you want?"`
- Options:
  - `"Yes, I have one"` → Paste the link
  - `"I need to browse"` → Check framer.com/marketplace or awwwards.com
  - `"No preference"` → I'll suggest based on your business

---

**Q8.2 - Design Match** *(after they share a link)*
- Question: `"How closely should we match that site?"`
- Options:
  - `"Use it as a close reference"` → Match the feel closely
  - `"Just take inspiration"` → Use general direction only

---

**Q8.3 - Design Feel** *(for Services)*
- Question: `"Should the design feel premium or approachable?"`
- Options:
  - `"Premium and exclusive"` → Dark theme, elegant, refined
  - `"Approachable and trustworthy"` → Clean, bright, warm

---

**Q8.4 - Design Feel** *(for Products)*
- Question: `"Should the design feel cutting-edge or simple?"`
- Options:
  - `"Modern and cutting-edge"` → Bold animations, gradients
  - `"Simple and focused"` → Minimal, let product speak

---

**Q8.5 - Animation Level**
- Question: `"How much animation do you want?"`
- Options:
  - `"Keep it subtle"` → Smooth scroll reveals, gentle hovers
  - `"Make it dynamic"` → Bold entrances, interactive elements

---

### PHASE 9: Call to Action

---

**Q9.1 - Desired Action**
- Question: `"What's the ONE action visitors should take?"`
- Options:
  - `"Book a call"` → Schedule a meeting
  - `"Sign up"` → Create an account
  - `"Buy directly"` → Make a purchase
  - `"Request a quote"` → Get pricing

---

**Q9.2 - Form Complexity**
- Question: `"How much info do you need to collect?"`
- Options:
  - `"Just name and email"` → Minimal friction
  - `"Add company name"` → B2B qualification
  - `"Add phone number"` → Direct contact
  - `"Custom fields needed"` → I'll ask what

---

**Q9.3 - Form Destination**
- Question: `"Where should form submissions go?"`
- Options:
  - `"Email me directly"` → To your inbox
  - `"My CRM"` → HubSpot, Salesforce, etc.
  - `"Calendly or booking link"` → Direct scheduling
  - `"I'm not sure"` → We'll figure it out

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

**DESIGN**
- Inspiration: [URL]
- Feel: [premium/approachable/modern/simple]
- Animation: [subtle/dynamic]

**CTA**
- Action: [book/signup/buy/quote]
- Form: [fields + destination]

---

Anything to add or correct?
```

---

## Key Rules Reminder

### ✅ DO
- Use `AskUserQuestion` tool for every question
- Ask ONE question per modal
- Provide 2-4 clear options
- Wait for answer before next question

### ❌ DON'T
- Ask questions as plain chat text
- Combine multiple questions in one modal
- Provide more than 4 options
- Skip waiting for answers
