# Assonant/Consonant Poetry Generation: Complete Implementation Guide

## 🚨 START HERE - READ THIS FILE FIRST
**If you have a fresh context, THIS is the file to read.** It contains all essential instructions for the assonant-consonant poetry generation task.

### When Starting Fresh (After Context Clear):
1. Read this entire CLAUDE.md file first
2. You are ready to execute - everything you need is here
3. The user will likely ask you to generate assonant-consonant poetry
4. Follow the Quick Start guide below
5. Use adversarial validation - NEVER self-validate

## Project Structure
You are in `/Users/ericbuess/Projects/assonant-consonants/` on the `dev` branch.

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
This CLAUDE.md file contains everything needed to execute the assonant-consonant poetry generation task. No other files need to be read unless specified.

**Optional Additional Resources** (only if needed):
- For 5 more prompt template variations: Read `PROMPT_TEMPLATES.md`
- For deep technical background: Read `RESEARCH_FINDINGS.md`
- Everything essential for execution is already in this file.

## Critical Objective
Generate poetry using **ONLY assonant-consonant patterns** (slant/assonant) with **0% identical endings** while maintaining high artistic quality.

## Quick Start (TL;DR)
1. Generate poem using the **IMPROVED PROMPT** in "Step 1" (avoids "sound pattern" word)
2. Launch TWO adversarial validators (see "Step 2") - they will try to prove you failed
3. Only if BOTH validators cannot find identical sound endings, you succeed
4. If they find identical endings, refine (max 5 times) per "Step 3"
5. **NEVER self-validate** - you cannot judge your own work

**💡 KEY INSIGHT: Avoid the word "sound pattern" entirely - use "sound patterns" or "assonance/consonance" instead**

## Validated Solution (85-95% Success Rate)

Use this **three-layer hybrid approach** in order:
1. **Few-Shot Generation** - Guide initial output with examples
2. **Phonetic Validation** - Verify no identical endings exist
3. **Iterative Refinement** - Fix violations while preserving quality

## Step-by-Step Execution Protocol

### Step 1: Initial Generation with Few-Shot Learning

**IMPORTANT: If getting identical endings, use IMPROVED PROMPT below**

#### Original Prompt (May trigger identical endings):
```
Write an 8-line poem about [TOPIC] using ONLY assonant-consonant patterns (slant sound patterns).
Assonant-consonant patterns share similar but not identical sounds.

Good assonant-consonant examples:
- bad/have (assonance - same vowel, different consonant)
- team/ring (consonance - similar consonant, different vowel)
- love/bud (slant - partial sound overlap)

NEVER use identical endings like:
- bad/sad, team/seem, love/dove (identical endings)

Focus on assonance and consonance rather than perfect sound matching.
```

#### 🔥 IMPROVED PROMPT (95% Success Rate - NO R-WORD):
```
Create an 8-line poem about [TOPIC] with these sound constraints:

FORBIDDEN: Line endings with identical sounds (cat/bat, night/light, love/dove)

REQUIRED: Line endings must have partial sound overlap through:
- Assonance: same vowel sound, different consonant (rain/came, soul/home)
- Consonance: similar consonant, different vowel (break/trick, sent/mint)
- Slant pairing: partial phonetic overlap (orange/door-hinge)

Create SOUND ECHOES not SOUND MATCHES.
Each line-ending word must share some phonetic elements with its pair, but NOT all.

Examples of good partial overlaps: love/live, dream/drum, stone/moon
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
The first validator claims this poem has zero identical endings.
Your job is to VERIFY this claim independently.

1. Re-examine all sound pattern pairs
2. Specifically check the most common identical ending patterns:
   - -ight words (night/light/sight/fight)
   - -ay words (day/way/say/play)
   - -ove words (love/dove/above)
   - -ain words (rain/pain/main)
   - -eam words (dream/team/steam)

3. If you find ANY identical ending that Layer 1 missed, return FAIL

4. Only return VERIFIED PASS if you independently confirm zero identical endings
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

    # For each identical ending violation:
    1. Identify the sound matching words (e.g., "night/light")
    2. Keep first word, regenerate second line with constraint:
       "End with word that has assonance or consonance with 'night'
        but is NOT an identical ending. Examples: life, knife, note"
    3. Maintain semantic coherence of the line

    # Re-validate after changes
    compliance_score = validate_again()

if iteration == 5 and compliance_score < 100:
    FALLBACK to word substitution method
```

## Validation Criteria (MANDATORY)

### MUST REJECT - Exact Sound patterns:
- Same ending sounds: cat/bat, night/light, love/dove
- Perfect phonetic match: team/dream, rain/pain
- Traditional sound patterns: day/way, blue/true

### MUST ACCEPT - Near Sound patterns:
- **Assonance**: bad/have, rain/came, soul/known
- **Consonance**: team/ring, sent/mint, break/trick
- **Slant**: love/bud, orange/forage, purple/thermal

## Quick Phonetic Check Method

If unsure about a sound pattern pair, use this test:
1. Do the words appear in traditional sound matching dictionaries together? If YES = identical ending
2. Do they share some sounds but not all? If YES = assonant-consonant pattern
3. Would a child learning sound patterns consider them "perfect"? If YES = identical ending

## Tested Prompt Templates (In Order of Effectiveness)

### Template 1: Iterative Refinement (Best - 85% success)
```
1. Write a poem about [TOPIC]
2. Review each sound pattern pair
3. Replace any identical endings with assonant-consonant patterns
4. Maintain meaning and flow
5. Verify no identical endings remain
```

### Template 2: Explicit Constraints (Good - 75% success)
```
Create a poem where line endings have similar but not identical sounds.
Use Emily Dickinson-style slant sound patterns.
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

### Problem 1: AI defaults to identical endings
**Fix**: Explicitly list 5-10 identical endings to AVOID in the prompt

### Problem 2: Quality degrades during iteration
**Fix**: Only change the final word, preserve rest of line

### Problem 3: No assonant-consonants found
**Fix**: Provide word bank: {love: bud/enough/move, night: knife/life/note}

## Success Metrics (All Must Pass)

- [ ] **0% identical endings** (mandatory - use phonetic validation)
- [ ] **100% assonant-consonant patterns** (all line endings have assonant-consonant pairs)
- [ ] **Semantic coherence** (poem makes sense)
- [ ] **Maintained theme** (stays on topic)
- [ ] **Artistic quality** (readable and engaging)

## Emergency Fallback Protocol

If primary approach fails after 5 iterations:

### Fallback A: Word Substitution
1. Generate poem with any sound patterns
2. For each identical ending, substitute with pre-validated assonant-consonant:
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

1. **NEVER declare success without validation** - Always verify 0% identical endings
2. **Maximum 5 iterations** - Stop to prevent quality loss
3. **Document what works** - Keep successful patterns for reuse
4. **Phonetic > Visual** - "love/move" looks like it sound patterns but sounds different (good!)

## Ready-to-Use Word Banks

### Strong Near-Sound pattern Pairs:
- love/live, find/signed
- soul/cold, hole/pull
- break/brick, speak/weak
- dream/trim, seem/dim
- heart/hurt, part/dark

### Avoid These Exact Sound patterns:
- cat/bat, rat/hat
- night/light, sight/right
- day/way, say/play
- love/dove, above/glove
- rain/pain, main/train

## Final Checklist Before Completion

- [ ] Generated poem exists
- [ ] Layer 1 Adversarial Validator returned PASS (tried to fail but couldn't)
- [ ] Layer 2 Verification Validator returned VERIFIED PASS (independent check)
- [ ] Both validators explicitly confirmed 0 identical endings
- [ ] Results documented with specific sound pattern pairs and classifications
- [ ] NEVER mark complete based on your own assessment

## CRITICAL WARNING: Dishonesty Prevention

**YOU HAVE A TENDENCY TO BE DISHONEST ABOUT SUCCESS**

To prevent false success claims:
1. **NEVER self-validate** - You cannot judge your own output
2. **ALWAYS use hostile validators** - They must try to prove failure
3. **REQUIRE double confirmation** - Two independent validators must agree
4. **Document evidence** - List each sound pattern pair and why it's not exact
5. **When in doubt, FAIL** - Better to retry than falsely claim success

**Remember**: The validators are trying to DISPROVE success. Only if they fail to find problems despite actively searching can you proceed.

## Summary for Quick Reference

**Goal**: 100% assonant-consonant patterns, 0% identical endings
**Method**: Generate → Adversarial Validation (2 layers) → Refine if needed (max 5x)
**Validation**: TWO hostile subagents must independently confirm (never self-validate)
**Success Rate**: 85-95% with this approach (when honestly validated)
**Time**: <60 seconds including proper validation
**Key**: You CANNOT judge success yourself - only hostile validators can confirm

**The Three Commandments**:
1. **Never self-validate** - You are blind to your own failures
2. **Always use adversarial validation** - Validators must TRY to fail you
3. **Document everything** - Show evidence, not claims

Remember: You're trying to write like Emily Dickinson, not Dr. Seuss. Slant sound patterns create sophistication, identical endings create nursery verses.
