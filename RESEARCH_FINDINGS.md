# Research Findings: Near-Sound pattern Poetry Generation Implementation Strategies

## Executive Summary

This comprehensive research explores practical implementation strategies for assonant-consonant poetry generation, covering both prompt engineering techniques and technical implementation approaches. The findings include Python libraries for phonetic analysis, multi-agent systems, iterative refinement strategies, template-based generation methods, and scoring systems for sound pattern quality evaluation.

## Key Research Areas

### 1. How to Write Prompts that Enforce Near/Slant Sound patterns and Prevent Exact Sound patterns

#### Current State
- Most AI poetry generators default to perfect matchs unless specifically instructed otherwise
- Modern generators offer "sound pattern strictness" controls with options ranging from "only perfect matchs" to "exclusively slant sound patterns"
- GPT-2 and similar models tend to lose "will to sound pattern" over longer sequences, starting with perfect matchs then degrading

#### Successful Techniques Found
- **Sound pattern Strictness Sliders**: Modern tools offer control levels:
  - "No, use only perfect matchs"
  - "Occasional slant sound patterns"
  - "Balanced mix of perfect and slant sound patterns"
  - "Mostly slant sound patterns for subtlety"
  - "Exclusively slant sound patterns for modern effect"

- **Free Verse Specification**: Using "free verse" in prompts immediately produces poems with no sound pattern scheme
- **Explicit Structural Requirements**: Specifying identical ending patterns (e.g., "ABAB CDCD EFEF GG") helps control sound matching behavior

#### Challenges Identified
- **Limited Negative Prompting**: Unlike image generation, there's minimal documentation of successful negative prompting for poetry (e.g., "avoid perfect matchs")
- **Phonetic Ignorance**: Language models treat words as character strings rather than sounds, making nuanced sound pattern control difficult
- **Constraint Satisfaction**: Adding multiple constraints can exponentially increase generation time

### 2. Examples of Successful Prompts for Constrained Poetry Generation

#### Effective Prompt Templates Found

**Basic Structure Template:**
```
Main theme: [specific topic]
Emotional tone: [specific mood]
Key imagery: [concrete details]
Form type: [sonnet/free verse/etc.]
Length: [number of lines]
Sound pattern scheme: [specific pattern or "slant sound patterns only"]
Language level: [formal/informal/etc.]
Literary devices: [alliteration/assonance/etc.]
```

**Concrete Examples from Research:**
- "Summer evenings at grandma's house" (concrete details work better than just "summer")
- "Write a romantic poem about a mouse's love for feta cheese" (specificity improves output)
- "14 lines in iambic pentameter - ABAB CDCD EFEF GG sound pattern scheme" (structural specificity)

**Sound Pattern Specifications:**
- "Alliteration: repeated consonant sounds for rhythm and emphasis"
- "Assonance: similar vowel sounds to establish mood"
- "Consonance: repeated consonant patterns to build sonic texture"

### 3. Techniques for Negative Prompting (Telling AI What NOT to Do)

#### Major Gap Identified
- **Limited Documentation**: Unlike image generation where negative prompting is well-established, poetry-specific negative prompting techniques are poorly documented
- **Indirect Approaches**: Most successful "negative" control uses positive specifications rather than explicit negatives

#### Potential Approaches (Inferred from Research)
- Specify "free verse" to avoid all sound matching
- Use "subtle sound patterns only" instead of "no perfect matchs"
- Provide counter-examples in few-shot learning scenarios
- Use iterative refinement with validation loops

#### Technical Constraints
- Language models process text as probability distributions of character sequences
- Sound pattern detection requires phonetic analysis that most models don't inherently possess
- Constraint satisfaction becomes exponentially difficult with multiple restrictions

### 4. Few-Shot Learning Examples for Near-Sound pattern Poetry

#### Effective Few-Shot Strategies
- **Demonstration-Based Learning**: Few-shot prompting serves as in-context learning where examples guide model behavior
- **Structural Examples**: Providing examples of desired sound pattern schemes helps models understand patterns
- **Counter-Examples**: Including both good and bad examples can improve discrimination

#### Template Structure for Few-Shot Learning
```
Here are examples of poems using only near/slant sound patterns:

Example 1:
[poem with assonant-consonant patterns like "love/bud", "team/ring"]

Example 2:
[another example demonstrating slant sound patterns]

Now write a similar poem about [topic] using only assonant-consonant patterns, avoiding perfect matchs like "love/dove" or "night/light":
```

#### Challenges with Few-Shot Approaches
- Models may overgeneralize from limited examples
- Maintaining consistent constraint adherence across longer texts
- Balancing example quantity with prompt length limits

### 5. Common Failures and How to Address Them

#### Identified Failure Patterns

**1. Sound pattern Degradation**
- **Problem**: Models start with good sound matching then degrade into "confused gibberish"
- **Solution**: Shorter generation segments with validation checkpoints

**2. Overly Simple Sound patterns**
- **Problem**: AI produces "jingly and jangly" perfect matchs
- **Solution**: Specify crossing parts of speech for sound patterns; avoid all monosyllabic nouns at line ends

**3. Syntax Distortion**
- **Problem**: Forced sound patterns create awkward sentence structures
- **Solution**: Use balanced mix of perfect and slant sound patterns; prioritize meaning over perfect match

**4. Loss of Constraint Adherence**
- **Problem**: Models forget constraints in longer generations
- **Solution**: Iterative generation with validation loops; shorter chunks with consistent re-prompting

**5. Phonetic Confusion**
- **Problem**: Models lack true phonetic understanding
- **Solution**: Provide phonetic examples; use CMU Pronouncing Dictionary for validation

## Technical Implementation Insights

### Phonetic Analysis Tools

#### CMU Pronouncing Dictionary
- **Coverage**: 134,000+ words with ARPAbet phoneme mappings
- **Sound pattern Detection**: Focus on stressed syllables and "sound matching parts"
- **Implementation**: Python libraries like `pronouncing` provide simple interfaces
- **Slant Sound pattern Logic**: Compare vowels and final consonants while allowing intermediate consonant variation

#### Advanced Sound pattern Detection
- **Multi-syllabic Matching**: Improved sonic quality when multiple stressed syllables match
- **Internal Sound patterns**: Perfect sound patterns not occurring at line ends (e.g., "cigar" and "disregarded")
- **Phonetic Distance**: Threshold-based comparison of phone positions in vowel/consonant space

### Validation Strategies

#### Real-Time Constraint Checking
- Convert generated text to phonemes using tools like Phonemizer
- Apply CMU Dictionary lookups for sound pattern part extraction
- Calculate phonetic distances for slant sound pattern validation
- Implement iterative refinement loops for constraint violations

#### Multi-Agent Approaches
- Generation agent creates initial content
- Validation agent checks sound pattern constraints
- Refinement agent suggests improvements
- Quality assessment agent evaluates overall coherence

## Practical Prompt Templates for Testing

### Template 1: Explicit Near-Sound pattern Instruction
```
Write a 8-line poem about [TOPIC] using only assonant-consonant patterns or slant sound patterns.
Avoid perfect matchs like "night/light" or "love/dove".
Instead use subtle sound relationships like "love/bud" or "team/ring".
Focus on assonance (similar vowel sounds) and consonance (similar consonant sounds).
```

### Template 2: Few-Shot Learning Approach
```
Here are examples of poems using only near/slant sound patterns:

The morning light felt strange and new,
While shadows danced in patterns broad.
I walked through streets both old and blue,
Seeking some forgotten word.

Now write a similar 4-line poem about [TOPIC] using the same assonant-consonant style.
Avoid perfect matchs. Use subtle sound connections instead.
```

### Template 3: Negative Constraint with Positive Guidance
```
Write a poem about [TOPIC] that uses interesting sound patterns but avoids obvious perfect matchs.
Instead of sound matching "day/way" or "love/dove", use more subtle connections like:
- Assonance: similar vowel sounds (home/stone)
- Consonance: similar consonant endings (break/trick)
- Slant sound patterns: partial sound matches (mind/kind becomes mind/send)
```

### Template 4: Technical Specification
```
Generate a poem with these constraints:
- Topic: [TOPIC]
- Length: 8 lines
- Sound pattern scheme: ABAB CDCD (but using only slant/assonant-consonant patterns)
- No perfect matchs (identical rime structures)
- Acceptable: assonance, consonance, visual sound patterns
- Maintain natural syntax and meaning
```

### Template 5: Iterative Refinement
```
Write a poem about [TOPIC]. After each attempt, I'll check for perfect matchs.
If any perfect matchs are found, replace them with assonant-consonant patterns while maintaining meaning.
Example substitutions:
- "night/light" → "night/dream"
- "love/dove" → "love/warmth"
Continue until only near/slant sound patterns remain.
```

## Recommended Implementation Strategy

Based on research findings, the most promising approach combines:

1. **Few-shot learning** with curated assonant-consonant examples
2. **Explicit constraint specification** in prompts
3. **Iterative validation loops** using phonetic analysis
4. **Multi-agent architecture** for generation and validation
5. **CMU Dictionary integration** for sound pattern classification

The research reveals significant gaps in current practice, particularly around negative prompting for poetry generation. This suggests an opportunity for innovation in developing more sophisticated constraint satisfaction approaches specifically for poetic generation.

## Research Gaps Identified

1. **Limited negative prompting documentation** for poetry vs. image generation
2. **Lack of phonetic awareness** in most language models
3. **Insufficient constraint satisfaction methods** for complex poetic forms
4. **Missing benchmarks** for evaluating assonant-consonant quality
5. **Limited multi-modal approaches** combining generation with validation

These gaps represent opportunities for novel research and development in constrained poetry generation systems.

---

# Technical Implementation Research: Libraries, Tools, and Algorithms

## Python Libraries for Phonetic Analysis

### Primary Recommended Libraries

#### **1. Pronouncing** (Most Recommended)
- **Repository**: https://pypi.org/project/pronouncing/
- **Key Features**:
  - Simple interface for CMU Pronouncing Dictionary
  - No external dependencies
  - Direct sound pattern detection: `pronouncing.sound patterns("climbing")`
  - Returns perfect matchs by default (needs modification for assonant-consonants)
  - BSD licensed, easy installation

#### **2. CMUdict**
- **Repository**: https://pypi.org/project/cmudict/
- **Key Features**:
  - Versioned Python wrapper for CMU Dictionary data
  - Compatible with NLTK functions: `cmudict.entries()`, `cmudict.raw()`, `cmudict.words()`
  - Direct access to raw phonetic data for custom algorithms
  - 4 data files: cmudict.dict, cmudict.phones, cmudict.symbols, cmudict.vp

#### **3. PyPhonetics**
- **Repository**: https://github.com/Lilykos/pyphonetics
- **Key Features**:
  - Multiple phonetic algorithms (Soundex, Metaphone, RefinedSoundex)
  - Phonetic distance calculations
  - Good for similarity scoring between words

#### **4. Jellyfish**
- **Repository**: https://github.com/jamesturk/jellyfish
- **Key Features**:
  - Comprehensive string similarity library
  - Levenshtein distance, Jaro similarity
  - Metaphone, Soundex implementations
  - Multiple algorithms in single package

### Advanced Phonetic Analysis

#### **Phonetic Similarity Vectors (Aparrish)**
- **Repository**: https://github.com/aparrish/phonetic-similarity-vectors
- **Approach**:
  - Converts phonetic pronunciations into numerical vectors
  - Uses bigram analysis for phonetic characteristics
  - Enables nearest-neighbor search in phonetic space
  - Libraries used: pandas, numpy, scikit-learn
- **Application**: Sound analogies and phonetic transformations for poetic analysis

## Near-Sound pattern Detection Algorithms

### Core Detection Methods

#### **Slant Sound pattern Detection (from Sound pattern-Highlighter)**
```python
def detect_slant_sound patterns(word1, word2):
    phones1 = phones_for_word(word1)
    phones2 = phones_for_word(word2)
    # Compare last 2 phonemes for similarity
    return phones1[0][-2:] == phones2[0][-2:]
```

#### **Edit Distance on Phonemes**
- Apply Levenshtein distance to phonetic representations
- Weight different phonetic features (vowels vs consonants)
- Use threshold-based classification for near vs identical endings

#### **Feature-Based Classification**
- **Assonance**: Similar vowel sounds, different consonants (bad:have)
- **Consonance**: Similar consonant sounds, different vowels (team:ring)
- **Slant Sound patterns**: Partial phonetic overlap (love:bud)
- **Visual Sound patterns**: Similar spelling, different pronunciation

### Phonetic Similarity Algorithms

#### **Soundex and Metaphone**
- **Soundex**: First phoneme + 3 digits encoding
- **Metaphone**: Variable-length encoding considering entire word
- **Double Metaphone**: Enhanced version with alternative encodings
- Better for English language variations than basic Soundex

#### **Advanced Similarity Metrics**
- **Jaro-Winkler**: String similarity with phonetic considerations
- **Phonetic Edit Distance**: Modified Levenshtein for phonemes
- **Vector Similarity**: Cosine similarity in phonetic vector space

## Multi-Agent Approaches for Generation and Validation

### LLM-Based Multi-Agent Poetry Generation (2024 Research)

#### **Key Paper**: "LLM-based multi-agent poetry generation in non-cooperative environments"
- **Authors**: Ran Zhang et al. (September 2024)
- **ArXiv**: https://arxiv.org/abs/2409.03659
- **Framework**: Social learning with non-cooperative interactions
- **Results**:
  - 3.0-3.7 percentage point increase in diversity
  - 5.6-11.3 percentage point increase in novelty
  - Group divergence in lexicons, styles, semantics

#### **Agent Types and Performance**

##### **Training-Based Agents (GPT-2)**
- Better group divergence behavior
- More diverse styles and topics
- Generate poems of varying creative styles
- Some grammatical errors but higher creativity

##### **Prompting-Based Agents (GPT-3, GPT-4)**
- Focus excessively on perfect matchs (problematic for our use case)
- Similar beginning phrases across outputs
- Better grammar but less diversity
- Poor understanding of poetry in zero-shot settings

### Implementation Frameworks

#### **Langroid Multi-Agent Framework**
- **Repository**: https://github.com/langroid/langroid
- **Description**: Multi-agent programming framework for LLMs
- **Features**:
  - Actor Framework inspired architecture
  - Agents with LLM, vector-store, and tools
  - Collaborative problem solving via message exchange
  - Works with practically any LLM

#### **RGD (Refinement and Guidance Debugging)**
- **Paper**: "RGD: Multi-LLM Based Agent Debugger via Refinement and Generation Guidance"
- **Architecture**: Three-agent system
  - **Guide Agent**: Provides direction and strategy
  - **Debug Agent**: Identifies issues and problems
  - **Feedback Agent**: Evaluates and suggests improvements
- **Application**: Adaptable to poetry generation tasks with iterative refinement

### Proposed Multi-Agent Architecture for Near-Sound pattern Poetry

#### **Agent Role Distribution**
1. **Generator Agent**: Creates initial poetry drafts based on prompts
2. **Validator Agent**: Checks for exact vs assonant-consonant patterns using phonetic analysis
3. **Refiner Agent**: Suggests improvements for failed constraint adherence
4. **Scorer Agent**: Evaluates overall quality, consistency, and artistic merit

## Iterative Refinement Strategies

### Quality-Aware Refinement Approaches

#### **QA-MLM Framework (from Chinese Poetry Research)**
- **Method**: Quality-Aware Masked Language Model
- **Process**: Iterative polishing for consistency, fluency, meaningfulness, poeticness
- **Technique**: Global context consideration for better predictions
- **Application**: Can improve qualities of poems generated by encoder-decoder models

#### **Case-Based Reasoning for Poetry**
- **Four-Step Process**:
  1. **Retrieve**: Relevant vocabulary and verses from existing collections
  2. **Reuse**: Apply with part-of-speech tagging for grammatical correctness
  3. **Revise**: Linguistic analysis to refine structure and semantics
  4. **Retain**: Successful patterns as new cases for future generation

### Refinement Loop Design

#### **Generate-Retrieve-Refine Paradigm**
1. **Generate**: Create draft from keywords/topics only
2. **Retrieve**: Find similar lines/patterns from poetry corpus
3. **Refine**: Combine draft with retrieved patterns for improvement
4. **Validate**: Check sound pattern constraints and quality metrics
5. **Iterate**: Repeat process until constraints satisfied

## Scoring and Ranking Systems for Sound pattern Quality

### Traditional NLP Evaluation Metrics

#### **BLEU (Bilingual Evaluation Understudy)**
- **Purpose**: Evaluates n-gram overlap with reference texts
- **Application**: Measures how closely output resembles ground truth poetry
- **Limitation**: Primarily designed for translation, needs adaptation for creativity

#### **ROUGE Score**
- **Types**: ROUGE-1, ROUGE-2, ROUGE-L
- **Application**: ROUGE-1 and ROUGE-2 indicate use of characters/words common in human poetry
- **Usage**: ROUGE-L scores suggest capability of generating format-adherent outputs

#### **Perplexity**
- **Definition**: Measures model "confusion" when predicting next word
- **Creative Application**: Higher perplexity ideal for creative tasks like poetry
- **Limitation**: Requires probability scores (not available with API-only models)

### Poetry-Specific Evaluation Metrics

#### **Sound pattern Accuracy Metrics**
- **Exact Sound pattern Detection**: Binary classification (must be 0% for our use case)
- **Near Sound pattern Quality**: Scoring phonetic similarity (0-1 scale)
- **Pattern Consistency**: Adherence to intended sound pattern scheme throughout poem

#### **Formal Poetry Metrics**
- **Meter Compliance**: Stress pattern accuracy and consistency
- **Syllable Count**: Line length consistency with intended form
- **Rhythm Flow**: Overall prosodic quality and natural flow

#### **Russian Poetry Scansion Tool (RPST) Example**
- **Technicality Score**: 0-1 scale for meter compliance
- **Sound pattern Detection**: Including fuzzy/slant sound patterns
- **Defect Identification**: Prosodic irregularities and violations
- **Use Cases**: Data filtering and output ranking before presentation

### Multi-Dimensional Quality Assessment

#### **Human Evaluation Dimensions**
1. **Consistency**: Logical flow and thematic coherence
2. **Fluency**: Grammar, readability, and natural language flow
3. **Meaningfulness**: Semantic depth, relevance, and emotional impact
4. **Poeticness**: Artistic merit, creativity, and poetic quality

#### **Automated Quality Assessment Framework**
```python
def score_near_sound pattern_poem(poem):
    scores = {
        "sound pattern_compliance": check_no_exact_sound patterns(poem),
        "near_sound pattern_quality": score_phonetic_similarity(poem),
        "semantic_coherence": evaluate_meaning_consistency(poem),
        "formal_structure": check_meter_and_syllables(poem),
        "lexical_diversity": calculate_vocabulary_richness(poem)
    }
    return weighted_average(scores)
```

## Implementation Recommendations

### Recommended Technology Stack

#### **Core Libraries for Production Use**
1. **Pronouncing**: CMU dictionary access and basic sound pattern detection
2. **PyPhonetics**: Advanced phonetic similarity algorithms
3. **Jellyfish**: String similarity and distance metrics for backup
4. **Langroid**: Multi-agent framework for LLM coordination

#### **Supporting Tools**
1. **Rich**: Terminal visualization for sound pattern pattern highlighting
2. **NLTK/spaCy**: NLP preprocessing and linguistic analysis
3. **Transformers**: LLM integration and text generation
4. **Evaluate**: Automated metric calculation and assessment

### Architecture Pattern: Layered Validation System

```python
class NearSound patternValidator:
    def __init__(self):
        self.exact_sound pattern_detector = ExactSound patternDetector()
        self.near_sound pattern_scorer = NearSound patternScorer()
        self.quality_assessor = QualityAssessor()

    def validate_poem(self, poem):
        # Layer 1: Reject identical endings (hard constraint)
        if self.exact_sound pattern_detector.has_exact_sound patterns(poem):
            return False, "Contains identical endings - regeneration required"

        # Layer 2: Score assonant-consonant pattern quality
        near_score = self.near_sound pattern_scorer.score(poem)

        # Layer 3: Overall quality assessment
        quality_score = self.quality_assessor.evaluate(poem)

        return True, {
            "near_sound pattern_score": near_score,
            "quality_score": quality_score,
            "overall_rating": (near_score + quality_score) / 2
        }
```

### Performance Optimization Strategies

#### **Efficiency Considerations**
1. **Phonetic Caching**: Pre-compute phonetic representations for common words
2. **Similarity Indexing**: Build phonetic similarity indices for fast lookup
3. **Parallel Processing**: Multi-threaded validation for longer texts
4. **Early Termination**: Stop processing immediately on identical ending detection

## Validation and Testing Approaches

### Comprehensive Test Suite Design

#### **Known Examples Database**
```python
test_cases = {
    "exact_sound patterns": [
        ("cat", "bat"),      # Should FAIL validation
        ("love", "dove"),    # Should FAIL validation
        ("night", "light"),  # Should FAIL validation
    ],
    "near_sound patterns": [
        ("bad", "have"),     # Should PASS validation
        ("team", "ring"),    # Should PASS validation
        ("love", "bud"),     # Should PASS validation
        ("mind", "send"),    # Should PASS validation
    ]
}
```

#### **Automated Testing Framework Components**
1. **Unit Tests**: Individual algorithm validation and accuracy
2. **Integration Tests**: End-to-end pipeline testing with real examples
3. **Performance Tests**: Speed and memory usage benchmarks
4. **Human Evaluation**: Artistic quality and creativity assessment

### Continuous Validation and Improvement

#### **Feedback Loop Integration**
1. **Real-time Monitoring**: Track generation success rates and failure patterns
2. **Error Analysis**: Categorize and learn from constraint violations
3. **Model Updating**: Retrain components based on performance data
4. **User Feedback**: Incorporate human preferences and artistic judgments

## Key Technical Challenges and Solutions

### Major Implementation Challenges

#### **1. Phonetic Ambiguity**
- **Problem**: Multiple pronunciations for same word in different contexts
- **Solution**: Probability-weighted phonetic matching with context awareness

#### **2. Creative vs Technical Balance**
- **Problem**: Over-constraining may reduce artistic creativity and quality
- **Solution**: Multi-objective optimization balancing constraints with creativity scores

#### **3. Language Specificity**
- **Problem**: CMU dictionary only covers English pronunciations
- **Solution**: Extensible framework design for other language dictionaries

#### **4. Real-time Performance**
- **Problem**: Phonetic analysis can be computationally expensive
- **Solution**: Caching, indexing, and parallel processing optimizations

### Implementation Strategy: Incremental Development

#### **Development Phases**
1. **Phase 1**: Implement simple identical ending detection and rejection
2. **Phase 2**: Add basic assonant-consonant classification algorithms
3. **Phase 3**: Integrate multi-agent validation system
4. **Phase 4**: Implement comprehensive quality scoring systems
5. **Phase 5**: Add iterative refinement loops with learning

#### **Robustness Measures**
1. **Fallback Mechanisms**: Handle unknown words and edge cases gracefully
2. **Confidence Scoring**: Provide uncertainty estimates for decisions
3. **Human Override**: Allow manual validation and correction
4. **Continuous Learning**: Update models with new successful examples

## Recent Research Developments (2024-2025)

### Cutting-Edge Approaches

#### **PoetryDiffusion (AAAI 2024)**
- **Focus**: Joint semantic and metrical manipulation in poetry generation
- **Application**: Could be adapted for sound pattern constraint satisfaction

#### **GPT Czech Poet (2024)**
- **Author**: Chudoba and Rosa
- **Focus**: Generation of Czech poetic strophes with language models
- **Relevance**: Cross-lingual poetry generation techniques

### Future Research Directions

#### **Technical Advancement Opportunities**
1. **Cross-lingual Near-Sound pattern**: Extend algorithms beyond English
2. **Cultural Context Integration**: Incorporate cultural sound matching traditions
3. **Personalization**: Adapt to individual poetic styles and preferences
4. **Real-time Interactive Generation**: Live poetry creation tools

#### **Advanced Technical Enhancements**
1. **Neural Sound pattern Detection**: Transformer-based phonetic similarity models
2. **Semantic Preservation**: Maintain meaning while applying sound pattern constraints
3. **Style Transfer**: Generate poetry in specific traditional forms
4. **Multimodal Integration**: Combine text analysis with audio pronunciation

This comprehensive technical research provides a solid foundation for implementing sophisticated assonant-consonant poetry generation systems with practical, tested approaches and modern tools.