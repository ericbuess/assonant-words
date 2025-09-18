# Near-Rhyme Poetry Generation Plan

## Problem Statement
Force AI to generate poetry/songs using ONLY near rhymes (slant/assonant rhymes) and NOT exact rhymes.
- Good examples: bad:have, team:ring, love:bud
- Bad examples: bad:sad, team:seem, love:dove

## Phase 1: Research & Discovery
- [x] ✅ Research existing approaches for constrained poetry generation
  - [x] ✅ Search for academic papers on slant rhyme generation
  - [x] ✅ Look for existing tools/libraries for rhyme detection
  - [x] ✅ Find examples of successful near-rhyme poetry prompts
  - [x] ✅ Research phonetic analysis tools (CMU Pronouncing Dictionary, etc.)

- [x] ✅ Research rhyme classification methods
  - [x] ✅ Phonetic similarity metrics
  - [x] ✅ Vowel assonance detection
  - [x] ✅ Consonance patterns
  - [x] ✅ Stress pattern analysis

## Phase 2: Solution Architecture
- [x] ✅ Evaluate and rank approaches (using subagent):
  1. ✅ Phonetic analysis filtering (Rank #1: 85-95% success, best balance)
  2. ✅ Iterative validation loop (Rank #2: 75-85% success, self-correcting)
  3. ✅ Multi-agent generation/validation (Rank #3: 80-90% success, proven improvements)
  4. ✅ Few-shot learning with curated examples (Rank #4: 60-75% success, easy to implement)
  5. ✅ Template-based generation (Rank #5: 70-80% success, reliable for formal poetry)
  6. ✅ Prompt engineering with negative examples (Rank #6: 25-40% success, baseline approach)
  7. ✅ Reinforcement learning with custom scoring (Rank #7: 90-95% after training, too complex)

- [x] ✅ Select top 3 approaches for implementation:
  1. Phonetic analysis filtering (Primary validation)
  2. Iterative validation loop (Refinement mechanism)
  3. Few-shot learning with examples (Generation guidance)

## Phase 3: Implementation Strategy

### Core Components
- [ ] Create validation system
  - [ ] Define exact rhyme detection rules
  - [ ] Implement near-rhyme scoring algorithm
  - [ ] Build test suite with known good/bad examples

- [ ] Develop generation pipeline
  - [ ] Initial prompt construction
  - [ ] Generation attempt
  - [ ] Validation check
  - [ ] Iterative refinement (if needed)
  - [ ] Quality assessment

### Validation Criteria
1. **Exact Rhyme Detection** (MUST FAIL):
   - Same ending phonemes
   - Perfect vowel + consonant match
   - Identical rime (nucleus + coda)

2. **Near Rhyme Detection** (MUST PASS):
   - Assonance: Similar vowel sounds, different consonants
   - Consonance: Similar consonant sounds, different vowels
   - Slant: Partial phonetic overlap
   - Visual rhyme: Look similar but sound different

3. **Quality Metrics**:
   - Maintains rhythm/meter
   - Semantic coherence
   - Artistic merit
   - Consistency throughout piece

## Phase 4: Testing Protocol
- [ ] Generate test poem with approach #1
  - [ ] Validate with subagent
  - [ ] Score adherence (0-100%)
  - [ ] Log failures and reasons

- [ ] Iterate with refinements
  - [ ] Adjust prompts based on failures
  - [ ] Maximum 5 iterations per approach
  - [ ] Track improvement metrics

- [ ] Compare approaches
  - [ ] Success rate
  - [ ] Iteration count needed
  - [ ] Output quality
  - [ ] Consistency

## Phase 5: Self-Improvement Loop
1. **Generate** poem/song with constraints
2. **Analyze** with validation subagent
3. **Identify** exact rhymes if any
4. **Refine** prompt/approach based on failures
5. **Regenerate** until criteria met
6. **Document** successful patterns

## Success Criteria
- [ ] ⚪ 100% near rhymes (0% exact rhymes)
- [ ] ⚪ Minimum 8 line poem generated
- [ ] ⚪ 3 different successful approaches documented
- [ ] ⚪ Reproducible results (>80% success rate)

## Deliverables
- [x] ✅ Ranked list of approaches with pros/cons (RECOMMENDATIONS.md)
- [x] ✅ Best prompt templates for near-rhyme generation (PROMPT_TEMPLATES.md)
- [ ] Example poems demonstrating success (ready to test)
- [ ] Validation tool for checking rhyme types (protocol defined)
- [x] ✅ Documentation of patterns that work (CLAUDE.md)
- [x] ✅ Self-instructions for iterative improvement (SELF_INSTRUCTIONS.md)
- [x] ✅ Implementation guide for fresh context (CLAUDE.md)

## Notes
- Focus on practical, reproducible solutions
- Document what DOESN'T work as much as what does
- Keep examples concrete and testable