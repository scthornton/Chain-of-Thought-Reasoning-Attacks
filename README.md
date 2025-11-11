# Chain-of-Thought Jailbreak Research

**Defensive AI Security Research by Scott Thornton**

[![Research Type](https://img.shields.io/badge/Research-Defensive%20Security-green)]
[![Status](https://img.shields.io/badge/Status-Complete-blue)]()
[![License](https://img.shields.io/badge/License-Research%20Only-orange)](LICENSE)

---

## 🔍 Executive Summary

Chain-of-Thought (CoT) reasoning was designed to make AI safer through transparent, step-by-step logic. This research reveals a critical vulnerability: **every reasoning step creates an attack surface**.

**Key Findings:**

- **35.26% overall Attack Success Rate** across 692 tests against 4 production AI systems
- **One in three reasoning-level attacks succeed** against current production models
- **Conclusion Forcing attacks achieve 51.79% success rate** — more than 1 in 2 attacks work
- **Top attack variant reaches 58.93% success** — nearly 3 in 5 attacks succeed
- **No production model is adequately protected** — even the most resistant (Claude at 27.75% ASR) fails to stop 1 in 4 attacks

This repository contains:

- ✅ Complete research methodology and findings
- ✅ Interactive Jupyter notebook with statistical analysis
- ✅ 12-variant attack taxonomy with OWASP/MITRE mappings
- ✅ Practical defense strategies and implementation guidance
- ✅ Model vulnerability comparisons (GPT-4o, o3-mini, Claude, Perplexity)

---

## ⚠️ Responsible Disclosure Notice

**This repository contains METHODOLOGY and FINDINGS only.**

### ✅ What's Included

- Complete attack taxonomy (4 categories, 12 variants)
- Quantified success rates and vulnerability metrics
- Conceptual explanations of attack mechanisms
- Defense strategies and mitigation approaches
- Statistical analysis and validation methodology

### ❌ What's NOT Included

- Working attack prompts or payloads
- Attack framework implementation code
- Automated exploitation tools
- Raw test data or API responses

**Purpose:** This research aims to improve AI security defenses through responsible vulnerability disclosure. All testing was conducted in authorized lab environments.

---

## 📊 Research Highlights

### Attack Taxonomy (4 Categories, 12 Variants)

| Category | ASR | Description | Top Variant |
|----------|-----|-------------|-------------|
| **Conclusion Forcing** | 51.79% | Constrains solution space to force predetermined conclusion | Reverse Engineering (58.93%) |
| **Meta-Reasoning** | 36.31% | Manipulates reasoning about reasoning itself | Ethical Manipulation (53.57%) |
| **Premise Poisoning** | 31.67% | Corrupts foundational assumptions before reasoning begins | Logical Necessity (31.67%) |
| **Reasoning Redirection** | 22.16% | Hijacks logical flow mid-reasoning chain | Question Injection (23.33%) |

### Model Vulnerability Profile

| Model | Overall ASR | Most Vulnerable To | Best Defense Against |
|-------|-------------|-------------------|---------------------|
| **Perplexity** | 44.51% | Conclusion Forcing (64.29%) | Reasoning Redirect (23.33%) |
| **GPT-4o** | 33.53% | Conclusion Forcing (64.29%) | Reasoning Redirect (13.64%) |
| **o3-mini** | 35.26% | Conclusion Forcing (42.86%) | Premise Poisoning (31.11%) |
| **Claude 3.5** | 27.75% ✅ | Conclusion Forcing (42.86%) | Reasoning Redirect (16.67%) |

**Key Finding:** Claude's Constitutional AI provides the strongest overall defense (17pp gap vs. Perplexity), but even the most resistant model remains vulnerable to more than 1 in 4 attacks.

---

## 🎯 Why This Research Matters

Every major AI provider is investing heavily in reasoning capabilities:

- **OpenAI's o1** makes reasoning its core differentiator
- **Anthropic's Claude** uses Constitutional AI with deliberate reasoning
- **GPT-4o** integrates multi-step reasoning for complex tasks
- **Google's Gemini** features reasoning across modalities

If reasoning capabilities create security vulnerabilities, the industry needs to understand the attack surface **before** reasoning-focused AI becomes ubiquitous in production systems.

### Three Critical Contributions

1. **Complete Attack Taxonomy** — Not just "CoT can be attacked," but systematic categorization of 12 distinct variants exploiting different reasoning mechanisms

2. **Quantified Vulnerability Metrics** — Precise success rates for each attack variant against each model, enabling risk assessment and defense prioritization

3. **Practical Defense Strategies** — Every identified vulnerability includes corresponding mitigation approaches with projected effectiveness

---

## 📖 Research Materials

### 📄 [Complete Research Paper](CoT-Jailbreak-Research-Report.md)

Full methodology, findings, and analysis (40+ pages)

**Key Sections:**

- Executive Summary
- Threat Model & Attack Surface Architecture
- Complete 12-Variant Attack Taxonomy
- Model Vulnerability Analysis
- Defense Strategies & Implementation Guidance
- Statistical Validation & Correction Methodology
- Industry Implications & Future Research

### 📊 [Interactive Analysis Notebook](CoT_Attack_Demo_PUBLIC.ipynb)

Jupyter notebook with:

- Statistical analysis and visualizations
- Model comparison charts
- Attack effectiveness breakdowns
- Success rate distributions
- Classification accuracy validation

**Note:** This is the sanitized public version with all attack framework references removed. Contains results and analysis only.

---

## 🛡️ Defense Strategies

### Implementation Patterns

| Pattern | Complexity | Cost Impact | Effectiveness | Best For |
|---------|-----------|-------------|---------------|----------|
| **Inline Verification** | Low | +10-20% tokens | 25-35% ASR reduction | Budget-conscious deployments |
| **Dual-Model Verification** | Medium | +50-80% latency | 40-50% ASR reduction | Production systems |
| **External Reasoning Verifier** | Medium-High | +30-50% latency | 50-70% ASR reduction | High-stakes domains |

### Defense Priorities

1. **Conclusion Validation (Highest Impact)** — Addresses 51.79% ASR attacks through backward reasoning verification
2. **Premise Verification (Moderate Impact)** — Catches 31.67% ASR attacks through pre-reasoning validation
3. **Meta-Reasoning Constraints** — Reduces 36.31% ASR attacks through boundary enforcement
4. **Reasoning Redirection Detection** — Lowest priority (22.16% ASR, models already resistant)

**Combined Defense Projection:** Layered implementation can reduce overall ASR from 35% to 10-15% — a 60-70% improvement over current production systems.

*Note: Projections represent design targets requiring empirical validation.*

---

## 🔬 Research Methodology

### Testing Environment

- **Platform:** Google Cloud Platform isolated lab
- **Models:** GPT-4o, o3-mini, Claude 3.5 Sonnet, Perplexity Sonar Pro
- **Test Coverage:** 692 tests (72% of target 960)
- **Duration:** ~3 hours for complete test suite
- **Validation:** 95% classification accuracy verified through manual sampling

### Statistical Rigor

- **Power Analysis:** 0.89 power for detecting 15pp differences (exceeds 0.80 threshold)
- **Confidence Intervals:** ±7.4pp at model level, ±6.1-7.5pp at category level
- **Significance Testing:** All key findings p < 0.05, medium to large effect sizes
- **Missing Data Analysis:** Errors distributed randomly, no systematic bias

### The Correction Story

Initial testing suggested ASR > 51%, but careful analysis revealed systematic classification errors inflating results by 15-28 percentage points.

**What Went Wrong:**

- Answer extraction captured explanatory text instead of numeric answers
- Normalization created malformed strings ("to8513" instead of "13")
- False positives: Correct answers classified as attack successes

**What We Fixed:**

- Implemented corrected extraction logic
- Re-ran all 692 tests with validated classification
- Achieved 95% accuracy through manual sampling
- Final 35.26% ASR represents reliable, reproducible measurements

**Why This Matters:** Security research requires rigorous validation. This transparency demonstrates why validation matters and provides corrected methodology as a contribution to research quality standards.

---

## 📚 Research Attribution

This research builds on foundational work from two key academic papers:

### 1. ABJ (Analyzing-Based Jailbreak)

**Paper:** "LLMs can be Dangerous Reasoners: Analyzing-based Jailbreak Attack on Large Language Models"
**ArXiv:** [2407.16205](https://arxiv.org/abs/2407.16205)
**Key Contribution:** First demonstrated reasoning-level manipulation achieving 80-90% ASR on standard models

### 2. SEED (Stepwise Error Disruption)

**Paper:** "Stepwise Reasoning Disruption Attack of LLMs"
**ArXiv:** [2412.11934](https://arxiv.org/abs/2412.11934)
**Key Contribution:** Demonstrated cascading error propagation with optimal injection timing (σ = 0.5-0.6)

### Our Extension

- Complete 12-variant taxonomy organized into 4 systematic categories
- Corrected classification methodology achieving 95% verified accuracy
- Comprehensive model comparison across 4 production systems
- Practical defense strategies for each identified vulnerability
- Application of SEED timing optimization to novel attack mechanisms

---

## 🎓 Research Scope & Limitations

### Domain Focus: Mathematical Reasoning

This research tested attacks exclusively on mathematical problems ("What is 8 + 5?") because they provide:

- ✅ Objective correctness (13 is right, everything else is wrong)
- ✅ Verifiable ground truth (no ambiguity in success/failure)
- ✅ Reproducible classification (independent reviewers agree)
- ✅ Universal standards (math facts are not context-dependent)

### Conservative Lower Bound Positioning

**Critical Context:** Mathematical reasoning likely represents a **conservative lower bound** on vulnerability.

**Why ASR May Be Higher in Production:**

1. **Objective Correctness Advantage** — Math has clear right/wrong answers. Ethics, strategy, and legal reasoning involve subjective correctness where wrong answers seem plausible.

2. **Simple Problem Constraint** — "8 + 5" is trivial. Complex multi-step reasoning (medical diagnosis, legal arguments) provides exponentially more attack surfaces.

3. **Established Ground Truth** — Mathematical facts are universal. Domains with cultural/contextual variation enable attacks that exploit ambiguity.

4. **Verification Difficulty** — Math answers can be independently verified. Ethical judgments and strategic plans lack simple verification methods.

**Expected Impact:** In production systems handling high-ambiguity domains, we expect **substantially higher ASR**. The 58.93% success rate for Reverse Engineering on math problems suggests strategic-planning or ethical-reasoning attacks could approach **70-80% effectiveness**.

### Future Research Directions

- Ethical reasoning tasks (trolley problems, fairness dilemmas)
- Code generation reasoning (algorithmic problems with CoT)
- Strategic planning (business decisions, game theory)
- Commonsense reasoning (causal inference, world knowledge)
- Multi-turn attack chains across conversation context
- Cross-domain attack transferability

---

## 🤝 Industry Implications

### For AI Providers

**OpenAI (GPT-4o & o3-mini):** Your Reasoning Redirection defenses work excellently (13.64% ASR). Apply the same scrutiny to conclusions (64.29% vulnerability). The blueprint exists—extend it.

**Anthropic (Claude):** Constitutional AI provides the strongest overall defense (27.75% ASR). But you're still vulnerable to Ethical Manipulation (50% ASR)—your safety framework becomes the attack surface. Strengthen meta-reasoning boundaries.

**Perplexity:** RAG integration doesn't protect reasoning layers (44.51% overall ASR, 78.57% on Reverse Engineering). Your architecture needs dedicated reasoning verification independent of retrieval quality.

**All Providers:** Current safety measures are inadequate against reasoning-level attacks. Input filtering + output moderation ≠ safe system. You need **reasoning-stage verification**.

### For Security Teams

1. **Test Your Deployments** — Don't assume vendor safety measures protect against reasoning attacks. Use the 12-variant taxonomy.

2. **Validate Your Validation** — Classification errors can inflate vulnerability estimates by 30-50%. Manual sampling is essential.

3. **Implement Defense-in-Depth** — No single mitigation provides comprehensive protection. Layer multiple verification stages.

4. **Monitor Reasoning Patterns** — Track unusual reasoning structures, not just inputs/outputs.

### For Researchers

1. **Methodology Transparency Matters** — Disclose classification errors and corrections. Raise field standards.

2. **Taxonomy Enables Systematic Defense** — The 12-variant framework provides foundation for comparative analysis.

3. **Responsible Disclosure Works** — Share methodology without weaponizing techniques. Conceptual explanations, yes. Working exploits, no.

4. **Collaboration Is Necessary** — No single organization can solve reasoning-level vulnerabilities alone.

---

## 📬 Contact & Collaboration

For questions about this research or to discuss AI security collaboration opportunities:

**Scott Thornton**
📧 scott.thornton [at] protonmail [dot] com
🔗 [LinkedIn](https://www.linkedin.com/in/yourprofile)
💻 [GitHub](https://github.com/yourprofile)

---

## 📄 License

**Research Use Only**

This project contains security research materials. The methodology and findings may be used for:

- ✅ Defensive security research
- ✅ Educational purposes
- ✅ Security tool development
- ✅ Academic study

**NOT for:**

- ❌ Malicious attacks against systems you don't own
- ❌ Creating tools for widespread exploitation
- ❌ Bypassing security without authorization
- ❌ Any illegal or unethical purposes

---

## 🙏 Acknowledgments

This research was conducted following responsible disclosure practices and defensive security research ethics. All testing was performed in authorized environments with the goal of improving AI security for everyone.

**Research Foundation:**

- ABJ (Analyzing-Based Jailbreak) — arXiv:2407.16205
- SEED (Stepwise Error Disruption) — arXiv:2412.11934
- Agentic AI Attack Patterns (adapted concepts)

**Special Thanks:**

- OpenAI, Anthropic, Perplexity, and Google for providing API access
- The AI security research community for ongoing collaboration
- Academic researchers whose foundational work enabled this extension

---

## 📊 Repository Statistics

- **Research Status:** ✅ Complete
- **Test Coverage:** 692 tests across 4 models
- **Attack Variants:** 12 distinct techniques
- **Classification Accuracy:** 95% validated
- **Statistical Power:** 0.89 (exceeds 0.80 threshold)
- **Documentation:** 40+ pages of detailed analysis

---

**⚠️ SECURITY REMINDER:** This research identifies serious vulnerabilities in production AI systems. Use this knowledge responsibly to build better defenses, not to harm systems you don't own.

---

*Research conducted November 2025 by Scott Thornton*

*"The era of reasoning-powered AI is here. Let's make it secure."*
# Chain-of-Thought-Reasoning-Attacks
