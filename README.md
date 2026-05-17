# X Algorithm Analysis: Claude Opus 4.6 Max vs GPT-5.5 Extra-High

A head-to-head comparison of two frontier AI models analyzing the open-source X "For You" recommendation algorithm.

Both models were given the **same prompts**, the **same codebase**, and ran at their **maximum reasoning tiers with 1M token context**. Then each was asked to evaluate the other's report.

---

## Models Used

| | Claude | GPT |
|---|---|---|
| **Model** | Claude Opus 4.6 Max | GPT-5.5 Extra-High |
| **Context Window** | 1M tokens | 1M tokens |
| **Variant** | Maximum (highest reasoning tier) | Extra-High (highest reasoning tier) |
| **Mode** | Cursor Agent (parallel subagents) | Cursor Agent |

**Why Opus 4.6 instead of 4.7?** The general sentiment and benchmarks around Opus 4.7 suggest its performance hasn't matched 4.6 for deep code analysis tasks. Opus 4.6 remains the stronger pick for thorough, multi-file repository exploration.

---

## Repository Structure

```
output/
├── README.md                      # This file
├── markdown/
│   ├── x-algorithm-analysis-claude.md           # Claude's X thread (20 posts)
│   ├── x-algorithm-reach-thread.md              # GPT's X thread (16 posts) [original]
│   ├── x-algorithm-reach-thread-created-by-gpt.md  # GPT's X thread [labeled copy]
│   ├── x-algorithm-reach-article.md             # GPT's full article [original]
│   ├── x-algorithm-reach-article-created-by-gpt.md # GPT's full article [labeled copy]
│   ├── claude-vs-gpt-comparison.md              # Claude's comparison report
│   ├── x-algorithm-report-comparison.md         # GPT's comparison report [original]
│   ├── x-algorithm-report-comparison-created-by-gpt.md # GPT's comparison [labeled copy]
│   └── x-article-claude-vs-gpt-final.md         # Final X Article (balanced)
├── pdf/
│   ├── x-algorithm-analysis-claude.pdf          # Claude's PDF report (7 pages)
│   ├── x-algorithm-reach-report.pdf             # GPT's PDF report (4 pages) [original]
│   ├── x-algorithm-reach-report-created-by-gpt.pdf # GPT's PDF report [labeled copy]
│   ├── claude-vs-gpt-comparison.pdf             # Claude's comparison PDF (5 pages)
│   ├── x-algorithm-report-comparison.pdf        # GPT's comparison PDF [original]
│   ├── x-algorithm-report-comparison-created-by-gpt.pdf # GPT's comparison [labeled copy]
│   ├── generate_claude_report.py                # Script that generated Claude's PDF
│   └── generate_comparison.py                   # Script that generated Claude's comparison PDF
```

---

## Prompts Given (Same Prompts to Both Models)

### Prompt 1: Algorithm Analysis

> YOU ARE AN EXPERT ALGORITHMS ANALYZER who has deep expertise in analyzing and concluding how the algorithms are behaving. Your job is to go through this entire repo and prepare a summary report on:
> - how this algorithm is behaving
> - how this algorithm is favoring which type of content
> - how someone can increase and boost the reach on X
> - totally on the basis of analyzing these algorithms, what are the don'ts and all
> - how actually I can get good reach on X

### Prompt 2: Generate PDF and Markdown

> CONVERT THIS INTO PDF AND A MARKDOWN FILE TO COPY PASTE AND DIRECTLY SHARE ON X

### Prompt 3: Cross-Evaluation

> For an expert and unbiased researcher, your job is to now go through the analysis report provided by [the other model] in the PDF folder of this repository. Analyze your report with [the other model's] report and give me a prepared summary report on whether your report is better or [the other model's] report is better. Give me a comparative table or chart or summary PDF on the basis of that and a markdown file as well.

### Prompt 4: Final X Article

> Both models were asked to prepare an X Article with a proper comparison report mentioning model variants, where GPT wins, where Claude wins, and a final verdict with a brief overview of the algorithm.

---

## Results Summary

### Claude's Self-Evaluation: Claude 73 / GPT 70 (out of 90)
- Claude wins: Technical Depth, Code Specificity, Unique Insights, Comprehensiveness
- GPT wins: Accuracy/Honesty, Conciseness, X Thread Shareability, Creator Accessibility

### GPT's Self-Evaluation: GPT 8.35 / Claude 7.18 (weighted out of 10)
- GPT wins: Code Accuracy, Evidence Discipline, Caveats & Uncertainty
- Claude wins: Completeness, Practical Usefulness, Readability/Shareability

### The Pattern
Each model designed a scoring rubric that favored its own strengths. Claude's rubric rewards depth. GPT's rubric rewards caution. Both are valid. Neither is neutral.

### Final Verdict
- **For technical audiences** (engineers, growth hackers): Claude's report
- **For general creators** (just want to know what to do): GPT's report
- **For posting on X right now**: GPT's thread
- **For deep reference material**: Claude's report
- **For executive briefing**: GPT's report

**The ideal approach: GPT for truth. Claude for depth. Combine both for the complete picture.**

---

## The Algorithm (What Both Reports Agree On)

The X "For You" feed is powered by a multi-stage pipeline:

1. **Viewer Context** -- hydrate engagement history, follows, mutes, blocks, topics
2. **Candidate Retrieval** -- Thunder (in-network) + Phoenix (out-of-network via Grok transformer)
3. **Hydration** -- enrich with metadata, media, engagement counts, mutual follows
4. **Filtering** -- remove duplicates, old posts, blocked/muted, muted keywords, seen posts
5. **ML Scoring** -- Phoenix Grok transformer predicts 15+ engagement probabilities per tweet
6. **Weighted Scoring** -- Final Score = SUM(weight x P(action)) for all action types
7. **Diversity** -- exponential decay for repeated authors
8. **Selection** -- top-K by score
9. **Safety** -- visibility filtering removes policy-violating content

**Core formula:** `Final Score = SUM(weight_i x P(action_i))`

Positive actions (like, reply, repost, share, dwell, follow) boost. Negative actions (block, mute, report, not_interested, not_dwelled) suppress.

---

## Author

**[@Shreyas_Pandeyy](https://x.com/Shreyas_Pandeyy)**

---

## Source Repository

The algorithm source code analyzed: [x-algorithm](https://github.com/xai-org/x-algorithm) (May 2026 release)

## License

Analysis reports and comparison content are original work. The underlying algorithm code is licensed under Apache 2.0 by X.AI Corp.
