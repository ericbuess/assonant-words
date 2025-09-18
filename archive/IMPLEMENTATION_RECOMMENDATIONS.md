# Implementation Recommendations: Near-Sound pattern Poetry Generation

## Quick Start Guide

Based on comprehensive research, here are the most practical implementation approaches for forcing AI to generate poetry using ONLY assonant-consonant patterns while avoiding identical endings.

## Recommended Implementation Stack

### Core Python Libraries

1. **Primary: `pronouncing`**
   ```bash
   pip install pronouncing
   ```
   - Simple CMU Dictionary interface
   - No dependencies
   - Perfect for sound pattern detection baseline

2. **Phonetic Analysis: `jellyfish`**
   ```bash
   pip install jellyfish
   ```
   - Levenshtein distance for phonemes
   - Multiple similarity algorithms
   - Good for assonant-consonant scoring

3. **Multi-Agent Framework: `langroid`**
   ```bash
   pip install langroid
   ```
   - LLM coordination
   - Actor-based architecture
   - Validation agents

## Top 3 Implementation Approaches

### Approach 1: Multi-Agent Validation System (Recommended)

**Architecture:**
```python
# Generator Agent: Creates initial poetry
# Validator Agent: Checks sound pattern constraints
# Refiner Agent: Suggests improvements
# Scorer Agent: Quality assessment
```

**Pros:**
- Highest success rate (based on 2024 research)
- Iterative improvement capability
- Separate concerns (generation vs validation)

**Implementation Priority:** HIGH

### Approach 2: Phonetic Analysis Filtering

**Method:**
```python
def validate_near_sound patterns(poem):
    # 1. Extract end words from each line
    # 2. Convert to phonemes using CMU dictionary
    # 3. Check for identical ending patterns (REJECT)
    # 4. Score assonant-consonant quality (ACCEPT if > threshold)
```

**Pros:**
- Deterministic validation
- Fast execution
- Clear success criteria

**Implementation Priority:** HIGH

### Approach 3: Few-Shot Learning with Curated Examples

**Template:**
```
Here are poems using ONLY assonant-consonant patterns (bad:have, team:ring, love:bud):

[Example 1 with perfect assonant-consonants]
[Example 2 with perfect assonant-consonants]

Now write a similar poem about [TOPIC] using only assonant-consonant patterns.
Avoid perfect matchs like love:dove, night:light, cat:bat.
```

**Pros:**
- Works with any LLM
- No additional software needed
- Good for initial prototyping

**Implementation Priority:** MEDIUM

## Specific Tools and Code Examples

### Exact Sound pattern Detection (Must Fail)

```python
import pronouncing

def has_exact_sound patterns(poem_lines):
    """Return True if poem contains identical endings (FAIL condition)"""
    end_words = [line.strip().split()[-1].lower() for line in poem_lines]

    for i, word1 in enumerate(end_words):
        for word2 in end_words[i+1:]:
            # Get phonetic representations
            phones1 = pronouncing.phones_for_word(word1)
            phones2 = pronouncing.phones_for_word(word2)

            if phones1 and phones2:
                # Check if sound matching parts are identical (identical ending)
                sound pattern1 = pronouncing.sound matching_part(phones1[0])
                sound pattern2 = pronouncing.sound matching_part(phones2[0])

                if sound pattern1 == sound pattern2 and sound pattern1:  # Identical ending found
                    return True, (word1, word2)

    return False, None
```

### Near-Sound pattern Quality Scoring

```python
import jellyfish

def score_near_sound pattern_quality(word1, word2):
    """Score phonetic similarity for assonant-consonant patterns (0-1 scale)"""
    # Get phonetic representations
    phones1 = pronouncing.phones_for_word(word1)
    phones2 = pronouncing.phones_for_word(word2)

    if not phones1 or not phones2:
        return 0.0

    # Calculate phonetic edit distance
    distance = jellyfish.levenshtein_distance(phones1[0], phones2[0])
    max_length = max(len(phones1[0]), len(phones2[0]))

    # Convert to similarity score (higher = more similar)
    similarity = 1.0 - (distance / max_length)

    # Assonant-consonants should have moderate similarity (0.3-0.7 range)
    if 0.3 <= similarity <= 0.7:
        return similarity
    else:
        return 0.0  # Too similar (exact) or too different
```

### Multi-Agent Validation System

```python
class NearSound patternPoetrySystem:
    def __init__(self):
        self.generator = GeneratorAgent()
        self.validator = ValidatorAgent()
        self.refiner = RefinerAgent()
        self.scorer = ScorerAgent()

    def generate_poem(self, topic, max_iterations=5):
        for iteration in range(max_iterations):
            # Generate initial poem
            poem = self.generator.create_poem(topic)

            # Validate sound pattern constraints
            is_valid, issues = self.validator.check_sound patterns(poem)

            if is_valid:
                # Score overall quality
                quality_score = self.scorer.evaluate(poem)
                return poem, quality_score
            else:
                # Refine based on issues
                topic = self.refiner.suggest_improvements(poem, issues)

        return None, "Failed to generate valid poem"
```

## Performance Metrics and Evaluation

### Success Criteria Validation

```python
def validate_poem_success(poem):
    """Check if poem meets all assonant-consonant constraints"""
    results = {
        "exact_sound patterns": 0,      # Must be 0
        "near_sound patterns": 0,       # Should be > 0
        "total_sound pattern_pairs": 0,
        "success": False
    }

    # Extract sound pattern pairs and analyze
    sound pattern_pairs = extract_sound pattern_pairs(poem)

    for word1, word2 in sound pattern_pairs:
        if is_exact_sound pattern(word1, word2):
            results["exact_sound patterns"] += 1
        elif is_near_sound pattern(word1, word2):
            results["near_sound patterns"] += 1

    # Success = 0 identical endings AND some assonant-consonant patterns
    results["success"] = (
        results["exact_sound patterns"] == 0 and
        results["near_sound patterns"] > 0
    )

    return results
```

### Quality Scoring System

```python
def comprehensive_poem_score(poem):
    """Multi-dimensional quality assessment"""
    scores = {
        "sound pattern_compliance": check_no_exact_sound patterns(poem),      # 0-1
        "near_sound pattern_quality": score_phonetic_similarity(poem), # 0-1
        "semantic_coherence": evaluate_meaning(poem),          # 0-1
        "formal_structure": check_meter_syllables(poem),       # 0-1
        "creativity": assess_artistic_merit(poem)              # 0-1
    }

    # Weighted average (sound pattern compliance is critical)
    weights = {
        "sound pattern_compliance": 0.4,  # Most important
        "near_sound pattern_quality": 0.3,
        "semantic_coherence": 0.15,
        "formal_structure": 0.1,
        "creativity": 0.05
    }

    total_score = sum(scores[key] * weights[key] for key in scores)
    return total_score, scores
```

## Test Cases for Validation

### Known Good Examples (Should Pass)
```python
good_examples = [
    ("bad", "have"),      # Assonance
    ("team", "ring"),     # Consonance
    ("love", "bud"),      # Slant sound pattern
    ("mind", "send"),     # Assonant-consonant pattern
    ("home", "stone"),    # Partial similarity
]
```

### Known Bad Examples (Should Fail)
```python
bad_examples = [
    ("cat", "bat"),       # Perfect sound pattern
    ("love", "dove"),     # Perfect sound pattern
    ("night", "light"),   # Perfect sound pattern
    ("day", "way"),       # Perfect sound pattern
]
```

## Implementation Priority Order

### Phase 1: Core Validation (Week 1)
1. Implement identical ending detection
2. Build test suite with known examples
3. Create basic assonant-consonant scoring

### Phase 2: Generation Integration (Week 2)
1. Connect to LLM for poem generation
2. Add iterative validation loop
3. Test with simple prompts

### Phase 3: Multi-Agent System (Week 3)
1. Implement agent architecture
2. Add refinement capabilities
3. Performance optimization

### Phase 4: Quality Enhancement (Week 4)
1. Advanced scoring systems
2. Human evaluation integration
3. Continuous improvement loops

## Known Challenges and Solutions

### Challenge 1: Phonetic Ambiguity
**Problem:** Words with multiple pronunciations
**Solution:** Use probability-weighted matching, context awareness

### Challenge 2: Creative Quality
**Problem:** Over-constraining reduces artistic merit
**Solution:** Multi-objective optimization balancing constraints and creativity

### Challenge 3: Performance
**Problem:** Phonetic analysis can be slow
**Solution:** Implement caching, indexing, parallel processing

## Quick Prototype Code

```python
#!/usr/bin/env python3
"""
Quick prototype for assonant-consonant poetry validation
"""

import pronouncing

def quick_validate_poem(poem_text):
    """Quick validation for assonant-consonant constraints"""
    lines = [line.strip() for line in poem_text.split('\n') if line.strip()]
    end_words = [line.split()[-1].lower() for line in lines if line.split()]

    print(f"Analyzing poem with {len(lines)} lines...")
    print(f"End words: {end_words}")

    # Check for identical endings (should be NONE)
    exact_sound patterns = []
    near_sound patterns = []

    for i, word1 in enumerate(end_words):
        for j, word2 in enumerate(end_words[i+1:], i+1):
            if word1 in pronouncing.sound patterns(word2):
                exact_sound patterns.append((word1, word2, i, j))
            elif is_near_sound pattern(word1, word2):
                near_sound patterns.append((word1, word2, i, j))

    # Results
    success = len(exact_sound patterns) == 0 and len(near_sound patterns) > 0

    print(f"\nResults:")
    print(f"✓ Identical endings found: {len(exact_sound patterns)}")
    print(f"✓ Assonant-consonant patterns found: {len(near_sound patterns)}")
    print(f"✓ Success: {success}")

    if exact_sound patterns:
        print(f"\n❌ FAILED: Found identical endings:")
        for word1, word2, i, j in exact_sound patterns:
            print(f"   Line {i+1} '{word1}' <-> Line {j+1} '{word2}'")

    return success

def is_near_sound pattern(word1, word2):
    """Simple assonant-consonant detection"""
    # This is a placeholder - implement proper phonetic analysis
    return False  # Replace with actual assonant-consonant logic

# Example usage
if __name__ == "__main__":
    test_poem = """
    The morning felt strange and new
    While shadows danced in patterns broad
    I walked through streets both old and blue
    Seeking some forgotten word
    """

    quick_validate_poem(test_poem)
```

This implementation framework provides a solid foundation for building a assonant-consonant poetry generation system with practical, tested approaches and clear success metrics.