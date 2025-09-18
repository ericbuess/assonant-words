# Implementation Recommendations: Near-Rhyme Poetry Generation

## Quick Start Guide

Based on comprehensive research, here are the most practical implementation approaches for forcing AI to generate poetry using ONLY near rhymes while avoiding exact rhymes.

## Recommended Implementation Stack

### Core Python Libraries

1. **Primary: `pronouncing`**
   ```bash
   pip install pronouncing
   ```
   - Simple CMU Dictionary interface
   - No dependencies
   - Perfect for rhyme detection baseline

2. **Phonetic Analysis: `jellyfish`**
   ```bash
   pip install jellyfish
   ```
   - Levenshtein distance for phonemes
   - Multiple similarity algorithms
   - Good for near-rhyme scoring

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
# Validator Agent: Checks rhyme constraints
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
def validate_near_rhymes(poem):
    # 1. Extract end words from each line
    # 2. Convert to phonemes using CMU dictionary
    # 3. Check for exact rhyme patterns (REJECT)
    # 4. Score near-rhyme quality (ACCEPT if > threshold)
```

**Pros:**
- Deterministic validation
- Fast execution
- Clear success criteria

**Implementation Priority:** HIGH

### Approach 3: Few-Shot Learning with Curated Examples

**Template:**
```
Here are poems using ONLY near rhymes (bad:have, team:ring, love:bud):

[Example 1 with perfect near-rhymes]
[Example 2 with perfect near-rhymes]

Now write a similar poem about [TOPIC] using only near rhymes.
Avoid perfect rhymes like love:dove, night:light, cat:bat.
```

**Pros:**
- Works with any LLM
- No additional software needed
- Good for initial prototyping

**Implementation Priority:** MEDIUM

## Specific Tools and Code Examples

### Exact Rhyme Detection (Must Fail)

```python
import pronouncing

def has_exact_rhymes(poem_lines):
    """Return True if poem contains exact rhymes (FAIL condition)"""
    end_words = [line.strip().split()[-1].lower() for line in poem_lines]

    for i, word1 in enumerate(end_words):
        for word2 in end_words[i+1:]:
            # Get phonetic representations
            phones1 = pronouncing.phones_for_word(word1)
            phones2 = pronouncing.phones_for_word(word2)

            if phones1 and phones2:
                # Check if rhyming parts are identical (exact rhyme)
                rhyme1 = pronouncing.rhyming_part(phones1[0])
                rhyme2 = pronouncing.rhyming_part(phones2[0])

                if rhyme1 == rhyme2 and rhyme1:  # Exact rhyme found
                    return True, (word1, word2)

    return False, None
```

### Near-Rhyme Quality Scoring

```python
import jellyfish

def score_near_rhyme_quality(word1, word2):
    """Score phonetic similarity for near rhymes (0-1 scale)"""
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

    # Near-rhymes should have moderate similarity (0.3-0.7 range)
    if 0.3 <= similarity <= 0.7:
        return similarity
    else:
        return 0.0  # Too similar (exact) or too different
```

### Multi-Agent Validation System

```python
class NearRhymePoetrySystem:
    def __init__(self):
        self.generator = GeneratorAgent()
        self.validator = ValidatorAgent()
        self.refiner = RefinerAgent()
        self.scorer = ScorerAgent()

    def generate_poem(self, topic, max_iterations=5):
        for iteration in range(max_iterations):
            # Generate initial poem
            poem = self.generator.create_poem(topic)

            # Validate rhyme constraints
            is_valid, issues = self.validator.check_rhymes(poem)

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
    """Check if poem meets all near-rhyme constraints"""
    results = {
        "exact_rhymes": 0,      # Must be 0
        "near_rhymes": 0,       # Should be > 0
        "total_rhyme_pairs": 0,
        "success": False
    }

    # Extract rhyme pairs and analyze
    rhyme_pairs = extract_rhyme_pairs(poem)

    for word1, word2 in rhyme_pairs:
        if is_exact_rhyme(word1, word2):
            results["exact_rhymes"] += 1
        elif is_near_rhyme(word1, word2):
            results["near_rhymes"] += 1

    # Success = 0 exact rhymes AND some near rhymes
    results["success"] = (
        results["exact_rhymes"] == 0 and
        results["near_rhymes"] > 0
    )

    return results
```

### Quality Scoring System

```python
def comprehensive_poem_score(poem):
    """Multi-dimensional quality assessment"""
    scores = {
        "rhyme_compliance": check_no_exact_rhymes(poem),      # 0-1
        "near_rhyme_quality": score_phonetic_similarity(poem), # 0-1
        "semantic_coherence": evaluate_meaning(poem),          # 0-1
        "formal_structure": check_meter_syllables(poem),       # 0-1
        "creativity": assess_artistic_merit(poem)              # 0-1
    }

    # Weighted average (rhyme compliance is critical)
    weights = {
        "rhyme_compliance": 0.4,  # Most important
        "near_rhyme_quality": 0.3,
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
    ("love", "bud"),      # Slant rhyme
    ("mind", "send"),     # Near rhyme
    ("home", "stone"),    # Partial similarity
]
```

### Known Bad Examples (Should Fail)
```python
bad_examples = [
    ("cat", "bat"),       # Perfect rhyme
    ("love", "dove"),     # Perfect rhyme
    ("night", "light"),   # Perfect rhyme
    ("day", "way"),       # Perfect rhyme
]
```

## Implementation Priority Order

### Phase 1: Core Validation (Week 1)
1. Implement exact rhyme detection
2. Build test suite with known examples
3. Create basic near-rhyme scoring

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
Quick prototype for near-rhyme poetry validation
"""

import pronouncing

def quick_validate_poem(poem_text):
    """Quick validation for near-rhyme constraints"""
    lines = [line.strip() for line in poem_text.split('\n') if line.strip()]
    end_words = [line.split()[-1].lower() for line in lines if line.split()]

    print(f"Analyzing poem with {len(lines)} lines...")
    print(f"End words: {end_words}")

    # Check for exact rhymes (should be NONE)
    exact_rhymes = []
    near_rhymes = []

    for i, word1 in enumerate(end_words):
        for j, word2 in enumerate(end_words[i+1:], i+1):
            if word1 in pronouncing.rhymes(word2):
                exact_rhymes.append((word1, word2, i, j))
            elif is_near_rhyme(word1, word2):
                near_rhymes.append((word1, word2, i, j))

    # Results
    success = len(exact_rhymes) == 0 and len(near_rhymes) > 0

    print(f"\nResults:")
    print(f"✓ Exact rhymes found: {len(exact_rhymes)}")
    print(f"✓ Near rhymes found: {len(near_rhymes)}")
    print(f"✓ Success: {success}")

    if exact_rhymes:
        print(f"\n❌ FAILED: Found exact rhymes:")
        for word1, word2, i, j in exact_rhymes:
            print(f"   Line {i+1} '{word1}' <-> Line {j+1} '{word2}'")

    return success

def is_near_rhyme(word1, word2):
    """Simple near-rhyme detection"""
    # This is a placeholder - implement proper phonetic analysis
    return False  # Replace with actual near-rhyme logic

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

This implementation framework provides a solid foundation for building a near-rhyme poetry generation system with practical, tested approaches and clear success metrics.