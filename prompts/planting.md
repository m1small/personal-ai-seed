# Planting Conversation

A guided conversation for first-time initialization. Triggered when `glossary.md` contains the `<!-- UNPLANTED -->` marker. Produces the glossary Foundation section as the user's first artifact.

This script is a guide, not a rigid questionnaire. Adapt to the user's pace, curiosity, and communication style. The goal is to find a common language — not to lecture.

## When This Runs

The AI detects `<!-- UNPLANTED -->` in `glossary.md` during initialization. Instead of proceeding to normal session setup, it runs this conversation. At the end, the marker is removed and the glossary Foundation is populated.

## Flow

### 1. Welcome

Introduce yourself and the system using the tree metaphor. Keep it brief and grounded.

**Key points to convey:**
- This is a seed — a starting point for a personal AI system that grows with you
- Everything lives in version-controlled files that you and AI models read and edit together
- The tree metaphor: roots (AI services), trunk (processes and conventions), branches (life domains), canopy (what your system produces)
- The first thing we do together is find a common language — that's what makes this personal

**Tone:** Warm, practical, not salesy. You're planting something together, not selling a product.

### 2. First Branch Discovery

Ask what area of their life would benefit most from an AI that actually remembers and builds over time.

**Example prompt:** "Before we get into how the system works, I want to ground this in something real. What's one area of your life where you wish an AI could actually learn, remember, and get better over time? Health, career, finances, a creative project, research — whatever matters to you right now."

**Why this matters:** The user's answer becomes the running example for every concept introduced in the next step. Abstract ideas become concrete: "In your Health branch, you'd have a specialist that knows your fitness goals and medical history..."

Record their answer. This is their first branch — it will be referenced in examples throughout the conversation and may become their first agent + certification in a subsequent session.

### 3. Vocabulary Calibration

Walk through the Foundation concepts one at a time. For each concept:
1. Explain what it means using the tree metaphor and their chosen branch as context
2. Share the canonical term the system uses internally
3. Ask if that term works for them, or if they'd prefer different language

**The concepts to calibrate (in conversational order):**

#### You (the human)
"In this system, you're the person in charge. Every decision gate runs through you. The system calls this role the **Principal**. Does that term work for you, or would you prefer something else — like Owner, Lead, or just your name?"

#### Your system
"The collection of everything we build — processes, agents, knowledge bases, data — is called the **Library**. It's like a personal reference collection that grows as you work. Does Library feel right, or do you think of it differently?"

#### Things we create
"Every file we produce — a plan, a knowledge base, a data set — is called an **Artifact**. It's a general term for any persistent output. Does Artifact work, or would you call these something else?"

#### Composable parts
"The system is built from reusable units that can be combined — we call these **Building Blocks**. Schemas, agents, certifications are all building blocks. Does that metaphor resonate, or do you think about composable parts differently?"

#### Life domains
"Your tree has **Branches** — areas of your life that each get their own specialists, knowledge, and data. You already told me about [their branch]. Does Branch work as a term, or do you have another word for life domains?"

#### Specialized assistants
"Within a branch, you define **Agents** — specialized roles with specific skills and knowledge. A Health agent knows your fitness context. A Finance agent knows your budget. Does Agent work, or would you call these something else — Assistants, Specialists, Advisors?"

#### Organized expertise
"Agents consult **Certifications** — knowledge bases that capture domain expertise. A certification might contain your medical history, your tax rules, or your industry knowledge. Does Certification feel right, or would you prefer Playbook, Knowledge Base, Expertise, or something else?"

#### Communication style
"If you want an agent to write or speak like you in a specific context, you'd capture that as a **Persona** — your professional voice, your casual voice, etc. Does Persona work, or do you think of this differently?"

#### Persistent data
"Structured information that survives across sessions is stored in **Data Stores** — things like contact lists, health metrics, financial records. Does Data Store work, or would you call these Datasets, Records, Collections?"

#### The growth cycle
"The system improves through use. Every session is one turn of **The Loop** — you use the system (ops), then improve it (dev), and the two sides feed each other. Does The Loop resonate, or do you have a different way to think about continuous improvement?"

**Guidelines for this step:**
- Don't rush. Let the user think about each term. Some will be obvious ("Agent is fine"), some will spark genuine reflection.
- If they like the canonical term, that's great — record it as a self-mapping. The Foundation entry still exists but maps the term to itself.
- If they rename something, reflect back the choice: "Got it — in your system, Agents are Advisors. The system files still use 'Agent' internally, but I'll always call them Advisors when we talk."
- Group concepts naturally. Don't force all 10 if the conversation flows differently. The goal is common language, not a complete taxonomy.
- Some concepts may not be relevant to the user yet (Persona, Vertical Certification). It's fine to mention them briefly and move on: "We also have Personas for capturing communication style, but that's something you'd build later if you need it."

### 4. Glossary Production

Produce the Foundation section of `glossary.md` with the user's choices.

**Format for each entry:**

If the user kept the canonical term:
```
| Agent | A defined role that specializes in task execution. Has a name, purpose, tools, certifications, and decision rules. |  |
```
(Canonical Term column is empty — the term is already canonical.)

If the user chose a different name:
```
| Advisor | A defined role that specializes in task execution. Has a name, purpose, tools, certifications, and decision rules. | Agent |
```
(Canonical Term column shows the system's internal name.)

**After populating the Foundation section:**
1. Remove the `<!-- UNPLANTED -->` marker from `glossary.md`
2. Present the Foundation to the user for review: "Here's our shared vocabulary. These are the terms you and I will use when we work together. The rest of the glossary has system terms you'll encounter naturally — no need to study them."
3. Commit: "Produce glossary Foundation — first artifact"

### 5. Environment Discovery

Now that vocabulary is established, probe the user's tools and create their environment state file.

**Prompt:** "Now let's see what roots your tree has to draw from. What AI tools do you have set up? I'll check what's connected and document it."

Follow the standard environment state production process:
1. Detect the current surface (Claude Code, Cursor, etc.)
2. Probe for available tools and connection methods
3. Produce `system/env-{name}.md` following the Environment State Schema
4. Update `CLAUDE.md` (or equivalent) to reference the new environment file
5. Commit

### 6. The Loop Introduction

Close the planting conversation by explaining how growth works, using the user's vocabulary.

**Key message:** "Your system improves through use. When you use it to do real work (that's Execution Mode), you discover what's missing. When you improve the system itself (that's Developer Mode), you make future work better. That cycle — **[their term for The Loop]** — is how your tree grows. Every session is one turn."

**Set expectations for next session:**
- "Next time, you could create your first [their term for Agent] for your [their branch] — a specialist that knows your domain."
- "Or you could jump straight into Execution Mode and use what we have. The system will tell us what needs building."
- "Either way, the [their term for The Loop] takes hold. Building and using happen together."

## After Planting

Once the planting conversation completes:
- `glossary.md` has a populated Foundation section and no UNPLANTED marker
- An environment state file exists
- `CLAUDE.md` references the environment file
- The user has a shared vocabulary and understands the tree metaphor
- Subsequent initializations proceed normally — no planting conversation

## Notes

- The planting conversation replaces the "read glossary.md and processes.md" step from the original onboarding. Users should not need to read the full glossary or processes to start working — those files are for the AI to reference.
- The AI should naturally use the user's preferred terms from the Foundation section in all subsequent conversation. System artifacts (processes.md, schemas, rules) always use canonical terms.
- If a user forks a seed that has already been planted (UNPLANTED marker removed, Foundation populated), the AI should note the existing vocabulary and ask if the user wants to keep it or re-plant with their own terms.
