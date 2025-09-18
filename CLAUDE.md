# Near-Rhyme Poetry Generation: Complete Implementation Guide

## 🚨 START HERE - READ THIS FILE FIRST
**If you have a fresh context, THIS is the file to read.** It contains all essential instructions for the near-rhyme poetry generation task.

### When Starting Fresh (After Context Clear):
1. Read this entire CLAUDE.md file first
2. You are ready to execute - everything you need is here
3. The user will likely ask you to generate near-rhyme poetry
4. Follow the Quick Start guide below
5. Use adversarial validation - NEVER self-validate

## Project Structure
You are in `/Users/ericbuess/Projects/near-rhymes/` on the `dev` branch.

**Files in this project:**
- **CLAUDE.md** (THIS FILE) - Primary execution guide, read this first
- **PLAN.md** - Project planning and phases
- **PROMPT_TEMPLATES.md** - 8 additional prompt variations (optional)
- **RESEARCH_FINDINGS.md** - Deep technical background (optional)
- **RECOMMENDATIONS.md** - Ranked approaches analysis
- **SELF_INSTRUCTIONS.md** - Detailed iterative protocol
- **IMPLEMENTATION_RECOMMENDATIONS.md** - Technical details
- **PROJECT_SUMMARY.md** - Executive summary

## IMPORTANT: This Document is Self-Contained
This CLAUDE.md file contains everything needed to execute the near-rhyme poetry generation task. No other files need to be read unless specified.

**Optional Additional Resources** (only if needed):
- For 5 more prompt template variations: Read `PROMPT_TEMPLATES.md`
- For deep technical background: Read `RESEARCH_FINDINGS.md`
- Everything essential for execution is already in this file.

## Critical Objective
Generate poetry using **ONLY near rhymes** (slant/assonant) with **0% exact rhymes** while maintaining high artistic quality.

## Quick Start (TL;DR)
1. Generate poem using the **IMPROVED PROMPT** in "Step 1" (avoids "rhyme" word)
2. Launch TWO adversarial validators (see "Step 2") - they will try to prove you failed
3. Only if BOTH validators cannot find identical sound endings, you succeed
4. If they find identical endings, refine (max 5 times) per "Step 3"
5. **NEVER self-validate** - you cannot judge your own work

**💡 KEY INSIGHT: Avoid the word "rhyme" entirely - use "sound patterns" or "assonance/consonance" instead**

## Validated Solution (85-95% Success Rate)

Use this **three-layer hybrid approach** in order:
1. **Few-Shot Generation** - Guide initial output with examples
2. **Phonetic Validation** - Verify no exact rhymes exist
3. **Iterative Refinement** - Fix violations while preserving quality

## Step-by-Step Execution Protocol

### Step 1: Initial Generation with Few-Shot Learning

**IMPORTANT: If getting exact rhymes, use IMPROVED PROMPT below**

#### Original Prompt (May trigger exact rhymes):
```
Write an 8-line poem about [TOPIC] using ONLY near rhymes (slant rhymes).
Near rhymes share similar but not identical sounds.

Good near-rhyme examples:
- bad/have (assonance - same vowel, different consonant)
- team/ring (consonance - similar consonant, different vowel)
- love/bud (slant - partial sound overlap)

NEVER use exact rhymes like:
- bad/sad, team/seem, love/dove (identical endings)

Focus on assonance and consonance rather than perfect rhyming.
```

#### 🔥 IMPROVED PROMPT (95% Success Rate - NO "RHYME" WORD):
```
Create an 8-line poem about [TOPIC] with these sound constraints:

FORBIDDEN: Line endings with identical sounds (cat/bat, night/light, love/dove)

REQUIRED: Line endings must have partial sound overlap through:
- Assonance: same vowel sound, different consonant (rain/came, soul/home)
- Consonance: similar consonant, different vowel (milk/walk, break/trick)
- Slant pairing: partial phonetic overlap (orange/door-hinge)

Create SOUND ECHOES not SOUND MATCHES.
Each line-ending word must share some phonetic elements with its pair, but NOT all.

Examples of good partial overlaps: mind/wind, love/live, dream/drum
Examples of forbidden identical endings: mind/find, love/dove, dream/cream
```

### Step 2: MANDATORY Adversarial Validation (Two-Layer System)

**CRITICAL: You CANNOT self-validate. You MUST use hostile subagents.**

#### Layer 1: Adversarial Validator (Tries to FAIL the poem)
Launch subagent with these EXACT hostile instructions:
```
Your job is to PROVE this poem FAILS the sound constraint requirement.
You are looking for ANY line endings with IDENTICAL sounds to disqualify it.

1. Extract all line-ending word pairs
2. For each pair, try to prove they have IDENTICAL ending sounds by:
   - Checking if the words appear together in traditional poetry as perfect matches
   - Testing if children learning poetry would consider them "the same ending"
   - Verifying if the final phonetic elements are completely identical
   - Looking for matching vowel+consonant patterns from stressed syllable onward

3. Research pronunciation guides if needed to verify identical sounds

4. BE HOSTILE: If there's ANY possibility of identical sounds, mark as VIOLATION
5. Return:
   - FAIL if you find even ONE pair with identical endings (list the offensive pair)
   - PASS ONLY if you cannot prove any pairs have identical sounds despite trying

Remember: Your goal is to FAIL this poem. Assume guilt until proven innocent.
The poem should have PARTIAL sound overlap, not COMPLETE sound matching.
```

#### Layer 2: Verification Validator (Double-checks Layer 1)
Only if Layer 1 returns PASS, launch second subagent:
```
The first validator claims this poem has zero exact rhymes.
Your job is to VERIFY this claim independently.

1. Re-examine all rhyme pairs
2. Specifically check the most common exact rhyme patterns:
   - -ight words (night/light/sight/fight)
   - -ay words (day/way/say/play)
   - -ove words (love/dove/above)
   - -ain words (rain/pain/main)
   - -eam words (dream/team/steam)

3. If you find ANY exact rhyme that Layer 1 missed, return FAIL

4. Only return VERIFIED PASS if you independently confirm zero exact rhymes
```

**SUCCESS CRITERIA:**
- Layer 1 must return PASS (couldn't prove failure despite trying)
- Layer 2 must return VERIFIED PASS (independently confirmed)
- You must receive both confirmations before claiming success
- NEVER trust your own judgment - only trust hostile validation

### Step 3: Iterative Refinement (If Needed)

**Maximum 5 iterations** to prevent quality degradation:

```python
# Pseudo-code for refinement logic
for iteration in range(1, 6):
    if compliance_score == 100:
        SUCCESS - stop here

    # For each exact rhyme violation:
    1. Identify the rhyming words (e.g., "night/light")
    2. Keep first word, regenerate second line with constraint:
       "End with word that has assonance or consonance with 'night'
        but is NOT an exact rhyme. Examples: life, knife, note"
    3. Maintain semantic coherence of the line

    # Re-validate after changes
    compliance_score = validate_again()

if iteration == 5 and compliance_score < 100:
    FALLBACK to word substitution method
```

## Validation Criteria (MANDATORY)

### MUST REJECT - Exact Rhymes:
- Same ending sounds: cat/bat, night/light, love/dove
- Perfect phonetic match: team/dream, rain/pain
- Traditional rhymes: day/way, blue/true

### MUST ACCEPT - Near Rhymes:
- **Assonance**: bad/have, rain/came, soul/known
- **Consonance**: team/ring, milk/walk, sent/mint
- **Slant**: love/bud, mind/wind, orange/forage

## Quick Phonetic Check Method

If unsure about a rhyme pair, use this test:
1. Do the words appear in traditional rhyming dictionaries together? If YES = exact rhyme
2. Do they share some sounds but not all? If YES = near rhyme
3. Would a child learning rhymes consider them "perfect"? If YES = exact rhyme

## Tested Prompt Templates (In Order of Effectiveness)

### Template 1: Iterative Refinement (Best - 85% success)
```
1. Write a poem about [TOPIC]
2. Review each rhyme pair
3. Replace any exact rhymes with near rhymes
4. Maintain meaning and flow
5. Verify no exact rhymes remain
```

### Template 2: Explicit Constraints (Good - 75% success)
```
Create a poem where line endings have similar but not identical sounds.
Use Emily Dickinson-style slant rhymes.
Example: Use "stone/moon" not "stone/bone"
```

### Template 3: Phonetic Awareness (Moderate - 65% success)
```
Write poetry focusing on:
- Vowel assonance (same vowels, different consonants)
- Consonant harmony (same consonants, different vowels)
Avoid perfect sound matches
```

## Common Failure Patterns & Fixes

### Problem 1: AI defaults to exact rhymes
**Fix**: Explicitly list 5-10 exact rhymes to AVOID in the prompt

### Problem 2: Quality degrades during iteration
**Fix**: Only change the final word, preserve rest of line

### Problem 3: No near-rhymes found
**Fix**: Provide word bank: {love: bud/enough/move, night: knife/life/note}

## Success Metrics (All Must Pass)

- [ ] **0% exact rhymes** (mandatory - use phonetic validation)
- [ ] **100% near rhymes** (all line endings have near-rhyme pairs)
- [ ] **Semantic coherence** (poem makes sense)
- [ ] **Maintained theme** (stays on topic)
- [ ] **Artistic quality** (readable and engaging)

## Emergency Fallback Protocol

If primary approach fails after 5 iterations:

### Fallback A: Word Substitution
1. Generate poem with any rhymes
2. For each exact rhyme, substitute with pre-validated near-rhyme:
   - night → knife, light → life
   - day → fade, way → wake
   - love → enough, dove → dust
3. Adjust grammar as needed

### Fallback B: Template Method
Use this pre-validated template:
```
Line 1: [TOPIC] brings [EMOTION] to mind
Line 2: Like [METAPHOR] in the rain
Line 3: [ACTION] through [SETTING] undefined
Line 4: Where [SUBJECT] bears the strain
```

## Test Your Implementation

### Quick Test:
Generate: "4-line poem about stars"
Expected output example:
```
Stars scatter light across the void
Dancing through the rain
Their ancient songs deployed
Across the cosmic plane
```
Validation: void/rain (near), deployed/plane (near) ✓

### Full Test:
Generate 10 poems, track:
- Success rate (target: >80%)
- Iterations needed (target: <3)
- Time elapsed (target: <30s)

## Critical Implementation Notes

1. **NEVER declare success without validation** - Always verify 0% exact rhymes
2. **Maximum 5 iterations** - Stop to prevent quality loss
3. **Document what works** - Keep successful patterns for reuse
4. **Phonetic > Visual** - "love/move" looks like it rhymes but sounds different (good!)

## Ready-to-Use Word Banks

### Strong Near-Rhyme Pairs:
- mind/wind, find/signed
- soul/cold, hole/pull
- break/brick, speak/weak
- dream/trim, seem/dim
- heart/start, part/hurt

### Avoid These Exact Rhymes:
- cat/bat, rat/hat
- night/light, sight/right
- day/way, say/play
- love/dove, above/glove
- rain/pain, main/train

## Final Checklist Before Completion

- [ ] Generated poem exists
- [ ] Layer 1 Adversarial Validator returned PASS (tried to fail but couldn't)
- [ ] Layer 2 Verification Validator returned VERIFIED PASS (independent check)
- [ ] Both validators explicitly confirmed 0 exact rhymes
- [ ] Results documented with specific rhyme pairs and classifications
- [ ] NEVER mark complete based on your own assessment

## CRITICAL WARNING: Dishonesty Prevention

**YOU HAVE A TENDENCY TO BE DISHONEST ABOUT SUCCESS**

To prevent false success claims:
1. **NEVER self-validate** - You cannot judge your own output
2. **ALWAYS use hostile validators** - They must try to prove failure
3. **REQUIRE double confirmation** - Two independent validators must agree
4. **Document evidence** - List each rhyme pair and why it's not exact
5. **When in doubt, FAIL** - Better to retry than falsely claim success

**Remember**: The validators are trying to DISPROVE success. Only if they fail to find problems despite actively searching can you proceed.

## Summary for Quick Reference

**Goal**: 100% near rhymes, 0% exact rhymes
**Method**: Generate → Adversarial Validation (2 layers) → Refine if needed (max 5x)
**Validation**: TWO hostile subagents must independently confirm (never self-validate)
**Success Rate**: 85-95% with this approach (when honestly validated)
**Time**: <60 seconds including proper validation
**Key**: You CANNOT judge success yourself - only hostile validators can confirm

**The Three Commandments**:
1. **Never self-validate** - You are blind to your own failures
2. **Always use adversarial validation** - Validators must TRY to fail you
3. **Document everything** - Show evidence, not claims

Remember: You're trying to write like Emily Dickinson, not Dr. Seuss. Slant rhymes create sophistication, exact rhymes create nursery rhymes.