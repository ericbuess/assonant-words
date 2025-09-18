# Research Findings: Near-Rhyme Poetry Generation Implementation Strategies

## Executive Summary

This comprehensive research explores practical implementation strategies for near-rhyme poetry generation, covering both prompt engineering techniques and technical implementation approaches. The findings include Python libraries for phonetic analysis, multi-agent systems, iterative refinement strategies, template-based generation methods, and scoring systems for rhyme quality evaluation.

## Key Research Areas

### 1. How to Write Prompts that Enforce Near/Slant Rhymes and Prevent Exact Rhymes

#### Current State
- Most AI poetry generators default to perfect rhymes unless specifically instructed otherwise
- Modern generators offer "rhyme strictness" controls with options ranging from "only perfect rhymes" to "exclusively slant rhymes"
- GPT-2 and similar models tend to lose "will to rhyme" over longer sequences, starting with perfect rhymes then degrading

#### Successful Techniques Found
- **Rhyme Strictness Sliders**: Modern tools offer control levels:
  - "No, use only perfect rhymes"
  - "Occasional slant rhymes"
  - "Balanced mix of perfect and slant rhymes"
  - "Mostly slant rhymes for subtlety"
  - "Exclusively slant rhymes for modern effect"

- **Free Verse Specification**: Using "free verse" in prompts immediately produces poems with no rhyme scheme
- **Explicit Structural Requirements**: Specifying exact rhyme patterns (e.g., "ABAB CDCD EFEF GG") helps control rhyming behavior

#### Challenges Identified
- **Limited Negative Prompting**: Unlike image generation, there's minimal documentation of successful negative prompting for poetry (e.g., "avoid perfect rhymes")
- **Phonetic Ignorance**: Language models treat words as character strings rather than sounds, making nuanced rhyme control difficult
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
Rhyme scheme: [specific pattern or "slant rhymes only"]
Language level: [formal/informal/etc.]
Literary devices: [alliteration/assonance/etc.]
```

**Concrete Examples from Research:**
- "Summer evenings at grandma's house" (concrete details work better than just "summer")
- "Write a romantic poem about a mouse's love for feta cheese" (specificity improves output)
- "14 lines in iambic pentameter - ABAB CDCD EFEF GG rhyme scheme" (structural specificity)

**Sound Pattern Specifications:**
- "Alliteration: repeated consonant sounds for rhythm and emphasis"
- "Assonance: similar vowel sounds to establish mood"
- "Consonance: repeated consonant patterns to build sonic texture"

### 3. Techniques for Negative Prompting (Telling AI What NOT to Do)

#### Major Gap Identified
- **Limited Documentation**: Unlike image generation where negative prompting is well-established, poetry-specific negative prompting techniques are poorly documented
- **Indirect Approaches**: Most successful "negative" control uses positive specifications rather than explicit negatives

#### Potential Approaches (Inferred from Research)
- Specify "free verse" to avoid all rhyming
- Use "subtle rhymes only" instead of "no perfect rhymes"
- Provide counter-examples in few-shot learning scenarios
- Use iterative refinement with validation loops

#### Technical Constraints
- Language models process text as probability distributions of character sequences
- Rhyme detection requires phonetic analysis that most models don't inherently possess
- Constraint satisfaction becomes exponentially difficult with multiple restrictions

### 4. Few-Shot Learning Examples for Near-Rhyme Poetry

#### Effective Few-Shot Strategies
- **Demonstration-Based Learning**: Few-shot prompting serves as in-context learning where examples guide model behavior
- **Structural Examples**: Providing examples of desired rhyme schemes helps models understand patterns
- **Counter-Examples**: Including both good and bad examples can improve discrimination

#### Template Structure for Few-Shot Learning
```
Here are examples of poems using only near/slant rhymes:

Example 1:
[poem with near rhymes like "love/bud", "team/ring"]

Example 2:
[another example demonstrating slant rhymes]

Now write a similar poem about [topic] using only near rhymes, avoiding perfect rhymes like "love/dove" or "night/light":
```

#### Challenges with Few-Shot Approaches
- Models may overgeneralize from limited examples
- Maintaining consistent constraint adherence across longer texts
- Balancing example quantity with prompt length limits

### 5. Common Failures and How to Address Them

#### Identified Failure Patterns

**1. Rhyme Degradation**
- **Problem**: Models start with good rhyming then degrade into "confused gibberish"
- **Solution**: Shorter generation segments with validation checkpoints

**2. Overly Simple Rhymes**
- **Problem**: AI produces "jingly and jangly" perfect rhymes
- **Solution**: Specify crossing parts of speech for rhymes; avoid all monosyllabic nouns at line ends

**3. Syntax Distortion**
- **Problem**: Forced rhymes create awkward sentence structures
- **Solution**: Use balanced mix of perfect and slant rhymes; prioritize meaning over perfect rhyme

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
- **Rhyme Detection**: Focus on stressed syllables and "rhyming parts"
- **Implementation**: Python libraries like `pronouncing` provide simple interfaces
- **Slant Rhyme Logic**: Compare vowels and final consonants while allowing intermediate consonant variation

#### Advanced Rhyme Detection
- **Multi-syllabic Matching**: Improved sonic quality when multiple stressed syllables match
- **Internal Rhymes**: Perfect rhymes not occurring at line ends (e.g., "cigar" and "disregarded")
- **Phonetic Distance**: Threshold-based comparison of phone positions in vowel/consonant space

### Validation Strategies

#### Real-Time Constraint Checking
- Convert generated text to phonemes using tools like Phonemizer
- Apply CMU Dictionary lookups for rhyme part extraction
- Calculate phonetic distances for slant rhyme validation
- Implement iterative refinement loops for constraint violations

#### Multi-Agent Approaches
- Generation agent creates initial content
- Validation agent checks rhyme constraints
- Refinement agent suggests improvements
- Quality assessment agent evaluates overall coherence

## Practical Prompt Templates for Testing

### Template 1: Explicit Near-Rhyme Instruction
```
Write a 8-line poem about [TOPIC] using only near rhymes or slant rhymes.
Avoid perfect rhymes like "night/light" or "love/dove".
Instead use subtle sound relationships like "love/bud" or "team/ring".
Focus on assonance (similar vowel sounds) and consonance (similar consonant sounds).
```

### Template 2: Few-Shot Learning Approach
```
Here are examples of poems using only near/slant rhymes:

The morning light felt strange and new,
While shadows danced in patterns broad.
I walked through streets both old and blue,
Seeking some forgotten word.

Now write a similar 4-line poem about [TOPIC] using the same near-rhyme style.
Avoid perfect rhymes. Use subtle sound connections instead.
```

### Template 3: Negative Constraint with Positive Guidance
```
Write a poem about [TOPIC] that uses interesting sound patterns but avoids obvious perfect rhymes.
Instead of rhyming "day/way" or "love/dove", use more subtle connections like:
- Assonance: similar vowel sounds (home/stone)
- Consonance: similar consonant endings (milk/walk)
- Slant rhymes: partial sound matches (mind/kind becomes mind/send)
```

### Template 4: Technical Specification
```
Generate a poem with these constraints:
- Topic: [TOPIC]
- Length: 8 lines
- Rhyme scheme: ABAB CDCD (but using only slant/near rhymes)
- No perfect rhymes (identical rime structures)
- Acceptable: assonance, consonance, visual rhymes
- Maintain natural syntax and meaning
```

### Template 5: Iterative Refinement
```
Write a poem about [TOPIC]. After each attempt, I'll check for perfect rhymes.
If any perfect rhymes are found, replace them with near rhymes while maintaining meaning.
Example substitutions:
- "night/light" → "night/dream"
- "love/dove" → "love/warmth"
Continue until only near/slant rhymes remain.
```

## Recommended Implementation Strategy

Based on research findings, the most promising approach combines:

1. **Few-shot learning** with curated near-rhyme examples
2. **Explicit constraint specification** in prompts
3. **Iterative validation loops** using phonetic analysis
4. **Multi-agent architecture** for generation and validation
5. **CMU Dictionary integration** for rhyme classification

The research reveals significant gaps in current practice, particularly around negative prompting for poetry generation. This suggests an opportunity for innovation in developing more sophisticated constraint satisfaction approaches specifically for poetic generation.

## Research Gaps Identified

1. **Limited negative prompting documentation** for poetry vs. image generation
2. **Lack of phonetic awareness** in most language models
3. **Insufficient constraint satisfaction methods** for complex poetic forms
4. **Missing benchmarks** for evaluating near-rhyme quality
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
  - Direct rhyme detection: `pronouncing.rhymes("climbing")`
  - Returns perfect rhymes by default (needs modification for near-rhymes)
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

## Near-Rhyme Detection Algorithms

### Core Detection Methods

#### **Slant Rhyme Detection (from Rhyme-Highlighter)**
```python
def detect_slant_rhymes(word1, word2):
    phones1 = phones_for_word(word1)
    phones2 = phones_for_word(word2)
    # Compare last 2 phonemes for similarity
    return phones1[0][-2:] == phones2[0][-2:]
```

#### **Edit Distance on Phonemes**
- Apply Levenshtein distance to phonetic representations
- Weight different phonetic features (vowels vs consonants)
- Use threshold-based classification for near vs exact rhymes

#### **Feature-Based Classification**
- **Assonance**: Similar vowel sounds, different consonants (bad:have)
- **Consonance**: Similar consonant sounds, different vowels (team:ring)
- **Slant Rhymes**: Partial phonetic overlap (love:bud)
- **Visual Rhymes**: Similar spelling, different pronunciation

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
- Focus excessively on perfect rhymes (problematic for our use case)
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

### Proposed Multi-Agent Architecture for Near-Rhyme Poetry

#### **Agent Role Distribution**
1. **Generator Agent**: Creates initial poetry drafts based on prompts
2. **Validator Agent**: Checks for exact vs near rhymes using phonetic analysis
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
4. **Validate**: Check rhyme constraints and quality metrics
5. **Iterate**: Repeat process until constraints satisfied

## Scoring and Ranking Systems for Rhyme Quality

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

#### **Rhyme Accuracy Metrics**
- **Exact Rhyme Detection**: Binary classification (must be 0% for our use case)
- **Near Rhyme Quality**: Scoring phonetic similarity (0-1 scale)
- **Pattern Consistency**: Adherence to intended rhyme scheme throughout poem

#### **Formal Poetry Metrics**
- **Meter Compliance**: Stress pattern accuracy and consistency
- **Syllable Count**: Line length consistency with intended form
- **Rhythm Flow**: Overall prosodic quality and natural flow

#### **Russian Poetry Scansion Tool (RPST) Example**
- **Technicality Score**: 0-1 scale for meter compliance
- **Rhyme Detection**: Including fuzzy/slant rhymes
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
def score_near_rhyme_poem(poem):
    scores = {
        "rhyme_compliance": check_no_exact_rhymes(poem),
        "near_rhyme_quality": score_phonetic_similarity(poem),
        "semantic_coherence": evaluate_meaning_consistency(poem),
        "formal_structure": check_meter_and_syllables(poem),
        "lexical_diversity": calculate_vocabulary_richness(poem)
    }
    return weighted_average(scores)
```

## Implementation Recommendations

### Recommended Technology Stack

#### **Core Libraries for Production Use**
1. **Pronouncing**: CMU dictionary access and basic rhyme detection
2. **PyPhonetics**: Advanced phonetic similarity algorithms
3. **Jellyfish**: String similarity and distance metrics for backup
4. **Langroid**: Multi-agent framework for LLM coordination

#### **Supporting Tools**
1. **Rich**: Terminal visualization for rhyme pattern highlighting
2. **NLTK/spaCy**: NLP preprocessing and linguistic analysis
3. **Transformers**: LLM integration and text generation
4. **Evaluate**: Automated metric calculation and assessment

### Architecture Pattern: Layered Validation System

```python
class NearRhymeValidator:
    def __init__(self):
        self.exact_rhyme_detector = ExactRhymeDetector()
        self.near_rhyme_scorer = NearRhymeScorer()
        self.quality_assessor = QualityAssessor()

    def validate_poem(self, poem):
        # Layer 1: Reject exact rhymes (hard constraint)
        if self.exact_rhyme_detector.has_exact_rhymes(poem):
            return False, "Contains exact rhymes - regeneration required"

        # Layer 2: Score near rhyme quality
        near_score = self.near_rhyme_scorer.score(poem)

        # Layer 3: Overall quality assessment
        quality_score = self.quality_assessor.evaluate(poem)

        return True, {
            "near_rhyme_score": near_score,
            "quality_score": quality_score,
            "overall_rating": (near_score + quality_score) / 2
        }
```

### Performance Optimization Strategies

#### **Efficiency Considerations**
1. **Phonetic Caching**: Pre-compute phonetic representations for common words
2. **Similarity Indexing**: Build phonetic similarity indices for fast lookup
3. **Parallel Processing**: Multi-threaded validation for longer texts
4. **Early Termination**: Stop processing immediately on exact rhyme detection

## Validation and Testing Approaches

### Comprehensive Test Suite Design

#### **Known Examples Database**
```python
test_cases = {
    "exact_rhymes": [
        ("cat", "bat"),      # Should FAIL validation
        ("love", "dove"),    # Should FAIL validation
        ("night", "light"),  # Should FAIL validation
    ],
    "near_rhymes": [
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
1. **Phase 1**: Implement simple exact rhyme detection and rejection
2. **Phase 2**: Add basic near-rhyme classification algorithms
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
- **Application**: Could be adapted for rhyme constraint satisfaction

#### **GPT Czech Poet (2024)**
- **Author**: Chudoba and Rosa
- **Focus**: Generation of Czech poetic strophes with language models
- **Relevance**: Cross-lingual poetry generation techniques

### Future Research Directions

#### **Technical Advancement Opportunities**
1. **Cross-lingual Near-Rhyme**: Extend algorithms beyond English
2. **Cultural Context Integration**: Incorporate cultural rhyming traditions
3. **Personalization**: Adapt to individual poetic styles and preferences
4. **Real-time Interactive Generation**: Live poetry creation tools

#### **Advanced Technical Enhancements**
1. **Neural Rhyme Detection**: Transformer-based phonetic similarity models
2. **Semantic Preservation**: Maintain meaning while applying rhyme constraints
3. **Style Transfer**: Generate poetry in specific traditional forms
4. **Multimodal Integration**: Combine text analysis with audio pronunciation

This comprehensive technical research provides a solid foundation for implementing sophisticated near-rhyme poetry generation systems with practical, tested approaches and modern tools.