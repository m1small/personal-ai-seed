# Sapling Planting Conversation

An extended planting conversation for saplings. Supplements `prompts/planting.md` with a "Tour the Branches" phase that walks the user through pre-built content.

## When This Runs

The AI detects both `<!-- UNPLANTED -->` in `glossary.md` AND a `prompts/sapling-context.md` file. The base planting conversation runs with modifications:

1. Welcome (adapted — acknowledge this is a sapling, not a raw seed)
2. First Branch Discovery (adapted — pre-built branches are already present)
3. Vocabulary Calibration (unchanged — the user still names their terms)
4. **Tour the Branches** (new — walk through pre-built content)
5. Glossary Production (unchanged)
6. Environment Discovery (adapted — tool contract templates guide the setup)
7. Growth and Development Loop Introduction (unchanged)

## Adaptations to Base Flow

### 1. Welcome (Adapted)

The welcome acknowledges the sapling's pre-grown content.

**Key points to convey:**
- This is a sapling — a seed that's already started growing. Someone has built out branches for you based on their experience.
- Read `prompts/sapling-context.md` to understand what's pre-built.
- Everything is still personal — we'll calibrate vocabulary, customize what's here, and you'll grow it from this point forward.
- The tree metaphor still applies: roots (AI services), trunk (processes), branches (some pre-built, some you'll grow), canopy (what your system produces).

**Tone:** Same as base — warm, practical. Emphasize that pre-built content is a starting point, not a prescription.

### 2. First Branch Discovery (Adapted)

The sapling already has branches. Adapt the discovery:

**Example prompt:** "This sapling comes with pre-built branches — [list from sapling-context.md]. Before we explore what's here, I want to know: is this the area you most want to focus on first? Or is there a different area of your life where you'd benefit most from an AI that remembers and builds over time?"

**Why this matters:** The pre-built branches may or may not be the user's priority. If they are — great, the examples in vocabulary calibration use the pre-built branch. If not — record their preferred first branch alongside the pre-built ones. Both are valid.

### 3. Vocabulary Calibration (Unchanged)

Run exactly as in `prompts/planting.md`. The user names their terms for Foundation concepts. Pre-built content uses canonical terms internally; the user's preferred names apply in conversation.

Add one concept to the calibration:

#### Pre-grown starting point
"This system started as a **Sapling** — a seed with some branches already built out. The pre-built content gives you a head start. Does Sapling work as a term for this, or do you think of it differently?"

### 4. Tour the Branches (New)

After vocabulary calibration and before glossary production, walk through the pre-built content.

**Prompt:** "Now let's look at what's already growing on your tree. This sapling came with some branches ready to use. I'll walk you through what's here so you know what you're working with."

**For each pre-built area (read from `prompts/sapling-context.md`):**

1. **Name the area** using the user's vocabulary (from calibration).
2. **Explain what's pre-built** — agents, data stores, schemas, tool contracts.
3. **Show what's ready to use** — pre-structured data stores, agent templates with decision rules.
4. **Identify customization points** — what the user needs to personalize (persona, credentials, domain knowledge).
5. **Ask if it makes sense** — "Does this match how you'd organize this part of your work, or would you restructure it?"

**Guidelines:**
- Don't read every file aloud. Summarize what's in each area and offer to go deeper on anything that interests them.
- If the user wants to rename an agent or restructure data stores, note it. Those changes happen in a subsequent session, not during planting.
- The goal is comprehension, not customization. They should know what they have before they start using it.

### 5. Glossary Production (Unchanged)

Run exactly as in `prompts/planting.md`. Include the Sapling Foundation entry if the user calibrated it.

### 6. Environment Discovery (Adapted)

Tool contract templates in the sapling guide the setup. Instead of probing from scratch, use the templates:

**Prompt:** "This sapling came with tool connection templates for [list tools from sapling-context.md]. Let's see which ones you have access to and get them connected."

**Process:**
1. Read the tool contract templates in `tools/`.
2. For each template, check if the tool is available in the current environment.
3. Walk the user through connecting tools that are available but not yet connected. Follow the setup guidance in each template.
4. Produce the environment state file with the results.
5. Note any tools that aren't available yet — they can be connected in a future session.

### 7. Growth and Development Loop Introduction (Unchanged)

Run exactly as in `prompts/planting.md`. Use the user's vocabulary.

**Additional sapling-specific closing:** "You're starting further along than someone planting from a seed — you have pre-built [their terms for agents/data stores/etc.] to work with right away. Next session, you could customize a [their term for Agent] that's already here, or start using what you have. The [their term for Growth and Development Loop] takes it from here."

## After Planting

Same as base planting, plus:
- User understands what's pre-built in the sapling
- Tool contract templates have been used to guide environment setup
- Customization needs are identified (recorded in sapling-context.md or session notes)
- Pre-built agents, data stores, and schemas are in place and understood

## Notes

- A sapling planting takes longer than a seed planting because of the branch tour. Budget for a longer first session.
- The branch tour should feel like a guided walkthrough, not a documentation review. Show the user what their system can do, not what files exist.
- If the user is experienced with the seed pattern (e.g., they're moving from a different tree to a sapling), the branch tour can be abbreviated. Ask: "Are you familiar with how Personal AI systems work, or would you like a full tour?"
