# CSC8646 – Generative AI for Business Coursework

This repository contains the coursework submission for the **Generative AI for Business** module (CSC8646). The project involves building and evaluating a commercial AI-powered children's interactive storytelling application across three tasks: a functional prototype, a marketing campaign, and a bias detection pipeline.

**Student:** Vivan Kushal Heneger  
**Student ID:** 250469037  
**Submission Deadline:** 20th February 2026

---

## Repository Structure

```
├── TASK1_GenAI.ipynb          # Task 1: Generative Storytelling App Prototype
├── TASK3_GenAI.ipynb          # Task 3: Bias Detection Pipeline
├── Generative_AI_Report.pdf   # Full Report (all three tasks)
├── Coursework.pdf             # Original coursework brief
└── README.md
```

> **Note:** A demo video (< 3 mins) for Task 1 is included in the submission zip.

---

## Task 1 – Generative Storytelling App [40 marks]

### Overview

A functional dual-interface prototype for an AI-powered children's interactive storytelling app, built using **Google AI Studio**. The app serves two user groups:

- **Parents** — set up story parameters (child's name, age, theme, setting, characters, moral/learning goal)
- **Children** — navigate through AI-generated scenes with interactive choices (Choice A / Choice B), illustrations, and audio narration

### Models Used

| Model | Role |
|---|---|
| Gemini 3.1 Pro | Core narrative generation, final architecture |
| Gemini 3 Flash | Fast JSON parsing, interactive UI, testing |

### Iterative Prompting Summary

| Iteration | Model | Technique | Outcome |
|---|---|---|---|
| 1 | Gemini 3.1 Pro | Basic prompt | Output too long, no structure |
| 2 | Gemini 3 Flash | JSON schema | Fast but generic choices |
| 3 (Final) | Gemini 3.1 Pro | System-user separation + JSON schema | Balanced safety, coherence, and interactivity |

### Key Architecture

```
Parent Input
    ↓
Prompt Construction (Safety Rules + User Inputs)
    ↓
Gemini 3.1 Pro API Call → Story JSON (150–200 words, 4 scenes)
    ↓
Parallel Asset Generation (AI Illustrations + TTS Audio)
    ↓
Child UI: Scene 1 → Choice A/B → Scene 2 → ... → Scene 4
    ↓
Final Summary + Moral → End
```

### Validation Results (50 edge-case prompts)

| Metric | Gemini 3 Flash | Gemini 3.1 Pro |
|---|---|---|
| Safety Failure Rate | 8% (4/50) | 0% |
| JSON Consistency | 99% | 100% |
| Latency | Low (3.1s avg) | Medium (5.5s avg) |
| Creative Depth | Moderate | High |

### How to Run

1. Open `TASK1_GenAI.ipynb` in Google Colab.
2. Add your **Google AI Studio API key** where indicated.
3. Run all cells to launch the prototype interface.
4. Enter parent inputs (child name, age, theme, setting, characters, moral) and click **Generate Story**.

```bash
# Required library
pip install google-generativeai
```

---

## Task 2 – Marketing Campaign [30 marks]

> Task 2 was completed entirely via prompting in Google AI Studio and ChatGPT. No notebook is included — all outputs and analysis are documented in `Generative_AI_Report.pdf`.

### Overview

A multi-modal marketing campaign was developed for the Generative Story Telling App targeting UK parents (ages 25–40) with children aged 4–8.

### Tools Used

- **Gemini Nano Banana** — Digital marketing poster generation (temperature testing: 0.3 / 0.7 / 0.9)
- **ChatGPT** — Instagram ad scripts (controlled vs creative), multimodal campaign concept, marketing plan

### Campaign Assets Produced

- 3 marketing posters (temperature variants: 0.3, 0.7, 0.9)
- 2 Instagram 15-second ad scripts (controlled and creative)
- 1 multimodal visual campaign concept
- Full marketing plan with budget, phases, KPIs, and financial projections

### Marketing Plan Summary

| Parameter | Value |
|---|---|
| Price | £4.99/month |
| Total Budget | £50,000 |
| Launch Market | UK |
| Target Audience | Parents aged 25–40, children aged 4–8 |
| Trial Offer | 7-day free trial |
| Projected Year 1 Revenue | ~£59,880 |

**Key Finding:** Temperature 0.7 produced the most balanced output — clear messaging with sufficient emotional appeal. Role-based prompting outperformed baseline prompting for persuasive content.

---

## Task 3 – Bias Detection [30 marks]

### Overview

A reproducible bias auditing pipeline was developed to analyse a dataset of 100 children's story premises (`premises.csv`) before integration into the app. The pipeline detects potential biases across gender representation, cultural signals, narrative themes, and role associations.

### Pipeline

```
Data Loading
    ↓
Text Normalisation
    ↓
Rule-Based Tagging (gender, culture, theme, role)
    ↓
Distribution & Cross-Tab Analysis
    ↓
Topic Modelling (TF-IDF + NMF)
    ↓
Bias Flagging
    ↓
Multi-Model LLM Validation (Gemini 1.5 Flash vs Gemini 1.5 Pro)
    ↓
Temperature Comparison (0.2 vs 0.8)
```

### Models & Configurations Compared

| Approach | Type | Prompting | Temperature | Agreement | Stability |
|---|---|---|---|---|---|
| Rule-Based Tagging | Deterministic | Lexicon-based | N/A | Baseline | 100% |
| Gemini 1.5 Flash | LLM | Baseline | 0.2 | Moderate | High |
| Gemini 1.5 Flash | LLM | Role-Based JSON | 0.8 | Higher | Lower |
| Gemini 1.5 Pro | LLM | Role-Based JSON | 0.2 | Highest | Very High |

### Key Findings

- **40%** of premises were male-coded vs **24%** female-coded
- Leadership signals appeared in **25%** of male-coded premises vs **8.3%** of female-coded premises
- **6%** of premises contained explicit cultural cues
- Temperature **0.2** with structured JSON prompting achieved the highest stability across runs
- **Gemini 1.5 Pro + Role-Based JSON + Temperature 0.2** was the most reliable audit configuration

### How to Run

1. Upload `premises.csv` to your Google Colab environment.
2. Open `TASK3_GenAI.ipynb` in Google Colab.
3. Add your **Google AI Studio API key** where indicated.
4. Run all cells to execute the full bias detection pipeline.

```bash
# Required libraries
pip install pandas scikit-learn matplotlib seaborn google-generativeai
```

---

## Requirements

- Python 3.8+
- Google Colab (recommended)
- Google AI Studio API key
- Libraries: `google-generativeai`, `pandas`, `scikit-learn`, `matplotlib`, `seaborn`

---

## References

- Bolukbasi et al. (2016) — Word embeddings and gender bias
- Bender et al. (2021) — Stochastic parrots and language model risks
- Livingstone & Helsper (2008) — Parental mediation of children's digital media
- Radesky & Christakis (2016) — Screen time and parental purchasing behaviour
- Google AI Studio Documentation & Responsible AI Resources
