---
marp: true
theme: gaia
class: lead
backgroundColor: #fff
color: #333
paginate: true
header: "Learning LLM Evaluation Together"
footer: "Building Better AI Evaluations"
---

# Learning LLM Evaluation

## Practical Insights from Our Journey

**Date:** December 2025
**Repository:** nibzard/evals

---

## 20 Insights from Our Journey

1. Foundation: Why Evaluation Matters
2. Framework: Eugene Yan's Approach
3. Practice: Hands-on Implementation
4. Discoveries: What We Learned
5. Growth: Building Better Evaluations

---

# Why LLM Evaluation Matters

### Key Challenges:
- Subjective assessments vs objective metrics
- Inconsistent quality standards
- Hidden failures impact users
- Lack of systematic evaluation

### Our Goal: Reliable Evaluation Systems

> "If you can't measure it, you can't improve it"
> - Peter Drucker

---

## Product Evals: Principle 1

### Binary Classification
- Clear pass/fail decisions
- Eliminates ambiguity
- Enables statistical validation

> **Why binary?**
> Removes evaluation subjectivity

---

## Product Evals: Principle 2

### Target Failure Rates
- 30-50% failure rate provides signal
- Use weaker models for organic failures
- Focus on catching defects

> **Key insight:**
> Failures reveal quality issues

---

## Product Evals: Principle 3

### Statistical Validation
- **Cohen's Kappa** for agreement
- **Fail Recall** as primary metric
- **Human benchmark:** κ~0.2-0.3

> **Humans disagree too!**
> Inter-rater reliability often only 0.2-0.3

---

# Understanding Cohen's Kappa

## Measuring Agreement Beyond Chance

### Kappa Values:
- **0.8-1.0:** Excellent (better than humans)
- **0.6-0.8:** Substantial (good for production)
- **0.4-0.6:** Moderate (acceptable start)
- **0.2-0.4:** Fair (needs improvement)
- **<0.2:** Poor (method issues)

---

# Understanding Cohen's Kappa

### Why Kappa Matters:
- Adjusts for chance agreement
- More meaningful than accuracy
- Accounts for dataset imbalance

> **Human benchmark:** κ often only 0.2-0.3

---

# Learning Exercise Design

### Step 1: Build Understanding
- Create 15-20 questions
- Write thoughtful answers
- Practice systematic thinking

---

# Learning Exercise Design

### Step 2: Establish Ground Truth
- Manual pass/fail labeling
- Develop evaluation criteria
- Create the "gold standard"

---

# Learning Exercise Design

### Step 3: Test Framework
- Run evaluation pipeline
- Compare AI with our labels
- Generate and interpret metrics

---

# Learning Exercise Design

### Step 4: Share Insights
- Document learnings
- Share challenges
- Build community knowledge

---

## Building the Evaluation Pipeline

### Key Components:
```python
# 1. Load ground truth
data = pd.read_csv('data/our_questions.csv')

# 2. Run evaluation
predictions = evaluator.evaluate(
    data['question'], data['response']
)

# 3. Calculate metrics
accuracy, kappa, confusion = calculate_metrics(
    ground_truth, predictions
)
```
---

### Models Used:
- **GPT-5.1:** High-quality ground truth
- **Gemini 2.0 Flash:** Cost-effective evaluation
- **Function Calling:** Reliable structured output

---

# Our Collective Results

### Success Patterns:
- 5 participants achieved excellent agreement (κ≥0.7)
- 60% achieved meaningful fail detection (≥80%)
- Most learned to interpret kappa correctly
- Technical implementation succeeded for everyone

---

### Common Challenges:
- Dataset balance proved crucial
- Ground truth consistency required clear criteria
- Methodological rigor sometimes overlooked

> **Key Insight:** Framework works when properly applied

---

## Learning from Best Results

### Successful Evaluations:

**Rei's Approach (κ=0.780):**
- Balanced dataset (35% failures)
- Clear criteria
- Excellent fail detection (85.7%)

---

**Mariela's Network Eval (κ=0.737):**
- Domain expertise
- Perfect fail detection (100%)
- Professional documentation

---

**Marul's Sports Eval (κ=0.733):**
- Clear interpretation
- Good difficulty balance
- Professional presentation

---

### Common Success Factors:
- Thoughtful ground truth
- Balanced failure rates
- Clear evaluation criteria

---

## Dataset Composition Impact

### Well-Balanced Sets (30-50% failures):
- Marija: 53% fail rate → κ=0.727
- Maksimilijan: 52% fail rate → κ=0.700
- Consistent, reliable metrics

---

### Imbalanced Sets (<20% failures):
- Jozo: 10% fail rate → κ=0.318
- High accuracy, poor significance
- Missed key failures

> **Key:** Balance > Volume
> 15 balanced samples > 20 imbalanced ones

---

# Patterns of Success

---

## Data & Ground Truth

### Clear Ground Truth:
- Consistent pass/fail standards
- Thoughtful reasoning
- Domain expertise

### Dataset Design:
- Mixed difficulty levels
- Balanced failures (30-50%)
- Relevant knowledge

---

## Technical & Analytical

### Technical Excellence:
- Proper CSV structure
- Correct pipeline execution
- Clear metric interpretation

### Analytical Thinking:
- Understanding kappa vs accuracy
- Identifying evaluator weaknesses
- Learning from disagreements

---

# Learning from Challenges

---

## Methodological Pitfalls

### Circular Validation Problem:
- Same model for truth AND evaluation
- Result: κ=0.0 (meaningless)
- Learning: Separate truth from evaluation

### Negative Kappa Surprise:
- κ=-0.176 (worse than random)
- Cause: Poor ground truth consistency
- Learning: High accuracy can mask issues

---

## The Balance Blind Spot

### The Problem:
- Low failure rates (10-15%)
- Impact: Inflated accuracy, poor power

### The Learning:
- Balance drives statistical validity
- 30-50% failure rate is optimal
- Balance > Volume for meaningful results

---

## Confusion Matrix Patterns

### Successful Pattern:
```
          Predicted
 Tr       Pass  Fail
 Pass     14      1    ← Few false alarms
 Fail      1      4    ← Catches failures
```
- High fail recall, balanced performance

---

### Problematic Pattern:
```
          Predicted
 Tr       Pass  Fail
 Pass     11      3
 Fail      2      0    ← Misses all failures!
```
- High accuracy, poor fail detection

> **Missing failures > False alarms**

---

# Domain Expertise Impact

## How Knowledge Affects Quality

### Technical Domains (Networks, Python):
- Precise questions, clear answers
- Natural failure opportunities
- Strong evaluator performance

---

### General Knowledge (Sports, Trivia):
- Requires nuanced understanding
- Subjective evaluation challenges
- Varied success rates

---

### Specialized Knowledge:
- Cultural topics = unique perspectives
- Language considerations (Croatian)
- Context importance in evaluation

> **Choose domains you can evaluate confidently**

---

# Fail Detection: Critical Metric

## Why Catching Failures Matters

### Excellent Fail Detection (≥80%):
- Mariela: 100% (4/4 failures)
- Marija: 100% (8/8 failures)
- Maksimilijan: 100% (10/10 failures)
- Rei: 85.7% (6/7 failures)

---

### Why It Matters:
- Product Safety: Prevents user harm
- Quality Assurance: Stops bad releases
- Trust Building: Builds confidence

> **Prioritize fail recall > accuracy**

---

# Statistical Insights

## Understanding What Numbers Mean

### Accuracy Misleading:
- 85% accuracy sounds good...
- But with 10% failures, it's meaningless
- Kappa reveals true agreement quality

---

### Sample Size Wisdom:
- 15-20 quality samples = meaningful signal
- Balance > total volume
- Confidence intervals show uncertainty

---

### Statistical Understanding:
- 90% accuracy ±15.6% (95% CI) = real uncertainty
- Small samples = high variance
- Kappa adjusts for chance

---

# Core Skills We Developed

## Technical & Analytical

### Technical Competence:
- 100% success running evaluation pipelines
- Proper use of tools and frameworks
- Understanding function calling vs text parsing

---

### Analytical Skills:
- Metric interpretation (kappa vs accuracy)
- Error analysis and pattern recognition
- Statistical thinking about results

---

# Core Skills We Developed

## Methodological & Critical

### Methodological Understanding:
- Ground truth importance & separation
- Dataset design best practices
- Quality assurance thinking for AI

### Critical Thinking:
- Questioning assumptions about AI quality
- Identifying evaluation weaknesses
- Learning from failures

---

# Building Better Evaluation Habits

## Before You Start

### Planning Phase:
1. Define Clear Pass/Fail Criteria
2. Plan for Balance (30-40% failures)
3. Choose Your Domain Wisely
4. Prepare Ground Truth First

> **Success starts with preparation**

---

# Building Better Evaluation Habits

## During & After

### During Evaluation:
1. Use Function Calling (more reliable)
2. Track Multiple Metrics
3. Analyze Disagreements
4. Document Your Process

---

### After Evaluation:
1. Interpret Kappa Carefully
2. Prioritize Fail Detection
3. Consider Statistical Significance
4. Share Your Learnings

---

# Common Pitfalls

## Validation & Balance

### The Separation Mistake:
❌ Same model for truth and evaluation
✅ Use different models/evaluators

---

### The Balance Blindness:
❌ Datasets with <20% failures
✅ Target 30-50% failure rates

---

### The Accuracy Illusion:
❌ Trusting high accuracy alone
✅ Look at kappa and fail recall together

---

# Common Pitfalls

## Criteria & Sample Size

### The Criteria Vagueness:
❌ Unclear pass/fail boundaries
✅ Document criteria upfront

---

### The Small Sample Trap:
❌ 5-10 samples = meaningful results
✅ Use 15+ balanced samples

> **Remember: Quality over quantity**

---

# Community Best Practices

## Data & Ground Truth

### Dataset Design:
- Clear domain expertise
- Include edge cases and failures
- Balance difficulty levels
- Target 30-40% failure rates

---

### Ground Truth Creation:
- Define criteria before labeling
- Document reasoning
- Review for consistency
- Use high-quality models (GPT-5.1)

---

# Community Best Practices

## Evaluation & Documentation

### Evaluation Process:
- Function calling with strict schemas
- Multiple metrics (accuracy, kappa, recall)
- Analyze disagreement patterns
- Consider confidence intervals

---

### Documentation:
- Share methodology and findings
- Include confusion matrices
- Interpret results clearly
- Discuss limitations

---

# Building Your Evaluation Skills

## Beginner & Intermediate

### Beginner Level:
- Run existing evaluation frameworks
- Understand basic metrics
- Practice with simple datasets
- Interpret confusion matrices

---

### Intermediate Level:
- Design balanced datasets
- Create reliable ground truth
- Understand Cohen's Kappa
- Analyze evaluator weaknesses

---

# Building Your Evaluation Skills

## Advanced & Expert

### Advanced Level:
- Optimize for fail detection
- Handle domain-specific challenges
- Contribute to methodology
- Build custom frameworks

---

### Expert Level:
- Research new approaches
- Address fairness and bias
- Scale to production systems
- Advance the field

---

# Appendix: Collective Learning

## Community Results Summary

| Domain | Samples | Kappa | Fail Detection | Key Insight |
|--------|---------|-------|----------------|-------------|
| Networks | 20 | 0.737 | 100% | Perfect catch of failures |
| General | 20 | 0.780 | 85.7% | Highest agreement |
| Sports | 20 | 0.733 | 80% | Professional presentation |
| Python | 21 | 0.700 | 100% | Detailed categorization |
| Oceans | 15 | 0.727 | 100% | Quality over quantity |
| Soccer | 20 | 0.318 | 33% | Balance importance |
| Motorsport | 16 | -0.176 | 0% | Ground truth quality |
| Marine | 20 | 0.000 | 0% | Separation principles |

**Overall:** 70% achieved meaningful results

