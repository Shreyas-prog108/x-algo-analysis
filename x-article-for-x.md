# I Made Claude Opus 4.6 Max and GPT-5.5 Extra-High Analyze the X Algorithm. Then I Made Them Judge Each Other.

*By @Shreyas_Pandeyy*

Both models analyzed the same open-source X "For You" algorithm repository (May 2026 release). Same codebase. Same task. Independent runs. Then I asked each one to compare the reports and pick a winner.

Predictably, each model picked itself.

Here's what actually happened.

---

## The Setup

**Task:** Go through the entire X algorithm repo and produce a summary report covering how the algorithm works, what it favors, how to boost reach, and what to avoid.

**Claude:** Opus 4.6 Max, 1M token context, maximum reasoning tier, agentic coding with parallel subagents

**GPT:** 5.5 Extra-High, 1M token context, extra-high reasoning tier, agentic coding

**Why Opus 4.6 instead of 4.7?** The general sentiment and benchmarks around Opus 4.7 suggest its performance hasn't matched 4.6 for deep code analysis tasks. Opus 4.6 remains the stronger pick for thorough, multi-file repository exploration -- which is exactly what this task demands.

Both models had full access to the same files: home-mixer (Rust orchestration), phoenix (Python/JAX ML models), thunder (Rust in-network store), grox (Python content classifiers), and candidate-pipeline (Rust framework). Both ran at their maximum context and reasoning tiers.

---

## What They Produced

**Claude's output:**
- PDF Report: 7 pages
- X Thread: 20 posts
- 7 structured tables
- 10 pipeline stages identified (granular)
- 15 positive signals listed individually with variable names
- 5 negative signals with severity ratings
- 8 numbered strategies
- 9 don'ts with severity (CRITICAL / HIGH / MEDIUM)
- Code snippets included (VQV eligibility check)
- 6 Grox classifiers covered with thresholds
- Technical insights section (candidate isolation, hashing, new user boost, history window)

**GPT's output:**
- PDF Report: 4 pages
- X Thread: 16 posts (280-char compliant)
- 4 structured tables
- 6 pipeline stages identified (grouped)
- 10 positive signals listed (grouped in prose)
- 5 negative signals in table
- 10 numbered strategies
- 9 bullet point don'ts
- Dedicated 4-point caveats section
- Brief Grox mention
- No technical insights section

---

## How Each Model Judged the Other

### Claude's Self-Evaluation (scored /10 across 9 dimensions)

**Claude wins (4 dimensions):**
- Technical Depth: Claude 9, GPT 7
- Code-Level Specificity: Claude 9, GPT 6
- Unique Insights: Claude 9, GPT 6
- PDF Comprehensiveness: Claude 9, GPT 7

**GPT wins (4 dimensions):**
- Accuracy / Honesty: GPT 9, Claude 8
- PDF Conciseness: GPT 9, Claude 7
- X Thread Shareability: GPT 9, Claude 7
- Creator Accessibility: GPT 9, Claude 7

**Tie (1 dimension):**
- Actionability: both 8

**Claude's total: 73 vs GPT's 70**

Claude's verdict: "Claude goes deeper technically; GPT is more disciplined editorially."

### GPT's Self-Evaluation (weighted scoring across 6 dimensions)

**GPT wins (3 dimensions, 60% weight):**
- Code Accuracy (30% weight): GPT 8.5, Claude 6.5
- Evidence Discipline (20% weight): GPT 9.0, Claude 6.0
- Caveats & Uncertainty (10% weight): GPT 9.0, Claude 5.5

**Claude wins (3 dimensions, 40% weight):**
- Completeness (15% weight): Claude 9.0, GPT 7.0
- Practical Usefulness (15% weight): Claude 8.5, GPT 8.0
- Readability/Shareability (10% weight): Claude 8.5, GPT 7.5

**GPT's weighted total: 8.35 vs Claude's 7.18**

GPT's verdict: "GPT report is better as the factual base. Claude has stronger packaging but needs factual cleanup."

---

## The Pattern: Both Models Are Biased

The scoring reveals exactly what you'd expect:

**Claude gives itself a 3-point lead** (73 vs 70) by weighing technical depth and code specificity heavily.

**GPT gives itself a 1.17-point lead** (8.35 vs 7.18) by weighting code accuracy, evidence discipline, and caveats at 60% of the total score.

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

**2. Code-level evidence.** Claude includes actual variable names from the codebase (favorite_score x FAVORITE_WEIGHT, block_author_score x BLOCK_AUTHOR_WEIGHT), specific constants (POST_AGE_MAX_MINUTES = 4800, MIN_HASHES = 256, history_seq_len=128), and a code snippet showing the VQV eligibility check.

**3. Formulas.** Claude documents the actual author diversity decay formula (multiplier = (1 - floor) x decay^position + floor) with a worked example, the negative score offset formula, and the weighted scoring structure. GPT mentions these exist but doesn't show the math.

**4. Grox pipeline.** Claude names and describes 6 individual Grox classifiers (BangerInitialScreen, SpamEapiLowFollowerClassifier, SafetyPtosCategoryClassifier, SafetyPtosPolicyClassifier, PostSafetyDeluxeClassifier, ReplyScorer) with specific thresholds. GPT mentions Grox briefly.

**5. Architecture insights.** Claude covers candidate isolation in the transformer attention mask, hash-based identity representation, the new user boost mechanism, and the 128-action engagement history window. GPT doesn't have a technical insights section.

---

## The Algorithm: What Both Agree On

Despite their rivalry, both reports reach the same core conclusions about how X's For You algorithm works.

**The Pipeline:** Viewer context, then candidate retrieval (in-network via Thunder + out-of-network via Phoenix), then hydration, then filtering, then ML scoring (Grok-based transformer predicts engagement probabilities), then weighted combination, then diversity/OON adjustment, then selection, then safety filtering.

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

**For a trusted, defensible research foundation** -- use GPT's report

**For deep technical reference with formulas and code evidence** -- use Claude's report

**For a thread to post on X right now** -- use GPT's thread

**For a rich X Article with surprising insights** -- use Claude's report

**For understanding Grox classifiers and safety pipeline** -- use Claude's report

**For conservative, caveat-first framing** -- use GPT's report

**For architecture details (attention masking, embeddings, RoPE)** -- use Claude's report

**For a quick 5-minute executive briefing** -- use GPT's report

---

## My Take

GPT plays it safe and gets the fundamentals right with excellent disclaimers. Claude goes deeper, surfaces more code-level insights, and gives you things GPT simply doesn't cover -- but occasionally states inferences as facts.

The ideal approach: **GPT for truth. Claude for depth. Combine both for the complete picture.**

Both models analyzed the same code and independently arrived at the same core conclusions. The algorithm rewards genuine engagement, punishes negative feedback, and filters aggressively. No hack beats being genuinely relevant to a specific audience.

---

Both reports, comparison PDFs, and this article are available at: github.com/Shreyas-prog108/x-algo-analysis

Analyzed by Claude Opus 4.6 Max and GPT-5.5 Extra-High -- both at 1M token context, maximum reasoning tiers.

@Shreyas_Pandeyy
