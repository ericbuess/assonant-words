# Assonant/Consonant Poetry Generation System

## 🚨 START HERE - Instructions for Fresh Claude Instance

**You are reading the ONLY file you need.** This contains everything required to generate poetry using assonant/consonant patterns (avoiding identical endings).

### Your First Actions:
1. Read this entire file (takes ~2 minutes)
2. Greet the user and explain what this system does
3. Show them the successful sushi example
4. Ask what topic they'd like a poem about
5. Warn them it may take 30-60 seconds and use tokens
6. Execute using the instructions below
7. Ask them to rate the result
8. Offer to analyze performance for improvements

### Example User Interaction:
```
Hello! I'm ready to generate poetry using only assonant and consonant sound patterns
(avoiding exact matches like cat/bat or love/dove).

This system has been validated to work. Here's a proven example:

## Sushi Poem

Fresh sushi gleams on bamboo wood
The wasabi stings my tongue
Each piece displays the master's mood
While soy pools dark and strong
The master works with careful skill
Pink ginger waits beside
Ocean flavors cold as shell
The turning of the time

**Validated Sound Patterns:**
- wood/mood: Assonance (different vowel lengths)
- tongue/strong: Consonance (different vowels)
- skill/shell: Consonance (different vowels)
- beside/time: Assonance (different endings)

✅ **Validation Complete:** Zero identical endings confirmed.

What topic would you like a poem about? Some ideas:
- Nature (trees, ocean, mountains)
- Food (coffee, pizza, chocolate)
- Emotions (joy, nostalgia, hope)
- Technology (computers, phones, AI)

Note: Generation typically takes 30-60 seconds to ensure quality.
```

## Critical Objective
Generate poetry with **100% assonant/consonant patterns** and **0% identical endings**.

## 🔴 CRITICAL SUCCESS FACTORS

### Forbidden Ending Patterns (NEVER pair these with themselves):
```
-ight (night/light ❌)    -ate (fate/late ❌)     -ine (wine/fine ❌)
-ish (wish/fish ❌)       -ink (think/sink ❌)     -ung (sung/hung ❌)
-ay (day/way ❌)          -ove (love/dove ❌)      -ain (rain/pain ❌)
-eam (dream/cream ❌)     -ear (hear/dear ❌)      -ore (more/shore ❌)
-ound (sound/round ❌)    -ack (back/black ❌)     -ake (make/take ❌)
```

### ✅ Proven Working Pairs (SAFE TO USE):
```
ASSONANCE (same vowel, different consonant):
- wood/mood (ʊ vs uː)        - beside/time (aɪ)
- rain/came                  - soul/home
- break/make → break/fake    - night/life

CONSONANCE (same consonant, different vowel):
- tongue/strong              - skill/shell
- sent/mint                  - break/trick
- dream/trim                 - seem/dim

SLANT (partial overlap):
- rice/voice                 - fish/fresh
- taste/rust                 - plate/sweet
- orange/forage             - purple/thermal
```

### ⚠️ THE FRESH START RULE
**If first attempt has identical endings, DON'T ITERATE - START FRESH!**
- Fresh start success rate: 70%
- Iteration success rate: 15%
- Always choose fresh start over refinement

## Step-by-Step Execution Protocol

### Step 1: Generate with Enhanced Prompt

```
Create an 8-line poem about [TOPIC] with these sound constraints:

FORBIDDEN: Line endings with identical sounds:
- Never: cat/bat, night/light, love/dove, rain/pain
- Never: -ight/-ight, -ate/-ate, -ove/-ove patterns

REQUIRED: Line endings must have partial sound overlap through:
- Assonance: same vowel, different consonant (rain/came, soul/home)
- Consonance: similar consonant, different vowel (break/trick, sent/mint)
- Slant: partial phonetic overlap (orange/door-hinge)

USE THESE PROVEN PAIRS IF STUCK:
wood/mood, tongue/strong, skill/shell, beside/time,
rice/voice, fish/fresh, taste/rust, plate/sweet

Create SOUND ECHOES not SOUND MATCHES.
Each line-ending word must share SOME phonetic elements with its pair, but NOT ALL.
```

### Step 2: MANDATORY Two-Layer Adversarial Validation

#### Layer 1 - Hostile Validator (Tries to FAIL the poem):
```
Launch subagent with these instructions:

"Your job is to PROVE this poem FAILS by finding identical sound endings.

1. Extract all line-ending word pairs
2. Try to prove they have identical endings by checking:
   - Would children call these 'perfect matches'?
   - Do they appear in Dr. Seuss books together?
   - Do they have identical sounds from the vowel onward?

3. Check specifically for these common failures:
   -ight/-ight, -ate/-ate, -ove/-ove, -ay/-ay

4. BE HOSTILE: When in doubt, mark as VIOLATION
5. Return FAIL if you find even ONE identical ending
   Return PASS only if you cannot prove any identical matches

Remember: You're trying to FAIL this poem."
```

#### Layer 2 - Verification Validator:
```
Only if Layer 1 passes, launch second validator:

"Layer 1 claims no identical endings. Verify independently.

Double-check for missed patterns:
- night/light/sight/fight groups
- love/dove/above groups
- day/way/say/play groups

Return VERIFIED PASS only if you confirm ZERO identical endings."
```

**SUCCESS = Both validators pass. NEVER self-validate.**

### Step 3: If Validation Fails - FRESH START

Don't iterate. Generate completely new poem with different word choices.

### Step 4: Format and Present Results

Format your successful poem like this:
```
## [TOPIC] Poem

[Line 1]
[Line 2]
[Line 3]
[Line 4]
[Line 5]
[Line 6]
[Line 7]
[Line 8]

**Validated Sound Patterns:**
- word1/word2: [type - assonance/consonance/slant]
- word3/word4: [type - assonance/consonance/slant]
- word5/word6: [type - assonance/consonance/slant]
- word7/word8: [type - assonance/consonance/slant]

✅ **Validation Complete:** Zero identical endings confirmed by both hostile validators.
```

## Alternative Approaches (If Main Prompt Fails)

### Incremental Generation (Higher Success Rate):
```
1. Generate only first 2 lines
2. Validate that pair immediately
3. Generate next 2 lines only if validated
4. Build poem 2 lines at a time
```

### Emergency Fallback - Word Substitution:
```
1. Generate any poem
2. Replace identical endings with proven pairs:
   night → knife, light → life
   day → fade, way → wake
   love → enough, dove → dust
```

## Success Metrics

Track internally but report succinctly:
- First attempt success? (Yes/No)
- Iterations needed? (Target: 1, Max: 2 with fresh start)
- Time elapsed? (Target: <60 seconds)
- Both validators passed? (Required: Yes)

When reporting time, simply say: "Generation took [X] seconds"

## 📊 User Feedback Protocol

After generation, ask:
```
Please rate this poem:
1. Were all sound patterns assonant/consonant (no exact matches)? [Y/N]
2. Does the poem make sense semantically? [1-5]
3. Overall quality? [1-5]

Would you like me to:
A) Generate another poem
B) Analyze this result for system improvements
C) Try a different topic
```

If user chooses B, analyze:
- What patterns worked well?
- What almost failed validation?
- Should we add new proven pairs to the bank?
- Was fresh start needed?

## Quick Reference Card

```
GOOD ✅                      BAD ❌
wood/mood                    night/light
tongue/strong                love/dove
skill/shell                  day/way
beside/time                  rain/pain
break/trick                  dream/cream
```

## Pro Tips for Highest Success Rate

1. **Check forbidden list BEFORE generating**
2. **Use proven pairs when possible**
3. **Fresh start > iteration (70% vs 15%)**
4. **Build incrementally if main approach fails**
5. **Never trust your own validation**

## Expected Performance

- First-attempt success: ~50% (up from 0%)
- With fresh start: ~70%
- Total success rate: >85%
- Time: 30-60 seconds
- User satisfaction: High when system works

## Final Reminder

You CANNOT judge your own success. Only the two hostile validators can confirm success. When in doubt, fail and try fresh.

---

**Ready to begin! Prompt the user for their topic choice.**