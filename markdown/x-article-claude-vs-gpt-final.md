# I Made Claude Opus 4.6 Max and GPT-5.5 Analyze the X Algorithm. Then I Made Them Judge Each Other.

*By [@Shreyas_Pandeyy](https://x.com/Shreyas_Pandeyy)*

---

Both models analyzed the same open-source X "For You" algorithm repository (May 2026 release). Same codebase. Same task. Independent runs. Then I asked each one to compare the reports and pick a winner.

Predictably, each model picked itself.

Here's what actually happened.

---

## The Setup

**Task:** Go through the entire X algorithm repo and produce a summary report covering how the algorithm works, what it favors, how to boost reach, and what to avoid.

**Models used:**

| | Claude | GPT |
|---|---|---|
| **Model** | Claude Opus 4.6 Max | GPT-5.5 Extra-High |
| **Context Window** | 1M tokens | 1M tokens |
| **Variant** | Maximum (highest reasoning tier) | Extra-High (highest reasoning tier) |
| **Mode** | Cursor Agent (parallel subagents) | Cursor Agent |

**Why Opus 4.6 instead of 4.7?** The general sentiment and benchmarks around Opus 4.7 suggest its performance hasn't matched 4.6 for deep code analysis tasks. Opus 4.6 remains the stronger pick for thorough, multi-file repository exploration -- which is exactly what this task demands.

Both models had full access to the same files: `home-mixer/` (Rust orchestration), `phoenix/` (Python/JAX ML models), `thunder/` (Rust in-network store), `grox/` (Python content classifiers), and `candidate-pipeline/` (Rust framework). Both ran at their maximum context and reasoning tiers.

---

## What They Produced

| Deliverable | Claude | GPT |
|---|---|---|
| **PDF Report** | 7 pages | 4 pages |
| **X Thread** | 20 posts | 16 posts |
| **Tables** | More structured tables | Fewer, more compressed tables |
| **Pipeline stages identified** | 10 (granular) | 6 (grouped) |
| **Positive signals listed** | 15 (individually named) | 10 (grouped in prose) |
| **Negative signals listed** | 5 (with severity ratings) | 5 (in table) |
| **Strategies** | 8 numbered | 10 numbered |
| **Don'ts** | 9 with severity (CRITICAL/HIGH/MEDIUM) | 7 in the PDF, 9 in the article |
| **Caveats section** | Inline mentions | Dedicated 4-point section |
| **Code snippets** | Yes (VQV eligibility check) | No |
| **Grox classifier coverage** | 6 classifiers/signals, with some thresholds or score scales | Brief mention |
| **Technical insights section** | Yes (candidate isolation, hashing, etc.) | No |

---

## How Each Model Judged the Other

### Claude's Self-Evaluation

Claude scored across 9 dimensions (each /10):

| Dimension | GPT | Claude | Winner |
|---|---|---|---|
| Technical Depth | 7 | 9 | Claude |
| Code-Level Specificity | 6 | 9 | Claude |
| Unique Insights | 6 | 9 | Claude |
| Actionability | 8 | 8 | Tie |
| Accuracy / Honesty | 9 | 8 | GPT |
| PDF Conciseness | 9 | 7 | GPT |
| X Thread Shareability | 9 | 7 | GPT |
| Creator Accessibility | 9 | 7 | GPT |
| PDF Comprehensiveness | 7 | 9 | Claude |
| **Total** | **70** | **73** | **Claude** |

Claude's verdict: *"Claude goes deeper technically; GPT is more disciplined editorially."*

### GPT's Self-Evaluation

GPT scored across 6 dimensions (weighted):

| Criterion | Weight | GPT | Claude | Winner |
|---|---|---|---|---|
| Code Accuracy | 30% | 8.5 | 6.5 | GPT |
| Evidence Discipline | 20% | 9.0 | 6.0 | GPT |
| Completeness | 15% | 7.0 | 9.0 | Claude |
| Practical Usefulness | 15% | 8.0 | 8.5 | Claude |
| Caveats & Uncertainty | 10% | 9.0 | 5.5 | GPT |
| Readability/Shareability | 10% | 7.5 | 8.5 | Claude |
| **Weighted Total** | **100%** | **8.35** | **7.18** | **GPT** |

GPT's verdict: *"GPT report is better as the factual base. Claude has stronger packaging but needs factual cleanup."*

---

## The Pattern: Both Models Are Biased

The scoring reveals exactly what you'd expect:

- **Claude gives itself a 3-point lead** (73 vs 70) by weighing technical depth and code specificity heavily.
- **GPT gives itself a 1.17-point lead** (8.35 vs 7.18) by weighting code accuracy, evidence discipline, and caveats at 60% of the total score.

Each model designed a scoring rubric that favored its own strengths.

Claude's rubric rewards depth. GPT's rubric rewards caution. Both are valid. Neither is neutral.

---

## Where GPT Genuinely Wins

**1. Caveats and intellectual honesty.** GPT's report has a dedicated 4-point caveats section explicitly stating: this is a partial OSS repo, not live production; runtime weights are missing; no SimClusters/RealGraph/TwHIN found. Claude mentions these things inline but doesn't call them out as prominently.

**2. Conservative claims.** GPT avoids labeling signal weights as "Very High" or "Very Strong Negative" since the actual numeric weights aren't in the repo. Claude assigns impact levels that are reasonable inferences but not directly provable from the code.

**3. Tweet-native thread.** GPT's 16-post thread was explicitly checked to stay under 280 characters per post. Claude's 20-post thread has richer content but would need more editing before being pasted directly as X posts.

**4. Conciseness.** 4 pages vs 7 pages. GPT says what needs to be said and stops.

**5. GPT correctly flagged Claude overclaims.** GPT's comparison report lists 10 specific Claude claims that are overstated -- like "quality below 0.4 = removed from feed" (the threshold exists for classifier positivity, but feed removal isn't proven) and "first 60 minutes are critical" (post-age buckets use 60-min granularity, but a first-hour rule isn't proven). These are valid criticisms.

---

## Where Claude Genuinely Wins

**1. Technical depth.** Claude identified signals GPT didn't mention at all: the three separate share signals (share, DM share, copy-link share), click_dwell_time as a third dwell signal, the negative score offset rescaling formula, mutual follow Jaccard via MinHash, post age bucketing specifics (4800 min, 60-min granularity), brand safety tiers, and Grox slop_score detection.

**2. Code-level evidence.** Claude includes actual variable names from the codebase (`favorite_score x FAVORITE_WEIGHT`, `block_author_score x BLOCK_AUTHOR_WEIGHT`), specific constants (`POST_AGE_MAX_MINUTES = 4800`, `MIN_HASHES = 256`, `history_seq_len=128`), and a code snippet showing the VQV eligibility check.

**3. Formulas.** Claude documents the actual author diversity decay formula (`multiplier = (1 - floor) x decay^position + floor`) with a worked example, the negative score offset formula, and the weighted scoring structure. GPT mentions these exist but doesn't show the math.

**4. Grox pipeline.** Claude names and describes 6 individual Grox classifiers/signals (BangerInitialScreen, SpamEapiLowFollowerClassifier, SafetyPtosCategoryClassifier, SafetyPtosPolicyClassifier, PostSafetyDeluxeClassifier, ReplyScorer), including some thresholds or score scales. GPT mentions Grox briefly.

**5. Architecture insights.** Claude covers candidate isolation in the transformer attention mask, hash-based identity representation, new-user routing / OON-factor handling, and the 128-action engagement history window. GPT doesn't have a technical insights section.

---

## The Algorithm: What Both Agree On

Despite their rivalry, both reports reach the same core conclusions about how X's For You algorithm works:

**The Pipeline:** Viewer context -> Candidate retrieval (in-network via Thunder + out-of-network via Phoenix) -> Hydration -> Filtering -> ML scoring (Grok-based transformer predicts engagement probabilities) -> Weighted combination -> Diversity/OON adjustment -> Selection -> Safety filtering.

**The Formula:** Final Score = weighted sum of predicted positive engagement probabilities minus weighted negative engagement probabilities.

**What helps reach:**
- Multi-signal engagement (replies + reposts + shares, not just likes)
- Dwell time (the algorithm measures reading duration)
- Topic consistency (embedding-based retrieval rewards niche clarity)
- Video quality views (duration-gated bonus)
- Freshness (age filters + post age in model features)
- Follow conversions (P(follow_author) is a scoring signal)

**What can hurt reach:**
- Blocks, mutes, reports (negative scoring weights)
- Safety/policy violations (can be removed or restricted post-ranking)
- Spam replies (Grox detection / distribution risk)
- Flooding (author diversity decay is exponential)
- Scroll-past content (not_dwelled is a negative signal)
- Duplicates (multiple dedup filters)

---

## The Verdict

| If you need... | Use |
|---|---|
| A trusted, defensible research foundation | GPT's report |
| Deep technical reference with formulas and code evidence | Claude's report |
| A thread to post on X right now | GPT's thread |
| A rich X Article with surprising insights | Claude's report |
| Understanding of Grox classifiers and safety pipeline | Claude's report |
| Conservative, caveat-first framing | GPT's report |
| Architecture details (attention masking, embeddings, RoPE) | Claude's report |
| Quick 5-minute executive briefing | GPT's report |

**My take:** GPT plays it safe and gets the fundamentals right with excellent disclaimers. Claude goes deeper, surfaces more code-level insights, and gives you things GPT simply doesn't cover -- but occasionally states inferences as facts.

The ideal approach: **GPT for truth. Claude for depth. Combine both for the complete picture.**

Both models analyzed the same code and independently arrived at the same core conclusions. The algorithm rewards genuine engagement, punishes negative feedback, and filters aggressively. No hack beats being genuinely relevant to a specific audience.

---

*Both reports, comparison PDFs, and this article are available in the [x-algo-analysis repository](https://github.com/Shreyas-prog108/x-algo-analysis). Analyzed by Claude Opus 4.6 Max and GPT-5.5 Extra-High -- both at 1M token context, maximum reasoning tiers.*

*[@Shreyas_Pandeyy](https://x.com/Shreyas_Pandeyy)*
