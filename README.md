# A Comparative Explainable AI Study: Performance vs. Trustworthiness in Breast Cancer Prediction

## Project Overview

This research project moves beyond the conventional accuracy-first approach to evaluating machine learning models in a clinical context. Using the UCTH Breast Cancer Dataset, it investigates the critical trade-off between predictive performance and clinical trustworthiness.

The core of the study is a head-to-head comparison between:
1.  A **"Glass Box" Model:** A simple, inherently interpretable pruned Decision Tree.
2.  A **"Black Box" Model:** A complex, high-performance Neural Network.

By using the **SHAP (SHapley Additive exPlanations)** framework as a "universal translator," this study doesn't just ask "Which model is more accurate?" but rather, **"Which model provides the most useful and trustworthy guidance for a practicing doctor?"**

The full analysis, code, and visualizations are documented in the accompanying Jupyter Notebook: [`research.ipynb`](research.ipynb).

## Key Research Questions

The analysis is structured around four key questions:

-   **RQ1 (Performance):** How do the models' predictive metrics (AUC, F1-Score) compare?
-   **RQ2 (Global Explanation):** Do the models agree on the most important clinical drivers of malignancy?
-   **RQ3 (Local Explanation):** Are the explanations for individual patient cases stable, plausible, and trustworthy?
-   **RQ4 (Clinical Utility):** Can the insights be translated into a practical decision-support tool?

## Core Findings & Conclusion

The study yielded a series of powerful, and at times counter-intuitive, insights:

1.  **Surprising Performance Parity (RQ1):** Contrary to the common assumption that complexity yields higher accuracy, the simpler **"Glass Box" Decision Tree performed on par with, and on key metrics slightly better than, the "Black Box" Neural Network** on this dataset. This finding immediately challenges the default justification for using opaque models.

2.  **Consensus on Key Predictors (RQ2):** Both models identified `inv_nodes` (involved lymph nodes), `Metastasis`, and `tumor_size_cm` as the most critical clinical drivers for predicting malignancy. This consensus grounds the AI's logic in established clinical knowledge and builds foundational trust.

3.  **The 'Black Box' as a Crucial Safety Net (RQ3):** **This is the most critical finding of the study.** An analysis of a borderline case, where the models disagreed, revealed the true value of the complex model.
    -   The simple Decision Tree confidently made an **incorrect diagnosis** (a false positive), its rigid rules failing to account for countervailing evidence.
    -   The Neural Network, explained via SHAP, correctly identified the case as benign by holistically weighing both the risk factors and the mitigating factors. Its nuanced, "balanced committee" approach **prevented a significant clinical error**.

#### **Final Verdict:**
Trust in a clinical AI system is not merely about understanding its process but having confidence in its outcomes, especially in ambiguous situations. While a simple model is appealing, it can be dangerously brittle. The true value of a well-designed complex model is its potential to act as a **safety net**, preventing errors where simplistic rules fail.

## Proposed Clinical Application: A Hybrid Two-Tiered System

Based on these findings, we propose a prototype for a clinical decision-support tool that leverages the strengths of both models:

-   **Tier 1: Rapid Triage (Glass Box):** Use the simple, transparent Decision Tree rules (converted into a flowchart or checklist) for a quick initial assessment of straightforward cases.

-   **Tier 2: Automated Safety Net (Black Box):** If the Decision Tree makes a prediction but the Neural Network's output falls within a predefined "uncertainty zone" (e.g., a probability between 0.25 and 0.75), the system automatically flags the case with an alert: **"ALERT: Discordant Prediction. High model uncertainty. Recommend expert clinical review."**

This hybrid system provides clinicians with the speed of a simple tool for the majority of cases and a powerful, automated "second opinion" to catch the complex exceptions that often lead to diagnostic errors.

## Repository Structure

```
.
├── data/
│   └── breast-cancer-dataset.csv  
├── research_files/
│   └── (Generated images and plots from the notebook)
├── research.ipynb                 # The main Jupyter Notebook with all code and analysis.
└── README.md                      # This file.
```

## How to Use This Repository

To replicate this analysis, please follow these steps:

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/mcgmed/breast_cancer_prediction_with_XAI.git
    cd breast_cancer_prediction_with_XAI
    ```

2.  **Set up a virtual environment (recommended):**
    ```bash
    python -m venv venv
    source venv/bin/activate  # On Windows, use `venv\Scripts\activate`
    ```

3.  **Install the required dependencies:**
    A `requirements.txt` file can be generated from the notebook. For now, install the core packages:
    ```bash
    pip install pandas numpy matplotlib seaborn scikit-learn tensorflow shap
    ```

4.  **Run the Jupyter Notebook:**
    Launch Jupyter and open `research.ipynb` to explore the code, visualizations, and detailed findings.
    ```bash
    jupyter notebook research.ipynb
    ```

## Dependencies

-   Python 3.10+
-   pandas
-   numpy
-   matplotlib
-   seaborn
-   scikit-learn
-   tensorflow
-   shap
