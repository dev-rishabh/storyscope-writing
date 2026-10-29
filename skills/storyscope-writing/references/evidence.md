# Evidence

Source: Jenna Russell, Rishanth Rajendhran, Chau Minh Pham, Mohit Iyyer, John Wieting. *StoryScope: Investigating idiosyncrasies in AI fiction.* COLM 2026. arXiv:2604.03136 (v6, 10 Aug 2026). Code and data: https://github.com/jenna-russell/storyscope

## Setup

- 10,272 human short stories from anthology collections, each with a writing prompt reverse-engineered by Gemini 2.5 Flash.
- Five models wrote to each prompt: Claude Sonnet 4.6, GPT-5.4, Gemini 3 Flash, DeepSeek V3.2, Kimi K2.5. 61,608 stories in total, mean 4,753 words.
- GPT-5.1 discovered 304 narrative features across 10 NarraBench dimensions. Gemini 3 Flash labelled every story (Krippendorff's alpha 0.90 across runs; human agreement kappa 0.84).
- XGBoost classifiers with bootstrap SHAP picked out 30 core features (stable human vs AI markers) and 75 fingerprint features (per source).

## Headline results

| Setting | Macro-F1 |
|---|---|
| Human vs AI, narrative features only (257) | 93.2 |
| Human vs AI, narrative + style (304) | 96.0 |
| Human vs AI, 30 core features only | 84.8 |
| Human vs AI, style features only (39) | 85.8 |
| Six-way attribution, narrative only | 68.4 |
| Six-way attribution, narrative + style | 77.3 |
| Gemini stories after LAMP style edits | 93.9 (95.5 before) |

Human stories were rarer in feature space (mean rarity percentile 0.71 vs 0.49). The human story was the rarest of the six versions of a prompt 57.8% of the time.

Per-class F1, narrative only: Human 88.5, Claude 77.1, GPT 73.0, then DeepSeek, Gemini and Kimi between 55.2 and 59.6.

## The 30 core features (Table 16 of the paper)

Gap = Human minus AI. Likert and ordinal rows are means; arrow rows are prevalence.

| Feature | Human | AI | Gap |
|---|---|---|---|
| **AI-elevated: thematic over-determination** | | | |
| Thematic explicitness and moralizing (1 to 5) | 3.28 | 3.94 | -0.65 |
| Moral / philosophical weighting (1 to 5) | 3.26 | 3.68 | -0.42 |
| Thematic unity (1 to 5) | 4.41 | 4.74 | -0.33 |
| Narrator comments on theme → yes | 52% | 77% | -25 |
| Dialogue function → philosophical debate | 34% | 59% | -25 |
| Reference explicitness → implicit echoes | 50% | 72% | -22 |
| **AI-elevated: sensory and embodied performativity** | | | |
| Emotional expression → embodied | 38% | 81% | -42 |
| Setting as psychological mirror (1 to 5) | 3.58 | 4.07 | -0.49 |
| Environmental emphasis (1 to 5) | 2.83 | 3.21 | -0.38 |
| Sensory modalities → olfactory | 57% | 82% | -26 |
| Sensory density (1 to 5) | 3.66 | 3.93 | -0.26 |
| Depth of interior access (1 to 5) | 3.67 | 3.93 | -0.26 |
| **AI-elevated: structural streamlining** | | | |
| Causal chain continuity (1 to 5) | 3.92 | 4.20 | -0.28 |
| Spatial granularity (ordinal) | 2.27 | 2.53 | -0.26 |
| Agency in resolution → protagonist choice | 46% | 69% | -23 |
| Character introduction → external description | 30% | 52% | -22 |
| Subplot integration → no subplots | 57% | 79% | -22 |
| Resolution mode → internal understanding | 27% | 47% | -21 |
| Opening spatial grounding (ordinal) | 2.12 | 2.33 | -0.20 |
| Pre-threat character investment (1 to 5) | 2.76 | 2.99 | -0.23 |
| **Human-elevated: intertextual richness** | | | |
| Intertextual strategy → explicit named reference | 47% | 24% | +23 |
| Reference explicitness → balanced mix | 37% | 16% | +21 |
| **Human-elevated: reader engagement** | | | |
| Fourth-wall permeability (ordinal) | 0.67 | 0.39 | +0.28 |
| Direct reader address (ordinal) | 0.28 | 0.07 | +0.21 |
| **Human-elevated: temporal complexity** | | | |
| Recontextualization after surprise (1 to 5) | 3.28 | 2.95 | +0.34 |
| Chronological discontinuity (1 to 5) | 2.40 | 2.12 | +0.28 |
| Nonlinear framing for delayed disclosure (1 to 5) | 1.96 | 1.68 | +0.28 |
| Anachrony intensity (1 to 5) | 2.58 | 2.31 | +0.27 |
| **Human-elevated: narrative diversity** | | | |
| Location variety (ordinal) | 1.34 | 1.08 | +0.26 |
| Dialogue-to-narration proportion (1 to 5) | 2.95 | 2.70 | +0.24 |
| Subplot integration → thematically parallel | 42% | 21% | +22 |
| Moral polarity → ambivalent / mixed | 59% | 38% | +21 |
| Emotional expression → explicit labels | 29% | 8% | +21 |

## Per-source fingerprints (Table 17, top 5 each)

Number of fingerprint features: Human 32, Claude 26, GPT 11, Gemini 11, DeepSeek 7, Kimi 3.

- **Human:** character introduced in dialogue; single focal character; narrator address mode → no direct address; back-loaded revelation; crossover genre ambition.
- **Claude:** weak event escalation; low event-type diversity; ending with epilogue or flash-forward; no dreams or visions; uncanny or haunted setting mood. Also honours literary convention in 62% of stories vs 39 to 56% for the others, and has the most uniform narrative voice.
- **GPT:** gossip and rumour as plot engine (64%); distant retrospective narrator; subverts reader expectations; no habitual narration; partial or ambiguous reconciliation.
- **Gemini:** protagonist's social circle expands; mostly direct speech; siege or ordeal schema; named personal names; frequent flashbacks. Tidiest endings, bleakest settings (88% bleak).
- **DeepSeek:** visible narrator; emotion via behavioural cues; atmosphere over plot; evenly interleaved backstory; embedded storytelling scenes. Front-loads context.
- **Kimi:** characters introduced in action; in medias res openings; no explicit trait labels. Sits at the generic centre of the AI cluster.

## Caveat

The study measures what makes AI fiction *detectable*. It does not claim that matching the human column makes writing better. Use the features as a check on defaults, not as a recipe.
