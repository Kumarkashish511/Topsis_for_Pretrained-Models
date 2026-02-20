# 🤖 TOPSIS-Based Ranking of Pre-Trained Conversational AI Models

> A structured, data-driven framework for evaluating and comparing state-of-the-art conversational AI models using the **TOPSIS** multi-criteria decision-making method.

---

## 📌 What is This Project?

Choosing the right conversational AI model for your application is rarely straightforward — models differ across accuracy, speed, cost, context length, and safety. This project cuts through the noise using **TOPSIS (Technique for Order Preference by Similarity to Ideal Solution)**, a proven MCDM (Multi-Criteria Decision Making) algorithm that ranks alternatives by:

- ✅ Minimizing distance from the **ideal best** solution
- ✅ Maximizing distance from the **ideal worst** solution

The result: a transparent, reproducible, and quantitative ranking of popular LLMs.

---

## 🎯 Models Evaluated

| Model | Developer | Type |
|---|---|---|
| GPT-3.5 | OpenAI | Closed-source API |
| GPT-4 | OpenAI | Closed-source API |
| Gemini 1.5 | Google DeepMind | Closed-source API |
| LLaMA-2 Chat | Meta AI | Open-source |
| Claude 3 | Anthropic | Closed-source API |

---

## 📊 Evaluation Criteria

| Criterion | Type | Description | Weight |
|---|---|---|---|
| Accuracy | Benefit ↑ | Correctness and relevance of responses | 0.30 |
| Context Handling | Benefit ↑ | Ability to maintain long conversation context | 0.25 |
| Response Time | Cost ↓ | Lower latency is preferred | 0.15 |
| Cost per 1K Tokens | Cost ↓ | Lower inference cost is preferred | 0.15 |
| Safety | Benefit ↑ | Prevention of harmful or biased outputs | 0.15 |

> **Total Weight = 1.0** — Weights reflect typical production priorities, with accuracy and context handling valued most.

---

## 🧮 TOPSIS Methodology

TOPSIS ranks alternatives through a systematic 7-step process:

```
Step 1 → Build Decision Matrix         (models × criteria raw scores)
Step 2 → Normalize the Matrix          r_ij = x_ij / √(Σ x_ij²)
Step 3 → Apply Criteria Weights        v_ij = w_j × r_ij
Step 4 → Identify Ideal Best (A⁺)      max benefit / min cost per column
Step 5 → Identify Ideal Worst (A⁻)     min benefit / max cost per column
Step 6 → Compute Euclidean Distances   S_i⁺ and S_i⁻ for each model
Step 7 → Compute TOPSIS Score          C_i = S_i⁻ / (S_i⁺ + S_i⁻)
```

A model with **C_i → 1** is closest to the ideal best; **C_i → 0** means closest to the worst.

### Key Formulas

**Normalization:**

$$r_{ij} = \frac{x_{ij}}{\sqrt{\sum_{i=1}^{m} x_{ij}^2}}$$

**TOPSIS Score:**

$$C_i = \frac{S_i^-}{S_i^+ + S_i^-}$$

---

## 📁 Project Structure

```
Topsis_for_Pretrained-Models/
│
├── Data_Generation.ipynb     # Notebook: data setup, TOPSIS computation & visualization
├── topsis_results.csv        # Output: ranked models with scores (generated on run)
├── topsis_ranking_graph.png  # Output: bar chart visualization (generated on run)
└── README.md                 # Project documentation
```

---

## ▶️ Getting Started

### Prerequisites

Make sure you have Python 3.7+ installed, then install the required libraries:

```bash
pip install numpy pandas matplotlib
```

### Running the Notebook

```bash
jupyter notebook Data_Generation.ipynb
```

Run all cells from top to bottom. The notebook will:
1. Define the decision matrix with model scores
2. Execute the full TOPSIS pipeline
3. Export `topsis_results.csv` with final rankings
4. Display and save `topsis_ranking_graph.png`

---

## 📈 Sample Output

After execution, `topsis_results.csv` will contain a table like:

| Rank | Model | TOPSIS Score |
|---|---|---|
| 1 | GPT-4 | 0.812 |
| 2 | Claude 3 | 0.764 |
| 3 | Gemini 1.5 | 0.701 |
| 4 | GPT-3.5 | 0.543 |
| 5 | LLaMA-2 Chat | 0.389 |

> *Note: Scores are illustrative. Run the notebook to generate results based on actual input data.*

A bar chart (`topsis_ranking_graph.png`) visualizes the final scores for easy comparison.

---

## 🔍 Why TOPSIS?

TOPSIS is widely used in decision science for model selection, vendor evaluation, and benchmarking because it:

- Handles **conflicting criteria** (e.g., accuracy vs. cost)
- Supports **weighted preferences** reflecting real-world priorities
- Is **mathematically transparent** and interpretable
- Scales easily to **more models or criteria**

---

## 🔧 Extending This Project

You can adapt this framework to your use case by:

- **Adding new models** — extend the decision matrix with rows
- **Changing criteria weights** — adjust the weight vector to reflect different priorities (e.g., prioritize cost for a budget-conscious deployment)
- **Adding new criteria** — e.g., multilingual support, fine-tuning capability, license type
- **Replacing scores** — plug in benchmark data from MMLU, HellaSwag, HumanEval, etc.

---



## 👨‍💻 Author

**Kumar Kashish**
[GitHub Profile](https://github.com/Kumarkashish511)


