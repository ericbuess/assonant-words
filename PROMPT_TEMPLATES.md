# Concrete Prompt Templates for Near-Rhyme Poetry Generation

## Ready-to-Test Prompt Templates

### Template 1: Direct Constraint Specification
```
Write an 8-line poem about [TOPIC] using only near rhymes or slant rhymes.

AVOID perfect rhymes like:
- night/light, love/dove, day/way, heart/part

USE subtle sound relationships like:
- love/bud (assonance)
- team/ring (consonance)
- home/stone (slant rhyme)
- mind/send (partial match)

Focus on meaning and natural flow while maintaining these sound constraints.
```

### Template 2: Few-Shot Learning with Examples
```
Here are examples of poems using only near/slant rhymes:

Example 1:
The morning felt strange and new,
While shadows danced in patterns broad.
I walked through streets both old and blue,
Seeking some forgotten word.

Example 2:
Love grows like a tender bud,
In gardens where the heart can sing.
Through seasons of both joy and mud,
We find what each new day will bring.

Now write a similar 8-line poem about [TOPIC] using the same near-rhyme style.
Avoid perfect rhymes. Use subtle sound connections instead.
```

### Template 3: Technical Specification with Validation
```
Generate a poem with these constraints:
- Topic: [TOPIC]
- Length: 8 lines
- Rhyme scheme: ABAB CDCD (using only slant/near rhymes)
- NO perfect rhymes (identical phonetic endings)
- YES to: assonance, consonance, visual rhymes, partial matches
- Maintain natural syntax and meaning
- If uncertain about a rhyme, err toward looser connections

Check each line ending against the constraint before finalizing.
```

### Template 4: Negative Constraint with Positive Guidance
```
Write a poem about [TOPIC] that uses interesting sound patterns but completely avoids obvious perfect rhymes.

FORBIDDEN rhyme types:
- Identical endings: cat/bat, ring/sing, play/stay
- Perfect sound matches: light/night, love/dove

ENCOURAGED connections:
- Assonance: home/stone (similar vowels)
- Consonance: milk/walk (similar consonants)
- Slant rhymes: mind/send (partial overlap)
- Visual rhymes: love/move (look similar, sound different)

Prioritize natural expression over forced sound patterns.
```

### Template 5: Iterative Refinement Approach
```
Step 1: Write a poem about [TOPIC] with natural expression, ignoring rhyme constraints.

Step 2: Examine each potential rhyme pair. Replace any perfect rhymes with near rhymes:
- "night/light" → "night/dream" or "night/still"
- "love/dove" → "love/warmth" or "love/hope"
- "day/way" → "day/time" or "day/path"

Step 3: Ensure the meaning and flow remain intact after substitutions.

Step 4: Final check - no identical phonetic endings should remain.
```

### Template 6: Sound Pattern Focus
```
Create a poem about [TOPIC] that emphasizes these specific sound techniques:

Primary technique: Assonance (repeated vowel sounds)
- Example: "hear the clear bell near the pier"

Secondary technique: Consonance (repeated consonant sounds)
- Example: "pitter patter of tiny feet"

Avoid: Perfect end rhymes
Length: 8 lines
Structure: Free verse with natural line breaks

Let sound patterns emerge organically from the meaning.
```

### Template 7: Multi-Agent Simulation
```
Poet Agent: Write an 8-line poem about [TOPIC] focusing on natural expression and meaning.

Rhyme Checker Agent: Examine the poem for perfect rhymes. List any found:
- Line X and Line Y: [word1/word2] = perfect rhyme

Revision Agent: Replace perfect rhymes with near rhymes while preserving meaning:
- [word1/word2] → [word1/alternative]

Quality Agent: Verify the final poem maintains:
- Natural flow and readability
- Consistent meaning and tone
- Only near/slant rhymes remain
```

### Template 8: Phonetic Awareness
```
Write a poem about [TOPIC] considering these phonetic principles:

Rhyme occurs in the "rime" (nucleus + coda) of stressed syllables.
Perfect rhyme = identical rime (love/dove)
Near rhyme = similar but not identical (love/live, love/move)

For this poem:
- Use words with similar vowel sounds but different consonants
- Or similar consonant patterns but different vowels
- Avoid any words with identical phonetic endings
- 8 lines, natural expression prioritized

Think phonetically, not just visually.
```

## Quick Reference: Good vs. Bad Rhyme Examples

### ✅ GOOD (Near/Slant Rhymes)
- love/bud
- team/ring
- home/stone
- mind/send
- heart/start
- day/dream
- light/life
- hope/deep

### ❌ BAD (Perfect Rhymes to Avoid)
- love/dove
- team/seem
- home/dome
- mind/kind
- heart/part
- day/way
- light/night
- hope/rope

## Testing Protocol

1. Choose a template based on your approach preference
2. Replace [TOPIC] with specific subject matter
3. Generate poem using the template
4. Manually check each rhyme pair against the good/bad examples
5. If perfect rhymes found, use Template 5 (iterative refinement)
6. Document success rate and patterns that work
7. Refine template based on results

## Validation Questions for Generated Poems

- Are there any identical phonetic endings? (If yes = failure)
- Do the sound connections enhance rather than force the meaning?
- Would the poem work even without the rhyme constraints?
- Are the near rhymes subtle enough to avoid "jingly" effects?
- Does the poem maintain natural syntax and flow?

## Next Steps

Test these templates systematically and document:
- Which templates produce the highest success rates
- Common failure patterns that emerge
- Refinements needed for each approach
- Best practices for specific topics or themes