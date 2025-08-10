# Email Marketing Campaign Analysis

By **Akshat Garg**

Optimizing marketing campaigns is one of the most common data science tasks. Among the many marketing tools available, emails stand out as particularly efficient — free, scalable, and easily personalized. Email optimization involves personalizing content and/or the subject line, selecting recipients, and determining send times.

Python libraries like **NumPy**, **Pandas**, **Matplotlib**, **Seaborn**, **scikit-learn**, **XGBoost**, and others excel at analyzing the factors to maximize the probability of users clicking on links inside emails.

---

## Dataset Description

This dataset contains information from an email marketing campaign and is composed of **three relational tables**:

### 1. `email_table.csv`
Provides metadata about each email sent during the campaign.

| Column Name           | Description                                                                 |
|-----------------------|-----------------------------------------------------------------------------|
| `email_id`            | Unique identifier for each email sent.                                      |
| `email_text`          | "short" or "long" body text.                                                |
| `email_version`       | "personalized" (with user's name) or "generic".                             |
| `hour`                | Local hour when the email was sent.                                         |
| `weekday`             | Day of the week the email was sent.                                         |
| `user_country`        | Country of the user receiving the email.                                    |
| `user_past_purchases` | Number of past purchases by the user.                                       |

### 2. `email_opened_table.csv`
Tracks which emails were opened.

| Column Name | Description                     |
|-------------|---------------------------------|
| `email_id`  | ID of the email that was opened |

### 3. `link_clicked_table.csv`
Logs emails where the link was clicked.

| Column Name | Description                              |
|-------------|------------------------------------------|
| `email_id`  | ID of the email whose link was clicked   |

---

## Model Selection

To maximize click probability, I preferred the **SVM with Differential Evolution (DE)** optimization over other models. DE automatically tunes SVM hyperparameters like `C`, kernel type, and `gamma`, avoiding manual tuning and improving accuracy on complex datasets.

I also tested:
- Logistic Regression  
- Random Forest  
- XGBoost  
- Neural Network  
- Standard SVM  

---

### Model Performance: CTR Simulation

| Model                        | Original CTR | Simulated CTR (Top 20%) | Improvement |
|------------------------------|--------------|-------------------------|-------------|
| Random Forest Classifier     | 1.94%        | 2.44%                   | +0.50%      |
| XGBoost Classifier           | 1.94%        | 3.94%                   | +2.00%      |
| Logistic Regression          | 1.94%        | 4.76%                   | +2.82%      |
| Neural Network (Keras)       | 1.94%        | 4.38%                   | +2.44%      |
| Support Vector Machine       | 1.94%        | 2.00%                   | +0.06%      |
| SVM (Differential Evolution) | 45.00%       | 95.00%                  | +50.00%     |

---

### Why the Model is Not Overfitting

1. **Cross-validated accuracy**: `0.866` — consistent across data splits.  
2. **Balanced classes**:  
   - Class 0: 55  
   - Class 1: 45  
3. **Predicted probabilities**:

```text
[[0.8839, 0.1160],
 [0.9033, 0.0966],
 [0.9811, 0.0188],
 [0.7224, 0.2775],
 [0.8557, 0.1442],
 [0.0137, 0.9862],
 [0.0029, 0.9970],
 [0.2867, 0.7132],
 [0.2407, 0.7592],
 [0.6353, 0.3646]]
