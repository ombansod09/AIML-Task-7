# AIML-Task-7
# ⚽ European Soccer Prediction: Support Vector Machines (SVM)

**Project Status:** Completed  
**Domain:** Sports Analytics / Classification  
**Dataset:** European Soccer Database (Hugo Mathien)

![Python](https://img.shields.io/badge/Python-3.8%2B-blue) ![Scikit-Learn](https://img.shields.io/badge/Library-Scikit--Learn-orange) ![SVM](https://img.shields.io/badge/Model-SVM-green)

## 1. Project Overview
This project applies **Support Vector Machines (SVM)** to the European Soccer Database to predict match outcomes. Specifically, we focus on a binary classification task: **Predicting if the Home Team will win** based on pre-match betting odds.

The goal is to visualize the decision boundary that separates a "Home Win" from a "Draw/Loss" using market data from major bookmakers (Bet365).

## 2. Methodology

### 2.1 Dataset Extraction
The data is stored in a SQLite database (`database.sqlite`). We executed SQL queries to extract the following from the `Match` table:
* **Target:** Calculated from `home_team_goal` vs `away_team_goal`. (1 = Home Win, 0 = Draw/Away Win).
* **Features:**
    * `B365H`: Bet365 odds for a Home Win.
    * `B365A`: Bet365 odds for an Away Win.

### 2.2 Preprocessing
* **Filtering:** Matches with null betting odds were removed to ensure data quality.
* **Scaling:** As SVMs are distance-based algorithms, `StandardScaler` was applied to normalize the odds, ensuring the hyperplane is not biased by the magnitude of the values.

### 2.3 Model Training & Tuning
We trained an SVM Classifier with the following process:
1.  **Grid Search:** Evaluated combinations of `C` (Regularization) and `gamma` (Kernel Coefficient).
2.  **Kernel:** Utilized the **RBF (Radial Basis Function)** kernel to capture non-linear relationships between the odds and the match outcome.

## 3. Key Findings

### Visualization
The 2D decision boundary plot reveals a clear separation:
* **Low Home Odds / High Away Odds:** The model confidently predicts a **Home Win** (Red Region).
* **High Home Odds / Low Away Odds:** The model predicts a **Draw or Loss** (Blue Region).
* **The Boundary:** The SVM successfully identified the "tipping point" in the odds where the probability shifts from a likely home win to a likely loss.

### Performance
The model achieves robust accuracy, effectively reverse-engineering the probability models used by bookmakers to set their lines.

## 4. Installation & Usage

### Prerequisites
* Python 3.x
* `database.sqlite` (Download from the [European Soccer Database](https://www.kaggle.com/datasets/hugomathien/soccer)) placed in the root directory.

### Execution
1.  **Install dependencies:**
    ```bash
    pip install pandas numpy matplotlib seaborn scikit-learn
    ```
2.  **Run the analysis:**
    ```bash
    python soccer_svm.py
    ```
