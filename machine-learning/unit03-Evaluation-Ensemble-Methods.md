

# 📊 Unit 3: Evaluation and Ensemble Methods

## 1. Evaluating ML Algorithms and Model Selection

### Introduction
After training a machine learning model, it's crucial to assess its performance, particularly its ability to **generalize** to unseen data. Evaluation metrics and proper model selection techniques prevent common pitfalls like overfitting and underfitting.

### Core Concepts and Definitions
* **Generalization:** The model's ability to perform well on new, previously unseen data, rather than just memorizing the training data.
* **Overfitting:** When the model learns the training data and noise too well, resulting in high accuracy on the training set but **poor performance** on the test set (high variance).
* **Underfitting:** When the model is too simple to capture the underlying patterns in the data, resulting in **poor performance** on both training and test sets (high bias).
* **Bias-Variance Tradeoff:**
    * **Bias:** Error due to overly simplistic assumptions (underfitting).
    * **Variance:** Error due to excessive sensitivity to small fluctuations in the training data (overfitting).
    * The goal is to find the **sweet spot** that minimizes the total error (Bias$^2$ + Variance + Irreducible Error).

#### A. Data Splitting and Validation
* **Training Set:** Used to **train** the model (find optimal weights $\theta$).
* **Validation Set (Dev Set):** Used to **tune hyperparameters** (e.g., the $k$ in k-NN, $C$ in SVM, or tree depth in DT). This allows for model selection without touching the final test set.
* **Test Set:** Used only **once** at the very end to provide an unbiased estimate of the final model's generalization ability.
* **Cross-Validation (CV):** A technique to ensure all data points are used for both training and validation. **k-Fold Cross-Validation** is most common: the data is split into $k$ equal parts; the model is trained $k$ times, each time using one part for validation and the remaining $k-1$ parts for training. The final score is the average of the $k$ results.

#### B. Classification Metrics
Metrics used when the output $\mathbf{Y}$ is categorical.

| Metric | Formula / Definition | Use Case / Interpretation |
| :--- | :--- | :--- |
| **Accuracy** | $\frac{\text{Correct Predictions}}{\text{Total Predictions}}$ | Simple ratio. **Poor for imbalanced data** (where one class dominates). |
| **Precision** | $\frac{TP}{TP + FP}$ | Measures how many of the **predicted positive** instances were actually positive. |
| **Recall (Sensitivity)** | $\frac{TP}{TP + FN}$ | Measures how many of the **actual positive** instances were correctly identified. |
| **F1-Score** | Harmonic Mean of Precision and Recall. | Better balanced measure than accuracy, especially for imbalanced data. |
| **ROC AUC** | Area Under the Receiver Operating Characteristic Curve. | Measures the model's ability to distinguish between classes across all threshold settings. |

> **Keywords:** Generalization, Overfitting, Underfitting, Bias-Variance Tradeoff, k-Fold CV, Precision, Recall, F1-Score, ROC AUC, Confusion Matrix (TP, FP, TN, FN).

---

## 2. Introduction to Statistical Learning Theory

### Introduction
Statistical Learning Theory (SLT) provides the theoretical foundation for machine learning, helping us understand the fundamental question: **Why does a model trained on a finite dataset generalize well to infinite unseen data?**

### Core Concepts and Definitions
* **PAC Learning (Probably Approximately Correct):** A framework developed to define formal conditions under which a learning algorithm can guarantee generalization. The model should be:
    * **Approximately Correct:** Its error on new data should be small.
    * **Probably Correct:** This guarantee should hold with high probability.
* **Risk:** The expected error of the hypothesis ($h$) over the entire true distribution ($D$) of the data.
    $$R(h) = \mathbb{E}_{(\mathbf{x}, y) \sim D} [L(h(\mathbf{x}), y)]$$
* **Empirical Risk ($\hat{R}$):** The observed error of the hypothesis on the finite **training set** ($S$).
    $$\hat{R}(h) = \frac{1}{m} \sum_{i=1}^{m} L(h(\mathbf{x}_i), y_i)$$
* **Goal of SLT:** To ensure that the Empirical Risk (what we minimize in training) is close to the true Risk (what we care about in real-world use). This is achieved through the **Generalization Bound**.
* **VC Dimension (Vapnik-Chervonenkis Dimension):** A measure of the **capacity** or complexity of a hypothesis space ($\mathcal{H}$).
    * It quantifies the number of points a model can **shatter** (i.e., classify in all possible $2^m$ ways).
    * A higher VC dimension means a **more complex model** and a tighter fit on training data, leading to a wider gap between empirical and true risk (higher chance of overfitting).

> **Keywords:** PAC Learning, True Risk ($R$), Empirical Risk ($\hat{R}$), Generalization Bound, **VC Dimension**, Model Capacity, Shattering.

---

## 3. Ensemble Methods

### Introduction
**Ensemble Methods** combine the predictions of several individual weak learners (base models) to produce a single, highly accurate prediction. The central idea is that a group of diverse, relatively weak models can be much stronger than any single model alone.

### Core Concepts and Definitions
The two primary methods for creating ensembles are **Bagging** and **Boosting**.

#### A. Bagging (Bootstrap Aggregating)
* **Concept:** Trains several identical weak learners **in parallel** on different, randomly sampled subsets (with replacement, called **bootstrap samples**) of the original training data.
* **Goal:** To reduce **Variance** (addressing overfitting). By averaging the results of many high-variance models, the overall variance is stabilized.
* **Prediction:**
    * **Classification:** Uses a **majority vote**.
    * **Regression:** Uses the **average** of the predictions.
* **Random Forests:** A highly popular extension of Bagging applied to Decision Trees.
    * In addition to training each tree on a bootstrap sample of data, it only considers a **random subset of features** at each split in the tree.
    * This **decorrelates** the individual trees, making the ensemble even more robust.

#### B. Boosting
* **Concept:** Trains weak learners **sequentially** (in series). Each subsequent learner is trained to give more attention to the data points that the previous learners misclassified.
* **Goal:** To reduce **Bias** (turning weak learners into strong learners).
* **Mechanism (Adaptive):** Weights are assigned to data points. Misclassified points have their weights increased, forcing the next learner to focus on them.
* **Prediction:** Uses a **weighted majority vote** where stronger, more accurate learners (those trained later) have a higher voting weight.
* **Popular Algorithms:** **AdaBoost** (Adaptive Boosting), **Gradient Boosting (GBM)**, and **XGBoost/LightGBM**.

### Comparative Table

| Feature | Bagging (e.g., Random Forest) | Boosting (e.g., AdaBoost) |
| :--- | :--- | :--- |
| **Training Style** | Parallel (independent learners) | Sequential (dependent learners) |
| **Primary Goal** | Reduce **Variance** (overfitting) | Reduce **Bias** (underfitting) |
| **Data Focus** | Each learner sees a different, random subset. | Focuses on previous misclassified points. |
| **Final Prediction** | Simple majority vote/average | Weighted majority vote |

> **Keywords:** Ensemble, Weak Learner, **Bagging**, Bootstrap Sampling, **Random Forest**, **Boosting**, Sequential Training, Data Weights, AdaBoost, Decorrelation.

---

