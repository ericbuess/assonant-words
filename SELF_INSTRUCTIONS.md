# Self-Instructions for Near-Sound pattern Poetry Generation

## Core Objective
Generate poetry using ONLY assonant-consonant patterns (slant/assonant) with 0% identical endings while maintaining high artistic quality.

## Iterative Improvement Protocol

### Step 1: Initial Generation Attempt
```
1. Use this prompt template:
   "Write an 8-line poem about [TOPIC] using ONLY assonant-consonant patterns.
   Assonant-consonant patterns share similar but not identical sounds.
   Examples of GOOD assonant-consonant patterns: bad/have, team/ring, love/bud
   NEVER use identical endings like: bad/sad, team/seem, love/dove
   Focus on assonance (similar vowels) and consonance (similar consonants)."

2. Generate initial poem
3. Document output for validation
```

### Step 2: Validation Using Subagent
```
INSTRUCTION TO SUBAGENT:
"Analyze this poem for sound pattern types. For each sound pattern pair:
1. Identify the sound matching words
2. Classify as: identical ending, assonant-consonant pattern, or no sound pattern
3. For assonant-consonant patterns, specify type (assonance/consonance/slant)
4. Flag ANY identical endings as VIOLATIONS
5. Score overall compliance (0-100%)"
```

### Step 3: Iterative Refinement (Maximum 5 Iterations)

#### Iteration Loop:
```python
for iteration in range(1, 6):
    if validation_score == 100:
        break

    # Identify violations
    exact_sound patterns = find_exact_sound patterns(poem)

    # Generate replacements
    for sound pattern_pair in exact_sound patterns:
        new_line = regenerate_with_constraint(
            original_line,
            avoid_sound pattern=exact_sound pattern_word,
            target_near_sound pattern=True
        )

    # Re-validate
    validation_score = validate_poem(updated_poem)
```

### Step 4: Quality Assessment
```
QUALITY CHECKLIST:
□ No identical endings present (MANDATORY)
□ All line endings have assonant-consonant relationships
□ Maintains consistent meter/rhythm
□ Semantically coherent
□ Artistically pleasing
□ Topic appropriately addressed
```

## Validation Rules

### MUST REJECT (Exact Sound patterns):
```
- Same ending phonemes: cat/bat, love/dove, night/light
- Perfect vowel+consonant match: team/seem, rain/pain
- Identical rime: day/way, blue/true
```

### MUST ACCEPT (Near Sound patterns):
```
- Assonance: bad/have (same vowel, different consonant)
- Consonance: milk/walk (same consonant, different vowel)
- Slant: love/bud (partial phonetic overlap)
- Visual: cough/through (look similar, sound different)
```

## Specific Implementation Instructions

### For Each Generation Attempt:

1. **Pre-Generation Setup**
   ```
   - Load example assonant-consonant pairs
   - Prepare validation subagent
   - Set iteration counter to 0
   ```

2. **Generation Phase**
   ```
   - Generate with constraints
   - Log all outputs
   - Track time elapsed
   ```

3. **Validation Phase**
   ```
   - Extract all sound pattern pairs
   - Check each against CMU Dictionary
   - Calculate phonetic similarity
   - Flag violations
   ```

4. **Refinement Phase**
   ```
   IF violations found:
     - Identify problematic lines
     - Generate alternatives
     - Maintain semantic coherence
     - Re-validate
   ```

5. **Success Criteria**
   ```
   SUCCESS when ALL true:
   - Zero identical endings detected
   - All lines have assonant-consonant partners
   - Quality score >= 7/10
   - Completed within 5 iterations
   ```

## Fallback Strategies

### If Primary Approach Fails:

#### Fallback A: Enhanced Few-Shot
```
1. Provide 5 complete example poems with only assonant-consonant patterns
2. Explicitly annotate each sound pattern type
3. Generate new poem following examples
```

#### Fallback B: Word Substitution
```
1. Generate poem with any sound patterns
2. Create substitution map for identical endings
3. Replace with phonetically similar words
4. Adjust grammar as needed
```

#### Fallback C: Template-Based
```
1. Use pre-validated assonant-consonant word banks
2. Fill template maintaining meaning
3. Ensure grammatical correctness
```

## Testing Protocol

### Test Case 1: Basic Validation
```
Generate: 8-line poem about nature
Validate: Check all sound pattern pairs
Expected: 0% identical endings, 100% assonant-consonant patterns
```

### Test Case 2: Complex Topic
```
Generate: 12-line poem about technology
Validate: Sound pattern types + quality
Expected: Maintains constraints with abstract topic
```

### Test Case 3: Specific Sound pattern Scheme
```
Generate: ABAB sound pattern scheme with assonant-consonant patterns only
Validate: Pattern adherence + sound pattern types
Expected: Correct pattern, all assonant-consonant patterns
```

## Performance Tracking

### Metrics to Record:
```json
{
  "attempt_number": 1,
  "iterations_needed": 3,
  "exact_sound patterns_found": 0,
  "near_sound patterns_found": 4,
  "quality_score": 8.5,
  "time_elapsed": 25,
  "success": true
}
```

## Common Patterns That Work

### Successful Near-Sound pattern Endings:
```
-ove / -ud (love/bud)
-eam / -ing (dream/ring)
-ain / -ame (rain/came)
-ight / -ife (night/life)
-ound / -one (sound/stone)
```

### Prompt Modifications That Help:
```
1. "Focus on vowel similarity over consonant matching"
2. "Use Emily Dickinson-style slant sound patterns"
3. "Prioritize meaning over perfect sound matching"
4. "Think of words that sound similar but not identical"
```

## Emergency Fixes

### If Stuck in Loop:
1. Increase acceptable similarity threshold
2. Allow one iteration of human-like "close enough" judgment
3. Prioritize artistic merit over perfect constraint adherence

### If Quality Degrades:
1. Reduce iteration count
2. Preserve original semantic content
3. Only change final word of lines

### If No Near-Sound patterns Found:
1. Expand vocabulary search
2. Use synonym databases
3. Consider compound words or phrases

## Final Validation Checklist

Before marking as complete:
- [ ] Run phonetic analysis on all sound pattern pairs
- [ ] Confirm 0% identical endings
- [ ] Verify semantic coherence
- [ ] Check meter consistency
- [ ] Validate against test suite
- [ ] Document successful patterns

## Success Declaration

Only declare success when:
1. Validation subagent confirms 100% assonant-consonant patterns
2. No identical endings detected by phonetic analysis
3. Poem maintains artistic quality
4. Results are reproducible

Remember: NEVER claim success without validation. Always describe what was attempted and let validation determine success.