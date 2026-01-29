# Data Science, AI & Machine Learning Interview Handbook

**Target Role:** Data Scientist, ML Engineer, AI Researcher, Applied Scientist  
**Focus:** Fundamentals to Advanced Production-Level Concepts

---

## Table of Contents

### Section 1 — Data Science Fundamentals
- What is Data Science
- Data Science vs ML vs AI vs DL
- Data Science Lifecycle
- Types of Analytics
- Statistical Thinking

### Section 2 — Statistics & Probability
- Descriptive Statistics
- Probability Distributions
- Hypothesis Testing
- A/B Testing
- Bayesian vs Frequentist
- Correlation vs Causation

### Section 3 — Mathematics for ML
- Linear Algebra Essentials
- Calculus for Optimization
- Gradient Descent
- Eigenvalues & Eigenvectors
- Matrix Operations

### Section 4 — Exploratory Data Analysis (EDA)
- Data Profiling
- Visualization Techniques
- Handling Missing Data
- Outlier Detection
- Feature Understanding

### Section 5 — Feature Engineering
- Feature Types
- Encoding Techniques
- Feature Scaling
- Feature Selection
- Feature Extraction
- Handling Imbalanced Data

### Section 6 — Supervised Learning
- Regression Algorithms
- Classification Algorithms
- Model Evaluation Metrics
- Bias-Variance Tradeoff
- Cross-Validation
- Hyperparameter Tuning

### Section 7 — Unsupervised Learning
- Clustering Algorithms
- Dimensionality Reduction
- Anomaly Detection
- Association Rules

### Section 8 — Ensemble Methods
- Bagging (Random Forest)
- Boosting (XGBoost, LightGBM)
- Stacking
- Voting

### Section 9 — Deep Learning Fundamentals
- Neural Network Architecture
- Activation Functions
- Loss Functions
- Optimizers
- Backpropagation
- Regularization Techniques

### Section 10 — Convolutional Neural Networks (CNN)
- CNN Architecture
- Convolution Operations
- Pooling Layers
- Famous Architectures (VGG, ResNet)
- Transfer Learning
- Image Classification

### Section 11 — Recurrent Neural Networks (RNN)
- RNN Architecture
- Vanishing Gradient Problem
- LSTM & GRU
- Sequence-to-Sequence
- Bidirectional RNNs

### Section 12 — Natural Language Processing (NLP)
- Text Preprocessing
- Word Embeddings
- Transformers & Attention
- BERT, GPT Architecture
- Text Classification
- Named Entity Recognition
- Sentiment Analysis

### Section 13 — Large Language Models (LLMs)
- LLM Architecture
- Prompt Engineering
- Fine-Tuning Strategies
- RAG (Retrieval Augmented Generation)
- LLM Evaluation
- Deployment Considerations

### Section 14 — Computer Vision
- Image Processing Basics
- Object Detection
- Image Segmentation
- GANs
- Vision Transformers

### Section 15 — Model Training & Optimization
- Training Loop
- Batch Size & Learning Rate
- Regularization
- Early Stopping
- Learning Rate Scheduling
- Mixed Precision Training

### Section 16 — MLOps & Model Deployment
- ML Pipeline Architecture
- Experiment Tracking
- Model Versioning
- Model Serving
- Monitoring & Drift Detection
- A/B Testing in Production

### Section 17 — Interview Scenarios & Case Studies
- Business Problem Framing
- Model Selection Scenarios
- Production Issues
- Ethics & Bias

---

## Section 1 — Data Science Fundamentals

### What is Data Science?

> **ELI5**: Data Science is like being a detective who uses math and computers to find hidden patterns in data and make predictions. Instead of solving crimes, you solve business problems.

**Definition**: Data Science is an interdisciplinary field that uses scientific methods, algorithms, and systems to extract insights and knowledge from structured and unstructured data.

**The Data Science Venn Diagram**:
```
        ┌─────────────────┐
        │  Domain/Business│
        │   Expertise     │
        └────────┬────────┘
                 │
    ┌────────────┼────────────┐
    │            │            │
┌───▼───┐   ┌────▼────┐   ┌───▼───┐
│ Math/ │   │  DATA   │   │ Comp  │
│ Stats │◄──┤ SCIENCE ├──►│Science│
│       │   │         │   │Hacking│
└───────┘   └─────────┘   └───────┘
```

---

### Data Science vs ML vs AI vs Deep Learning

| Term | Definition | Relationship |
|:---|:---|:---|
| **AI** | Machines mimicking human intelligence | Broadest category |
| **Machine Learning** | Algorithms that learn from data | Subset of AI |
| **Deep Learning** | ML using neural networks with many layers | Subset of ML |
| **Data Science** | Extracting insights from data using various techniques | Uses ML as one tool |

```
┌────────────────────────────────────────────────────┐
│              Artificial Intelligence               │
│  ┌──────────────────────────────────────────────┐  │
│  │            Machine Learning                  │  │
│  │  ┌────────────────────────────────────────┐  │  │
│  │  │         Deep Learning                  │  │  │
│  │  │   (Neural Networks)                    │  │  │
│  │  └────────────────────────────────────────┘  │  │
│  └──────────────────────────────────────────────┘  │
└────────────────────────────────────────────────────┘
```

---

### Types of Analytics

| Type | Question Answered | Complexity | Example |
|:---|:---|:---|:---|
| **Descriptive** | What happened? | Low | Sales report last quarter |
| **Diagnostic** | Why did it happen? | Medium | Why did sales drop in March? |
| **Predictive** | What will happen? | High | Forecast next quarter sales |
| **Prescriptive** | What should we do? | Highest | Optimal pricing strategy |

---

## Section 2 — Statistics & Probability

### Descriptive Statistics

**Measures of Central Tendency**:
| Measure | Formula | When to Use |
|:---|:---|:---|
| **Mean** | Σx / n | Symmetric distributions, no outliers |
| **Median** | Middle value | Skewed data, has outliers |
| **Mode** | Most frequent | Categorical data |

**Measures of Spread**:
| Measure | Description | Formula |
|:---|:---|:---|
| **Range** | Max - Min | Simple but sensitive to outliers |
| **Variance** | Average squared deviation | σ² = Σ(x - μ)² / n |
| **Standard Deviation** | Square root of variance | σ = √variance |
| **IQR** | Q3 - Q1 | Robust to outliers |

---

### Probability Distributions

**Discrete Distributions**:

| Distribution | Use Case | Parameters |
|:---|:---|:---|
| **Bernoulli** | Single yes/no trial | p (success probability) |
| **Binomial** | Number of successes in n trials | n, p |
| **Poisson** | Count of events in fixed interval | λ (average rate) |

**Continuous Distributions**:

| Distribution | Use Case | Parameters |
|:---|:---|:---|
| **Normal (Gaussian)** | Natural phenomena, errors | μ (mean), σ (std dev) |
| **Exponential** | Time between events | λ (rate) |
| **Uniform** | Equal probability in range | a (min), b (max) |

**Normal Distribution Properties**:
```
         ┌───────────────────────┐
         │                       │
     ────│───────────────────────│────
    -3σ  │   -2σ  -1σ  μ  +1σ +2σ│  +3σ
         │       68.2%           │
         │         95.4%         │
         │          99.7%        │
         └───────────────────────┘

• 68% of data within 1σ of mean
• 95% of data within 2σ of mean
• 99.7% of data within 3σ of mean
```

---

### Hypothesis Testing

**Process**:
1. State null hypothesis (H₀) and alternative (H₁)
2. Choose significance level (α, typically 0.05)
3. Calculate test statistic
4. Compute p-value
5. Reject H₀ if p-value < α

**Common Tests**:
| Test | Use Case |
|:---|:---|
| **t-test** | Compare means of two groups |
| **Chi-square** | Categorical variable independence |
| **ANOVA** | Compare means of 3+ groups |
| **Mann-Whitney U** | Non-parametric comparison |

**Errors**:
| | H₀ True | H₀ False |
|:---|:---|:---|
| **Reject H₀** | Type I Error (α) | Correct! |
| **Fail to Reject H₀** | Correct! | Type II Error (β) |

- **Type I (α)**: False positive - "crying wolf"
- **Type II (β)**: False negative - "missing the wolf"
- **Power = 1 - β**: Probability of detecting true effect

---

### A/B Testing

**Steps**:
1. **Define metric**: Conversion rate, revenue per user
2. **Calculate sample size**: Need enough power (80%+)
3. **Randomize users**: Control vs Treatment
4. **Run experiment**: Wait for statistical significance
5. **Analyze results**: Is difference significant & practical?

**Sample Size Formula**:
```
n = (2 * (Z_α + Z_β)² * σ²) / δ²

Where:
- Z_α = Z-score for significance (1.96 for 95%)
- Z_β = Z-score for power (0.84 for 80%)
- σ = standard deviation
- δ = minimum detectable effect
```

**Common Pitfalls**:
- **Peeking**: Checking results too early inflates Type I error
- **Multiple comparisons**: Testing many variants without correction
- **Simpson's Paradox**: Aggregate trend reverses in subgroups
- **Novelty effect**: Users behave differently just because it's new

---

### Correlation vs Causation

**Correlation**: Two variables move together
- Pearson: Linear relationship (-1 to 1)
- Spearman: Monotonic relationship (rank-based)

**Causation**: One variable directly affects another

**Why correlation ≠ causation**:
1. **Confounding variable**: Third variable causes both
2. **Reverse causality**: Effect causes the cause
3. **Coincidence**: Random correlation

**Establishing causation requires**:
- Randomized controlled experiments (A/B tests)
- Causal inference techniques (propensity matching, instrumental variables)

---

## Section 3 — Mathematics for ML

### Linear Algebra Essentials

**Vectors**:
```
a = [1, 2, 3]  # Row vector
    ┌ 1 ┐
b = │ 2 │      # Column vector
    └ 3 ┘

Dot Product: a · b = a₁b₁ + a₂b₂ + a₃b₃ = scalar
```

**Matrices**:
```
    ┌ 1  2  3 ┐
A = │ 4  5  6 │   Shape: 2×3 (rows × columns)
    └         ┘

Matrix Multiplication:
(m×n) × (n×p) = (m×p)

C = AB where C[i,j] = Σ A[i,k] × B[k,j]
```

**Key Operations**:
| Operation | Description | Use in ML |
|:---|:---|:---|
| **Transpose** | Flip rows/columns (Aᵀ) | Data reshaping |
| **Inverse** | A⁻¹ where AA⁻¹ = I | Solving linear systems |
| **Determinant** | Scalar representing matrix | Singularity check |

---

### Gradient Descent

**Concept**: Iteratively move in direction of steepest decrease to find minimum.

```
θ_new = θ_old - α * ∇J(θ)

Where:
- θ = parameters
- α = learning rate
- ∇J(θ) = gradient of loss function
```

**Variants**:
| Type | Batch Size | Pros | Cons |
|:---|:---|:---|:---|
| **Batch GD** | All data | Stable | Slow, memory-heavy |
| **Stochastic GD** | 1 sample | Fast, online learning | Noisy |
| **Mini-batch GD** | 32-512 | Best of both | Hyperparameter tuning |

**Learning Rate Impact**:
- **Too high**: Overshoots, may diverge
- **Too low**: Very slow convergence
- **Just right**: Smooth convergence to minimum

---

## Section 4 — Exploratory Data Analysis (EDA)

### EDA Checklist

```python
import pandas as pd
import numpy as np

# 1. Basic Info
df.shape                    # Rows, columns
df.dtypes                   # Data types
df.info()                   # Memory, non-null counts
df.describe()               # Statistical summary

# 2. Missing Values
df.isnull().sum()           # Count per column
df.isnull().sum() / len(df) # Percentage missing

# 3. Unique Values
df.nunique()                # Unique count per column
df['col'].value_counts()    # Frequency distribution

# 4. Duplicates
df.duplicated().sum()       # Count duplicates

# 5. Correlations
df.corr()                   # Correlation matrix
```

---

### Handling Missing Data

| Method | When to Use | Implementation |
|:---|:---|:---|
| **Drop rows** | < 5% missing, random | `df.dropna()` |
| **Drop columns** | > 50% missing | `df.drop(columns=[...])` |
| **Mean/Median** | Numerical, no outliers | `df.fillna(df.mean())` |
| **Mode** | Categorical | `df.fillna(df.mode()[0])` |
| **Forward/Backward fill** | Time series | `df.fillna(method='ffill')` |
| **Interpolation** | Time series, smooth | `df.interpolate()` |
| **Model-based** | Complex patterns | KNN, regression imputation |

---

### Outlier Detection

**Statistical Methods**:
```python
# Z-Score: > 3 standard deviations
z_scores = (df['col'] - df['col'].mean()) / df['col'].std()
outliers = df[abs(z_scores) > 3]

# IQR Method
Q1 = df['col'].quantile(0.25)
Q3 = df['col'].quantile(0.75)
IQR = Q3 - Q1
outliers = df[(df['col'] < Q1 - 1.5*IQR) | (df['col'] > Q3 + 1.5*IQR)]
```

**Handling Outliers**:
- **Remove**: If errors or irrelevant
- **Cap/Floor**: Winsorization (clip to percentiles)
- **Transform**: Log transform to reduce impact
- **Keep**: If legitimate extreme values

---

## Section 5 — Feature Engineering

### Encoding Techniques

**Categorical Encoding**:

| Method | Use Case | Example |
|:---|:---|:---|
| **Label Encoding** | Ordinal categories | Low=0, Medium=1, High=2 |
| **One-Hot Encoding** | Nominal categories | Color → [is_red, is_blue, is_green] |
| **Binary Encoding** | High cardinality | ID → binary representation |
| **Target Encoding** | Categorical + regression | Replace with target mean |

```python
# One-Hot Encoding
pd.get_dummies(df, columns=['category'])

# Label Encoding
from sklearn.preprocessing import LabelEncoder
le = LabelEncoder()
df['category_encoded'] = le.fit_transform(df['category'])
```

---

### Feature Scaling

| Method | Formula | When to Use |
|:---|:---|:---|
| **Min-Max (Normalization)** | (x - min) / (max - min) | Neural networks, KNN |
| **Standardization (Z-score)** | (x - μ) / σ | Linear models, SVM |
| **Robust Scaling** | (x - median) / IQR | Data with outliers |

```python
from sklearn.preprocessing import StandardScaler, MinMaxScaler

scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)
```

**When Scaling Matters**:
- ✅ Distance-based: KNN, K-Means, SVM
- ✅ Gradient-based: Neural Networks, Linear Regression
- ❌ Tree-based: Decision Trees, Random Forest, XGBoost

---

### Feature Selection

| Method | Type | Description |
|:---|:---|:---|
| **Correlation** | Filter | Remove highly correlated features |
| **Variance Threshold** | Filter | Remove low variance features |
| **Chi-Square** | Filter | Categorical feature importance |
| **Mutual Information** | Filter | Non-linear relationships |
| **RFE** | Wrapper | Recursively remove least important |
| **L1 Regularization** | Embedded | LASSO drives coefficients to zero |
| **Feature Importance** | Embedded | Tree-based importance scores |

---

### Handling Imbalanced Data

| Technique | Description | When to Use |
|:---|:---|:---|
| **Oversampling (SMOTE)** | Generate synthetic minority samples | More data is helpful |
| **Undersampling** | Remove majority samples | Have lots of data |
| **Class Weights** | Penalize minority class errors more | Simple approach |
| **Threshold Adjustment** | Lower classification threshold | Maximize recall |
| **Ensemble Methods** | BalancedRandomForest | Robust approach |

```python
from imblearn.over_sampling import SMOTE

smote = SMOTE(random_state=42)
X_resampled, y_resampled = smote.fit_resample(X, y)
```

---

## Section 6 — Supervised Learning

### Regression Algorithms

| Algorithm | Pros | Cons | Use Case |
|:---|:---|:---|:---|
| **Linear Regression** | Simple, interpretable | Assumes linearity | Baseline, simple relationships |
| **Ridge (L2)** | Handles multicollinearity | All features kept | Many correlated features |
| **Lasso (L1)** | Feature selection | Can be unstable | Feature selection needed |
| **Elastic Net** | Best of L1 + L2 | Two hyperparameters | High-dim data |
| **Decision Tree** | Non-linear, interpretable | Overfits easily | Explainability needed |
| **Random Forest** | Robust, handles non-linearity | Black box | General purpose |
| **XGBoost** | State-of-the-art accuracy | Needs tuning | Kaggle competitions |

**Regression Metrics**:
| Metric | Formula | Interpretation |
|:---|:---|:---|
| **MAE** | Σ\|y - ŷ\| / n | Average absolute error |
| **MSE** | Σ(y - ŷ)² / n | Penalizes large errors |
| **RMSE** | √MSE | Same units as target |
| **R²** | 1 - (SS_res / SS_tot) | Variance explained (0-1) |
| **MAPE** | Σ\|(y - ŷ)/y\| / n | Percentage error |

---

### Classification Algorithms

| Algorithm | Pros | Cons | Use Case |
|:---|:---|:---|:---|
| **Logistic Regression** | Probabilistic, interpretable | Linear decision boundary | Baseline, probability needed |
| **KNN** | Simple, no training | Slow prediction, curse of dim | Small datasets |
| **SVM** | Effective in high dim | Memory-intensive | Text classification |
| **Naive Bayes** | Fast, works with small data | Independence assumption | Text, spam filtering |
| **Decision Tree** | Interpretable, handles mixed data | Overfits | Explainability needed |
| **Random Forest** | Robust, feature importance | Slower than single tree | General purpose |
| **XGBoost/LightGBM** | Best accuracy | Needs tuning, black box | Competitions, production |

---

### Classification Metrics

**Confusion Matrix**:
```
                    Predicted
                  Pos      Neg
Actual   Pos      TP       FN
         Neg      FP       TN
```

| Metric | Formula | When to Optimize |
|:---|:---|:---|
| **Accuracy** | (TP+TN) / Total | Balanced classes |
| **Precision** | TP / (TP+FP) | Minimize false positives (spam) |
| **Recall** | TP / (TP+FN) | Minimize false negatives (disease) |
| **F1-Score** | 2 × (P×R)/(P+R) | Balance precision/recall |
| **AUC-ROC** | Area under ROC curve | Ranking ability |
| **Log Loss** | -Σ(y log(p)) | Probability calibration |

**When to Use Which**:
- **Fraud Detection**: High recall (catch all fraud) → accept some false positives
- **Spam Filter**: High precision (don't block legitimate email)
- **Medical Diagnosis**: High recall (don't miss diseases)

---

### Bias-Variance Tradeoff

```
Total Error = Bias² + Variance + Irreducible Error

High Bias (Underfitting)         High Variance (Overfitting)
├── Model too simple             ├── Model too complex
├── High training error          ├── Low training error
├── High test error              ├── High test error
└── Increase complexity          └── Simplify, regularize
```

**Solutions**:
| Problem | Solutions |
|:---|:---|
| **High Bias** | More features, less regularization, more complex model |
| **High Variance** | More data, regularization, simpler model, ensemble |

---

### Cross-Validation

**K-Fold Cross-Validation**:
```
Fold 1: [Test] [Train] [Train] [Train] [Train]
Fold 2: [Train] [Test] [Train] [Train] [Train]
Fold 3: [Train] [Train] [Test] [Train] [Train]
Fold 4: [Train] [Train] [Train] [Test] [Train]
Fold 5: [Train] [Train] [Train] [Train] [Test]

Final Score = Average of 5 fold scores
```

**Types**:
| Type | Use Case |
|:---|:---|
| **K-Fold** | Standard, balanced data |
| **Stratified K-Fold** | Imbalanced classification |
| **Time Series Split** | Temporal data (no future leakage) |
| **Leave-One-Out** | Very small datasets |

```python
from sklearn.model_selection import cross_val_score, StratifiedKFold

cv = StratifiedKFold(n_splits=5, shuffle=True, random_state=42)
scores = cross_val_score(model, X, y, cv=cv, scoring='f1')
```

---

## Section 7 — Unsupervised Learning

### Clustering Algorithms

| Algorithm | Pros | Cons | Best For |
|:---|:---|:---|:---|
| **K-Means** | Fast, scalable | Needs K, spherical clusters | Large datasets, clear clusters |
| **Hierarchical** | Dendrogram visualization | Slow for large data | Small data, any K |
| **DBSCAN** | Finds arbitrary shapes, handles noise | Sensitive to parameters | Spatial data, outliers |
| **Gaussian Mixture** | Soft clustering, probabilistic | Assumes Gaussian | Overlapping clusters |

**Choosing K (K-Means)**:
- **Elbow Method**: Plot inertia vs K, look for "elbow"
- **Silhouette Score**: Measure cluster cohesion (-1 to 1)

```python
from sklearn.cluster import KMeans
from sklearn.metrics import silhouette_score

for k in range(2, 10):
    kmeans = KMeans(n_clusters=k, random_state=42)
    labels = kmeans.fit_predict(X)
    score = silhouette_score(X, labels)
    print(f"K={k}, Silhouette={score:.3f}")
```

---

### Dimensionality Reduction

| Method | Type | Use Case |
|:---|:---|:---|
| **PCA** | Linear | Visualization, noise reduction |
| **t-SNE** | Non-linear | 2D/3D visualization |
| **UMAP** | Non-linear | Faster than t-SNE, preserves structure |
| **LDA** | Supervised | Classification preprocessing |

**PCA Steps**:
1. Standardize data
2. Compute covariance matrix
3. Find eigenvectors/eigenvalues
4. Select top k components
5. Transform data

```python
from sklearn.decomposition import PCA

pca = PCA(n_components=0.95)  # Retain 95% variance
X_reduced = pca.fit_transform(X)
print(f"Reduced to {pca.n_components_} components")
```

---

## Section 8 — Ensemble Methods

### Bagging vs Boosting

| Aspect | Bagging | Boosting |
|:---|:---|:---|
| **Training** | Parallel | Sequential |
| **Data sampling** | With replacement | Weighted by errors |
| **Goal** | Reduce variance | Reduce bias |
| **Example** | Random Forest | XGBoost, LightGBM |
| **Overfitting** | Less prone | Can overfit |

---

### Random Forest

```
     ┌─────────────────────────────────────────────────┐
     │             Bootstrap Samples                   │
     │   ┌─────┐   ┌─────┐   ┌─────┐       ┌─────┐     │
     │   │Tree1│   │Tree2│   │Tree3│  ...  │TreeN│     │
     │   └──┬──┘   └──┬──┘   └──┬──┘       └──┬──┘     │
     └──────┼────────┼────────┼────────────────┼───────┘
            │        │        │                │
            ▼        ▼        ▼                ▼
         ┌────────────────────────────────────────┐
         │          Aggregate (Vote/Average)      │
         └────────────────────────────────────────┘
                           │
                           ▼
                    Final Prediction
```

**Key Hyperparameters**:
- `n_estimators`: Number of trees
- `max_depth`: Tree depth (prevent overfitting)
- `min_samples_split`: Minimum samples to split
- `max_features`: Features considered per split

---

### XGBoost / LightGBM

**XGBoost (Extreme Gradient Boosting)**:
- Regularized objective function (L1 + L2)
- Handles missing values
- Parallel tree construction
- Built-in cross-validation

```python
import xgboost as xgb

params = {
    'objective': 'binary:logistic',
    'eval_metric': 'auc',
    'max_depth': 6,
    'learning_rate': 0.1,
    'n_estimators': 100,
    'subsample': 0.8,
    'colsample_bytree': 0.8,
    'reg_alpha': 0.1,  # L1
    'reg_lambda': 1.0  # L2
}

model = xgb.XGBClassifier(**params)
model.fit(X_train, y_train, eval_set=[(X_val, y_val)], early_stopping_rounds=10)
```

**LightGBM Advantages**:
- Leaf-wise growth (faster)
- Handles large datasets
- Native categorical support
- Lower memory usage

---

## Section 9 — Deep Learning Fundamentals

### Neural Network Architecture

```
Input Layer      Hidden Layers      Output Layer
   (x)              (h)                (y)
    
   ○─────────┐
             ├───○────┐
   ○─────────┤        ├───○────┐
             ├───○────┤        ├───○
   ○─────────┤        ├───○────┘
             ├───○────┘
   ○─────────┘

Each connection has a weight (w)
Each neuron: output = activation(Σ(inputs × weights) + bias)
```

---

### Activation Functions

| Function | Formula | Output Range | Use Case |
|:---|:---|:---|:---|
| **Sigmoid** | 1/(1+e⁻ˣ) | (0, 1) | Binary output, probability |
| **Tanh** | (eˣ-e⁻ˣ)/(eˣ+e⁻ˣ) | (-1, 1) | Hidden layers |
| **ReLU** | max(0, x) | [0, ∞) | Default for hidden layers |
| **Leaky ReLU** | max(0.01x, x) | (-∞, ∞) | Prevents dying ReLU |
| **Softmax** | eˣⁱ/Σeˣʲ | (0, 1), sum=1 | Multi-class output |

**ReLU is Default Because**:
- Computationally efficient
- No vanishing gradient (for positive values)
- Sparse activation (some neurons = 0)

---

### Loss Functions

| Task | Loss Function | Formula |
|:---|:---|:---|
| **Regression** | MSE | Σ(y - ŷ)² / n |
| **Regression** | MAE | Σ\|y - ŷ\| / n |
| **Binary Classification** | Binary Cross-Entropy | -Σ(y log(p) + (1-y)log(1-p)) |
| **Multi-class** | Categorical Cross-Entropy | -Σ y_i log(p_i) |

---

### Optimizers

| Optimizer | Description | When to Use |
|:---|:---|:---|
| **SGD** | Basic gradient descent | Baseline, with momentum |
| **Momentum** | Accelerates SGD | Faster convergence |
| **RMSprop** | Adaptive learning rate | RNNs |
| **Adam** | Momentum + RMSprop | Default choice |
| **AdamW** | Adam with weight decay | Transformers |

**Adam** is most common:
```python
optimizer = torch.optim.Adam(model.parameters(), lr=0.001)
```

---

### Regularization Techniques

| Technique | Description | When to Use |
|:---|:---|:---|
| **L1 (Lasso)** | Adds \|weights\| to loss | Feature selection |
| **L2 (Ridge)** | Adds weights² to loss | Prevent large weights |
| **Dropout** | Randomly zero neurons | Deep networks |
| **Batch Normalization** | Normalize layer inputs | Faster training |
| **Early Stopping** | Stop when val loss increases | Prevent overfitting |
| **Data Augmentation** | Create variations of data | Limited training data |

```python
import torch.nn as nn

model = nn.Sequential(
    nn.Linear(100, 64),
    nn.BatchNorm1d(64),
    nn.ReLU(),
    nn.Dropout(0.3),
    nn.Linear(64, 10)
)
```

---

## Section 10 — Convolutional Neural Networks (CNN)

### CNN Architecture

```
Input Image → [Conv → ReLU → Pool] × N → Flatten → FC → Output
                 ↓
           Feature Maps
```

**Components**:
| Layer | Purpose | Parameters |
|:---|:---|:---|
| **Convolution** | Extract features | Kernel size, stride, padding |
| **Activation** | Non-linearity | ReLU |
| **Pooling** | Reduce dimensions | Max/Average, size |
| **Flatten** | 2D → 1D | - |
| **Fully Connected** | Classification | Neurons |

---

### Convolution Operation

```
Input (5×5)          Kernel (3×3)         Output (3×3)
┌─────────────┐     ┌─────────┐         ┌─────────┐
│ 1 0 1 0 1   │     │ 1 0 1   │         │ 4 3 4   │
│ 0 1 0 1 0   │  *  │ 0 1 0   │    =    │ 2 4 3   │
│ 1 0 1 0 1   │     │ 1 0 1   │         │ 2 3 4   │
│ 0 1 0 1 0   │     └─────────┘         └─────────┘
│ 1 0 1 0 1   │
└─────────────┘

Output size = (Input - Kernel + 2*Padding) / Stride + 1
```

---

### Famous CNN Architectures

| Architecture | Year | Key Innovation |
|:---|:---|:---|
| **LeNet** | 1998 | First successful CNN |
| **AlexNet** | 2012 | Deep CNN, ReLU, Dropout |
| **VGG** | 2014 | Very deep (16-19 layers), 3×3 kernels |
| **GoogLeNet/Inception** | 2014 | Inception modules, 1×1 convolutions |
| **ResNet** | 2015 | Skip connections, 152+ layers |
| **EfficientNet** | 2019 | Compound scaling |

---

### Transfer Learning

```python
import torchvision.models as models
import torch.nn as nn

# Load pretrained model
model = models.resnet50(pretrained=True)

# Freeze base layers
for param in model.parameters():
    param.requires_grad = False

# Replace classifier
model.fc = nn.Sequential(
    nn.Linear(2048, 512),
    nn.ReLU(),
    nn.Dropout(0.3),
    nn.Linear(512, num_classes)
)
```

**When to Use**:
- Limited training data
- Similar domain to pretrained model
- Faster training

---

## Section 11 — Recurrent Neural Networks (RNN)

### RNN Architecture

```
        ┌────────────────────────────────────────┐
        │              Hidden State              │
        │    h₀ ──→ h₁ ──→ h₂ ──→ h₃ ──→ h₄      │
        │     ↑      ↑      ↑      ↑      ↑      │
        └─────┼──────┼──────┼──────┼──────┼──────┘
              │      │      │      │      │
Input:       x₀     x₁     x₂     x₃     x₄
              │      │      │      │      │
Output:      y₀     y₁     y₂     y₃     y₄
```

**Problem**: Vanishing/Exploding gradients for long sequences

---

### LSTM (Long Short-Term Memory)

```
┌────────────────────────────────────────────────────┐
│                     LSTM Cell                      │
│                                                    │
│   ┌──────┐   ┌──────┐   ┌──────┐   ┌───────┐       │
│   │Forget│   │Input │   │ Cell │   │Output │       │
│   │ Gate │   │ Gate │   │State │   │ Gate  │       │
│   └──────┘   └──────┘   └──────┘   └───────┘       │
│      fₜ         iₜ         Cₜ         oₜ             │
│                                                    │
│   What to     What to    Long      What to         │
│   forget      add        term      output          │
│                          memory                    │
└────────────────────────────────────────────────────┘
```

**Gates**:
- **Forget Gate**: What to remove from cell state
- **Input Gate**: What new info to store
- **Output Gate**: What to output

---

### GRU (Gated Recurrent Unit)

- Simplified LSTM
- Fewer parameters (faster training)
- Two gates: Reset and Update

```python
import torch.nn as nn

# LSTM
lstm = nn.LSTM(input_size=100, hidden_size=256, num_layers=2, 
               batch_first=True, bidirectional=True, dropout=0.3)

# GRU
gru = nn.GRU(input_size=100, hidden_size=256, num_layers=2,
             batch_first=True, bidirectional=True, dropout=0.3)
```

---

## Section 12 — Natural Language Processing (NLP)

### Text Preprocessing Pipeline

```python
import re
import nltk
from nltk.tokenize import word_tokenize
from nltk.corpus import stopwords
from nltk.stem import WordNetLemmatizer

def preprocess(text):
    # Lowercase
    text = text.lower()
    # Remove special characters
    text = re.sub(r'[^a-zA-Z\s]', '', text)
    # Tokenize
    tokens = word_tokenize(text)
    # Remove stopwords
    stop_words = set(stopwords.words('english'))
    tokens = [t for t in tokens if t not in stop_words]
    # Lemmatize
    lemmatizer = WordNetLemmatizer()
    tokens = [lemmatizer.lemmatize(t) for t in tokens]
    return tokens
```

---

### Word Embeddings

| Method | Description | Pros/Cons |
|:---|:---|:---|
| **One-Hot** | Binary vector per word | Sparse, no semantics |
| **TF-IDF** | Term frequency × inverse doc freq | Better, still sparse |
| **Word2Vec** | Dense vectors from context | Captures semantics |
| **GloVe** | Global word co-occurrence | Better for analogies |
| **FastText** | Subword embeddings | Handles OOV words |

**Word2Vec Example**:
```python
from gensim.models import Word2Vec

sentences = [["king", "queen", "royal"], ["man", "woman", "person"]]
model = Word2Vec(sentences, vector_size=100, window=5, min_count=1)

# Word similarity
model.wv.most_similar("king")

# Analogy: king - man + woman = queen
model.wv.most_similar(positive=['king', 'woman'], negative=['man'])
```

---

### Transformers & Attention

**Self-Attention Mechanism**:
```
Attention(Q, K, V) = softmax(QKᵀ / √d_k) × V

Where:
- Q = Query (what I'm looking for)
- K = Key (what I have)
- V = Value (what I return)
- d_k = dimension of keys
```

**Transformer Architecture**:
```
┌─────────────────────────────────────────────────────┐
│                     Transformer                     │
│  ┌────────────────────┐  ┌────────────────────┐     │
│  │      Encoder       │  │      Decoder       │     │
│  │  ┌──────────────┐  │  │  ┌──────────────┐  │     │
│  │  │Multi-Head    │  │  │  │Masked Multi- │  │     │
│  │  │Attention     │  │──│─►│Head Attention│  │     │
│  │  └──────────────┘  │  │  └──────────────┘  │     │
│  │  ┌──────────────┐  │  │  ┌──────────────┐  │     │
│  │  │Feed Forward  │  │  │  │Cross-Attention│ │     │
│  │  └──────────────┘  │  │  └──────────────┘  │     │
│  │         × N        │  │  ┌──────────────┐  │     │
│  └────────────────────┘  │  │Feed Forward  │  │     │
│                          │  └──────────────┘  │     │
│                          │         × N        │     │
│                          └────────────────────┘     │
└─────────────────────────────────────────────────────┘
```

---

### BERT (Bidirectional Encoder Representations)

**Key Innovations**:
- Bidirectional context (reads left and right)
- Pre-training tasks: Masked Language Model + Next Sentence Prediction
- Transfer learning for NLP

```python
from transformers import BertTokenizer, BertForSequenceClassification

tokenizer = BertTokenizer.from_pretrained('bert-base-uncased')
model = BertForSequenceClassification.from_pretrained('bert-base-uncased', num_labels=2)

inputs = tokenizer("Hello, how are you?", return_tensors="pt")
outputs = model(**inputs)
```

---

## Section 13 — Large Language Models (LLMs)

### LLM Architecture Overview

| Model | Parameters | Training Data | Key Feature |
|:---|:---|:---|:---|
| **GPT-3** | 175B | 570GB text | Few-shot learning |
| **GPT-4** | ~1.7T | Multimodal | Reasoning, vision |
| **LLaMA** | 7B-70B | Open weights | Efficient, open-source |
| **Claude** | ~175B | Constitutional AI | Safety-focused |

---

### Prompt Engineering

**Techniques**:
| Technique | Description | Example |
|:---|:---|:---|
| **Zero-shot** | No examples | "Classify sentiment: [text]" |
| **Few-shot** | Give examples | "Positive: great! Negative: terrible! Classify: [text]" |
| **Chain-of-Thought** | Step-by-step reasoning | "Let's think step by step..." |
| **Role prompting** | Assign persona | "You are an expert data scientist..." |

**Best Practices**:
1. Be specific and clear
2. Provide context and examples
3. Break complex tasks into steps
4. Specify output format
5. Use delimiters for structure

---

### Fine-Tuning Strategies

| Method | Description | Resources |
|:---|:---|:---|
| **Full Fine-tuning** | Update all parameters | Very expensive |
| **LoRA** | Low-rank adaptation, small trainable matrices | Efficient |
| **QLoRA** | Quantized LoRA | Very efficient |
| **Prompt Tuning** | Train soft prompts | Lightweight |
| **Instruction Tuning** | Train on instruction-response pairs | General purpose |

```python
from peft import LoraConfig, get_peft_model

config = LoraConfig(
    r=8,
    lora_alpha=32,
    target_modules=["q_proj", "v_proj"],
    lora_dropout=0.1,
)
model = get_peft_model(base_model, config)
```

---

### RAG (Retrieval Augmented Generation)

```
┌───────────────────────────────────────────────────────────┐
│                      RAG Pipeline                         │
│                                                           │
│  Query ──→ [Embedding] ──→ [Vector Search] ──→ Top K      │
│                                  ↓                        │
│  [LLM] ◄── [Prompt + Context] ◄──┘                        │
│    ↓                                                      │
│  Answer                                                   │
└───────────────────────────────────────────────────────────┘
```

**Components**:
1. **Document Store**: Vector database (Pinecone, Weaviate, ChromaDB)
2. **Embeddings**: Convert text to vectors
3. **Retriever**: Find relevant documents
4. **Generator**: LLM generates answer with context

---

## Section 14 — Computer Vision

### GANs (Generative Adversarial Networks)

**Concept**: Two neural networks competing against each other in a zero-sum game.
- **Generator (G)**: Creates fake data (images) from random noise. Tries to fool the discriminator.
- **Discriminator (D)**: Evaluates data as real (from dataset) or fake (from generator). Tries to catch the generator.

**Loss Function (Minimax Game)**:
`min_G max_D V(D, G) = E[log D(x)] + E[log(1 - D(G(z)))]`

**Challenges**:
- **Mode Collapse**: Generator produces limited variety of samples.
- **Vanishing Gradients**: If Discriminator is too good, Generator stops learning.

---

### Vision Transformers (ViT)

**Concept**: Applying the Transformer architecture (Self-Attention) directly to images, replacing CNNs.

**How it works**:
1. **Patchification**: Break image into fixed-size patches (e.g., 16x16).
2. **Linear Projection**: Flatten patches and map to vector embeddings.
3. **Positional Embeddings**: Add position info since Transformers have no inherent sense of space.
4. **Transformer Encoder**: Standard Multi-Head Self-Attention layers.
5. **Class Token**: Special token used for final classification output.

**ViT vs CNN**:
- **Cons**: Needs massive datasets (JFT-300M) to outperform CNNs (lacks inductive bias like translation invariance).
- **Pros**: Global receptive field from layer 1 (sees whole image at once).

---

### Object Detection

| Model | Description | Speed | Accuracy |
|:---|:---|:---|:---|
| **R-CNN** | Region proposals + CNN | Slow | High |
| **Fast R-CNN** | Shared computation | Medium | High |
| **Faster R-CNN** | Region Proposal Network | Fast | High |
| **YOLO** | Single-shot detection | Very Fast | Good |
| **SSD** | Multi-scale detection | Fast | Good |

---

### Image Segmentation

| Type | Description | Output |
|:---|:---|:---|
| **Semantic** | Classify each pixel | Class per pixel |
| **Instance** | Distinguish instances | Instance + class per pixel |
| **Panoptic** | Semantic + Instance | Complete scene understanding |

**Models**: U-Net, Mask R-CNN, DeepLab

---

## Section 15 — Model Training & Optimization

### Training Loop (PyTorch)

```python
import torch
import torch.nn as nn
import torch.optim as optim

model = MyModel()
criterion = nn.CrossEntropyLoss()
optimizer = optim.Adam(model.parameters(), lr=0.001)

for epoch in range(num_epochs):
    model.train()
    for batch_x, batch_y in train_loader:
        # Forward pass
        outputs = model(batch_x)
        loss = criterion(outputs, batch_y)
        
        # Backward pass
        optimizer.zero_grad()
        loss.backward()
        optimizer.step()
    
    # Validation
    model.eval()
    with torch.no_grad():
        val_loss = evaluate(model, val_loader)
    
    print(f"Epoch {epoch}: Train Loss={loss:.4f}, Val Loss={val_loss:.4f}")
```

---

### Learning Rate Scheduling

| Schedule | Description | Use Case |
|:---|:---|:---|
| **Step Decay** | Reduce by factor every N epochs | Simple approach |
| **Exponential** | Multiply by γ each epoch | Smooth decay |
| **Cosine Annealing** | Cosine curve from max to min | SOTA results |
| **One Cycle** | Warm up then cool down | Fast convergence |
| **ReduceOnPlateau** | Reduce when metric stalls | Adaptive |

```python
# Cosine Annealing
scheduler = torch.optim.lr_scheduler.CosineAnnealingLR(optimizer, T_max=100)

# ReduceOnPlateau
scheduler = torch.optim.lr_scheduler.ReduceLROnPlateau(optimizer, patience=5)
```

---

### Mixed Precision Training

```python
from torch.cuda.amp import autocast, GradScaler

scaler = GradScaler()

for batch_x, batch_y in train_loader:
    optimizer.zero_grad()
    
    with autocast():  # FP16 forward pass
        outputs = model(batch_x)
        loss = criterion(outputs, batch_y)
    
    scaler.scale(loss).backward()
    scaler.step(optimizer)
    scaler.update()
```

**Benefits**:
- 2x faster training
- 50% less memory
- Minimal accuracy loss

---

## Section 16 — MLOps & Model Deployment

### ML Pipeline Architecture

```
┌──────────────────────────────────────────────────────────────────┐
│                       ML Pipeline                                │
│                                                                  │
│  Data ──→ Feature ──→ Training ──→ Evaluation ──→ Deployment     │
│  Ingestion  Store      Pipeline                    (Model        │
│                                                    Serving)      │
│     ↓         ↓           ↓            ↓             ↓           │
│  [Airflow] [Feast]  [MLflow/W&B] [Great Exp.]  [Kubernetes]      │
│                                                                  │
│                    ↓                                             │
│              Monitoring (Drift, Performance)                     │
└──────────────────────────────────────────────────────────────────┘
```

---

### Experiment Tracking

```python
import mlflow

mlflow.set_experiment("my-experiment")

with mlflow.start_run():
    # Log parameters
    mlflow.log_param("learning_rate", 0.001)
    mlflow.log_param("batch_size", 32)
    
    # Train model
    model = train(...)
    
    # Log metrics
    mlflow.log_metric("accuracy", 0.95)
    mlflow.log_metric("f1_score", 0.92)
    
    # Log model
    mlflow.sklearn.log_model(model, "model")
```

---

### Model Serving Options

| Option | Pros | Cons | Use Case |
|:---|:---|:---|:---|
| **REST API (Flask/FastAPI)** | Simple | Limited scale | POC, low traffic |
| **TensorFlow Serving** | Optimized for TF | TF only | Production TF models |
| **TorchServe** | Optimized for PyTorch | PyTorch only | Production PyTorch |
| **Triton (NVIDIA)** | Multi-framework | Complex | High performance |
| **SageMaker** | Managed | Vendor lock-in | AWS environments |

---

### Model Monitoring

**Types of Drift**:
| Drift Type | What Changes | Detection |
|:---|:---|:---|
| **Data Drift** | Input feature distribution | Statistical tests (KS, Chi-square) |
| **Concept Drift** | Relationship X→Y | Performance degradation |
| **Label Drift** | Output distribution | Compare prediction distribution |

```python
from evidently import ColumnDriftReport

report = ColumnDriftReport(columns=feature_columns)
report.run(reference_data=train_df, current_data=prod_df)
report.show()
```

---

## Section 17 — Interview Scenarios & Case Studies

### Scenario 1: Model Selection

**Question**: You need to predict customer churn with 100K rows. Which algorithm?

**Approach**:
1. Start with **Logistic Regression** (baseline, interpretable)
2. Try **Random Forest** (handles non-linearity)
3. Try **XGBoost** (typically best performance)
4. Consider imbalanced class handling (class weights, SMOTE)
5. Evaluate with **AUC-ROC** and **Precision-Recall** (not accuracy!)

---

### Scenario 2: Feature Engineering

**Question**: You have user transaction data. What features would you create?

**Answer**:
- **Aggregations**: Total spend, avg order value, order count
- **Recency**: Days since last order
- **Frequency**: Orders per week/month
- **Time-based**: Weekend vs weekday orders
- **Behavioral**: Category preferences, time-of-day patterns
- **Derived**: Customer lifetime value, growth rate

---

### Scenario 3: Model Performance Drop

**Question**: Model accuracy dropped 10% in production. What do you do?

**Systematic Approach**:
1. **Verify the issue**: Check metrics pipeline, not a bug?
2. **Check data quality**: Missing values, schema changes?
3. **Check data drift**: Compare production vs training distributions
4. **Check upstream changes**: Did data source change?
5. **Retrain on recent data**: Capture new patterns
6. **Consider concept drift**: Relationship between features and target changed

---

### Scenario 4: Bias Detection

**Question**: Your hiring model shows gender bias. How do you fix it?

**Approach**:
1. **Audit**: Check performance across demographic groups
2. **Remove sensitive features**: Gender, but also proxies (name, college)
3. **Balanced training**: Equal representation
4. **Regularization**: Adversarial debiasing
5. **Post-processing**: Equalize decision threshold across groups
6. **Human oversight**: Don't fully automate high-stakes decisions

---

### Scenario 5: Scaling ML

**Question**: Model inference takes 500ms but needs to be 50ms. How?

**Optimization Techniques**:
1. **Model compression**: Quantization (FP32 → INT8)
2. **Distillation**: Train smaller student model
3. **Pruning**: Remove unimportant weights
4. **Batching**: Process multiple requests together
5. **Caching**: Cache frequent predictions
6. **Hardware**: GPU/TPU for inference
7. **Model selection**: Use simpler model if accuracy acceptable

---

## Quick Reference

### Common Python Libraries
```python
# Data Manipulation
import pandas as pd
import numpy as np

# Visualization
import matplotlib.pyplot as plt
import seaborn as sns

# ML
from sklearn.model_selection import train_test_split, cross_val_score
from sklearn.preprocessing import StandardScaler, LabelEncoder
from sklearn.metrics import accuracy_score, f1_score, roc_auc_score

# Deep Learning
import torch
import torch.nn as nn
import tensorflow as tf

# NLP
from transformers import AutoTokenizer, AutoModel

# Experiment Tracking
import mlflow
import wandb
```

### Model Evaluation Cheat Sheet
| Task | Primary Metrics | Secondary Metrics |
|:---|:---|:---|
| **Binary Classification** | AUC-ROC, F1 | Precision, Recall, Accuracy |
| **Multi-class Classification** | Macro F1, Accuracy | Confusion Matrix |
| **Regression** | RMSE, MAE | R², MAPE |
| **Ranking** | NDCG, MAP | MRR |
| **Object Detection** | mAP | IoU |

---

## Section 18 — ML/AI Tools & Frameworks

### Data Processing & Analysis Tools

| Tool | Category | Use Case |
|:---|:---|:---|
| **Pandas** | Data manipulation | Tabular data operations, EDA |
| **NumPy** | Numerical computing | Array operations, linear algebra |
| **Polars** | Fast DataFrame | Large datasets, faster than Pandas |
| **Dask** | Parallel computing | Out-of-memory datasets |
| **Spark (PySpark)** | Distributed computing | Big data processing |
| **Vaex** | Out-of-core DataFrames | Billion-row datasets |

### ML Frameworks

| Framework | Strengths | Best For |
|:---|:---|:---|
| **Scikit-learn** | Simple API, classical ML | Tabular data, prototyping |
| **XGBoost** | Gradient boosting | Structured data, competitions |
| **LightGBM** | Fast, memory efficient | Large datasets |
| **CatBoost** | Categorical features | Minimal preprocessing |

### Deep Learning Frameworks

| Framework | Company | Strengths |
|:---|:---|:---|
| **PyTorch** | Meta | Research, dynamic graphs, debugging |
| **TensorFlow** | Google | Production, TF Serving, mobile |
| **Keras** | Google | High-level API, rapid prototyping |
| **JAX** | Google | Research, auto-diff, XLA |
| **MXNet** | Apache | Distributed training |

### NLP Libraries

| Library | Use Case |
|:---|:---|
| **Hugging Face Transformers** | Pre-trained models (BERT, GPT, LLaMA) |
| **spaCy** | Production NLP pipelines |
| **NLTK** | Educational, basic NLP |
| **Gensim** | Topic modeling, Word2Vec |
| **LangChain** | LLM applications, agents |
| **LlamaIndex** | RAG applications |

### Computer Vision Libraries

| Library | Use Case |
|:---|:---|
| **OpenCV** | Image processing, computer vision |
| **Pillow** | Image manipulation |
| **torchvision** | PyTorch vision models |
| **Detectron2** | Object detection, segmentation |
| **YOLO (Ultralytics)** | Real-time object detection |
| **Albumentations** | Image augmentation |

### MLOps & Experiment Tracking

| Tool | Category | Features |
|:---|:---|:---|
| **MLflow** | Experiment tracking | Logging, model registry, deployment |
| **Weights & Biases** | Experiment tracking | Visualizations, hyperparameter sweeps |
| **DVC** | Data versioning | Git for data, pipeline management |
| **Kubeflow** | ML pipelines | Kubernetes-native ML workflows |
| **Airflow** | Workflow orchestration | DAG-based scheduling |
| **Prefect** | Workflow orchestration | Modern, Python-native |
| **BentoML** | Model serving | Packaging, deployment |
| **Seldon** | Model serving | Kubernetes model deployment |

### Vector Databases (for RAG/Embeddings)

| Database | Features |
|:---|:---|
| **Pinecone** | Managed, scalable, fast |
| **Weaviate** | Open-source, hybrid search |
| **ChromaDB** | Lightweight, embedded |
| **Milvus** | Open-source, distributed |
| **Qdrant** | Rust-based, filtering |
| **FAISS** | Facebook, similarity search |

### AutoML Tools

| Tool | Features |
|:---|:---|
| **Auto-sklearn** | Automated scikit-learn |
| **H2O AutoML** | Enterprise, distributed |
| **Google AutoML** | Cloud-based, no code |
| **TPOT** | Genetic programming |
| **Optuna** | Hyperparameter optimization |
| **Ray Tune** | Distributed hyperparameter tuning |

### Cloud ML Platforms

| Platform | Services |
|:---|:---|
| **AWS SageMaker** | Training, hosting, Studio, JumpStart |
| **Google Vertex AI** | AutoML, custom training, pipelines |
| **Azure ML** | Designer, pipelines, endpoints |
| **Databricks** | MLflow, Unity Catalog, Feature Store |

---

## Section 19 — 50+ Interview Questions with Answers

### Statistics & Probability Questions

**Q1: What is the Central Limit Theorem?**
> The CLT states that the sampling distribution of the mean approaches a normal distribution as sample size increases, regardless of the population distribution (if mean and variance exist).

**Q2: Explain p-value in simple terms.**
> P-value is the probability of observing results as extreme as the current results, assuming the null hypothesis is true. If p < 0.05, we reject the null hypothesis.

**Q3: What's the difference between Type I and Type II errors?**
> - Type I (False Positive): Rejecting true null hypothesis (α)
> - Type II (False Negative): Failing to reject false null hypothesis (β)
> - Example: Type I = Convicting innocent person; Type II = Freeing guilty person

**Q4: How do you handle multiple hypothesis testing?**
> Use Bonferroni correction (α/n) or False Discovery Rate (FDR) control. Running many tests increases false positives.

**Q5: When would you use Bayesian vs Frequentist approach?**
> - **Bayesian**: Prior knowledge available, uncertainty quantification needed
> - **Frequentist**: Large sample, objective analysis, no prior information

---

### Machine Learning Questions

**Q6: Explain the bias-variance tradeoff.**
> - **Bias**: Error from oversimplified assumptions (underfitting)
> - **Variance**: Error from sensitivity to training data (overfitting)
> - **Goal**: Find the sweet spot minimizing total error

**Q7: Why do we split data into train/validation/test?**
> - **Train**: Fit model parameters
> - **Validation**: Tune hyperparameters, prevent overfitting
> - **Test**: Final unbiased evaluation (never touch during development)

**Q8: What is regularization and why is it used?**
> Regularization adds penalty to loss function to prevent overfitting:
> - L1 (Lasso): Adds |weights|, produces sparse models
> - L2 (Ridge): Adds weights², shrinks weights toward zero

**Q9: Explain the difference between bagging and boosting.**
> - **Bagging**: Train models in parallel on bootstrapped samples, reduce variance
> - **Boosting**: Train models sequentially, each correcting previous errors, reduce bias

**Q10: How does Random Forest prevent overfitting?**
> 1. Bagging: Each tree sees random subset of data
> 2. Feature randomness: Each split considers random subset of features
> 3. Averaging: Final prediction averages many trees

**Q11: What makes XGBoost better than traditional gradient boosting?**
> - Regularization (L1/L2) in objective function
> - Handles missing values automatically
> - Parallel tree construction
> - Pruning (max_depth first, then prune)
> - Built-in cross-validation

**Q12: How do you handle categorical features with high cardinality?**
> - Target encoding (mean of target per category)
> - Frequency encoding
> - Hash encoding
> - Entity embeddings (for deep learning)
> - Leave-one-out encoding

**Q13: What is data leakage and how do you prevent it?**
> Data leakage occurs when training data contains information about the target that wouldn't be available at prediction time.
> **Prevention**:
> - Split data before any preprocessing
> - Use pipelines that fit only on training data
> - Check feature importance for suspiciously important features

**Q14: Explain k-fold cross-validation.**
> Split data into k folds, train on k-1 folds, validate on 1 fold, repeat k times, average results. Provides more robust performance estimate than single train/test split.

**Q15: When would you use precision vs recall?**
> - **Precision**: Cost of false positive is high (spam filtering, search rankings)
> - **Recall**: Cost of false negative is high (disease detection, fraud)

---

### Deep Learning Questions

**Q16: Why do we use activation functions?**
> Without activation functions, neural networks are just linear transformations. Activation functions add non-linearity, allowing networks to learn complex patterns.

**Q17: Why is ReLU preferred over sigmoid?**
> - No vanishing gradient (for positive values)
> - Computationally efficient (just max(0,x))
> - Sparse activation (some neurons = 0)
> - Prevents saturation

**Q18: What is the vanishing gradient problem?**
> In deep networks, gradients become very small in early layers during backpropagation (especially with sigmoid/tanh), making learning slow. Solutions: ReLU, residual connections, batch normalization.

**Q19: Explain batch normalization.**
> Normalizes layer inputs to have zero mean and unit variance. Benefits:
> - Faster training
> - Higher learning rates possible
> - Reduces internal covariate shift
> - Slight regularization effect

**Q20: What is dropout and how does it work?**
> Randomly sets neurons to zero during training with probability p. Forces network to learn redundant representations, acting as regularization. At inference, all neurons are active (scaled by 1-p).

**Q21: Explain the difference between parameters and hyperparameters.**
> - **Parameters**: Learned during training (weights, biases)
> - **Hyperparameters**: Set before training (learning rate, batch size, architecture)

**Q22: Why use mini-batch gradient descent over full batch?**
> - Memory efficient (doesn't need all data in memory)
> - Faster updates (more iterations per epoch)
> - Noise helps escape local minima
> - Parallelizable on GPUs

**Q23: What is transfer learning?**
> Using a pre-trained model (trained on large dataset) as starting point for new task. Freeze early layers (general features), fine-tune later layers (task-specific).

**Q24: Explain the attention mechanism.**
> Attention allows model to focus on relevant parts of input when producing output. Computes weighted sum of values where weights are based on similarity between query and keys.

---

### NLP Questions

**Q25: What is tokenization?**
> Breaking text into smaller units (tokens). Types:
> - Word-level: "Hello world" → ["Hello", "world"]
> - Subword (BPE): "unhappiness" → ["un", "happiness"]
> - Character-level: "cat" → ["c", "a", "t"]

**Q26: Explain Word2Vec.**
> Neural network that learns word embeddings from context:
> - **Skip-gram**: Predict context from word
> - **CBOW**: Predict word from context
> Captures semantic relationships: king - man + woman ≈ queen

**Q27: What is the difference between BERT and GPT?**
> - **BERT**: Bidirectional encoder, masked language modeling, good for understanding
> - **GPT**: Autoregressive decoder, next token prediction, good for generation

**Q28: Explain self-attention in transformers.**
> Each token attends to all other tokens in sequence, computing weighted representation based on relevance. Enables capturing long-range dependencies without recurrence.

**Q29: What is positional encoding?**
> Since transformers process all tokens in parallel (no inherent position), positional encodings add position information. Can be sinusoidal (fixed) or learned.

**Q30: What is fine-tuning vs prompting?**
> - **Fine-tuning**: Update model weights on task-specific data
> - **Prompting**: Use natural language instructions without changing weights
> - **Few-shot prompting**: Include examples in prompt

---

### Computer Vision Questions

**Q31: Why use convolutions instead of fully connected layers for images?**
> - **Parameter sharing**: Same kernel across image (fewer parameters)
> - **Translation invariance**: Detect features anywhere in image
> - **Local connectivity**: Capture spatial patterns

**Q32: What is max pooling?**
> Downsampling by taking maximum value in each region. Reduces spatial dimensions, provides translation invariance, reduces computation.

**Q33: Explain skip connections in ResNet.**
> Add input of block to its output (x + F(x)). Allows gradient to flow directly, enables training very deep networks, helps preserve information.

**Q34: What is data augmentation?**
> Creating variations of training images (rotation, flip, crop, color jitter) to increase dataset size and improve generalization.

**Q35: Explain the difference between object detection and segmentation.**
> - **Detection**: Bounding boxes around objects
> - **Semantic segmentation**: Pixel-wise class labels
> - **Instance segmentation**: Separate each object instance

---

### LLM Questions

**Q36: What is temperature in LLM sampling?**
> Controls randomness of output. Lower temperature (0.1) = more deterministic, higher (1.0+) = more creative/random.

**Q37: Explain RAG (Retrieval Augmented Generation).**
> Combine LLM with external knowledge base:
> 1. Embed query and documents
> 2. Retrieve relevant documents
> 3. Add to context and generate response
> Reduces hallucinations, keeps knowledge current.

**Q38: What is LoRA fine-tuning?**
> Low-Rank Adaptation: Instead of updating all weights, add small trainable matrices to frozen model. Much more efficient than full fine-tuning.

**Q39: What are hallucinations in LLMs?**
> LLMs generating factually incorrect or nonsensical information that sounds plausible. Mitigation: RAG, fact-checking, temperature control, grounding.

**Q40: Explain context window limitations.**
> LLMs can only process limited tokens at once (4K-128K+). Long documents need chunking, summarization, or hierarchical approaches.

---

### MLOps Questions

**Q41: What is model drift?**
> - **Data drift**: Input distribution changes over time
> - **Concept drift**: Relationship between features and target changes
> Detection: Monitor input distributions, model performance

**Q42: How do you version ML models?**
> - Model registry (MLflow, W&B)
> - Associate with code version (git), data version (DVC), hyperparameters
> - Track lineage: data → features → model → predictions

**Q43: Explain A/B testing for ML models.**
> Split traffic between old and new model, measure business metrics, ensure statistical significance before full rollout.

**Q44: What is feature store?**
> Centralized repository for features:
> - Consistent features between training and serving
> - Feature reuse across teams
> - Point-in-time correctness
> Examples: Feast, Tecton, Databricks Feature Store

**Q45: How do you monitor models in production?**
> - Prediction latency
> - Error rates
> - Input data distributions
> - Prediction distributions
> - Business metrics (click-through, conversion)

---

### System Design Questions

**Q46: Design a recommendation system.**
> **Components**:
> 1. Candidate generation: Collaborative filtering, content-based
> 2. Ranking: ML model to score candidates
> 3. Re-ranking: Business rules, diversity
> 4. Serving: Low-latency, caching
> **Metrics**: CTR, engagement, revenue

**Q47: Design a fraud detection system.**
> - **Real-time**: Rule engine + ML model for immediate decisions
> - **Batch**: Deep analysis, pattern detection
> - **Features**: Transaction velocity, device fingerprint, behavioral patterns
> - **Challenges**: Highly imbalanced, adversarial, latency requirements

**Q48: Design a search ranking system.**
> 1. Query understanding (intent, entities)
> 2. Candidate retrieval (inverted index, ANN)
> 3. Ranking (Learning to Rank: pointwise, pairwise, listwise)
> 4. Re-ranking (personalization, freshness)

**Q49: How would you deploy an ML model with 10ms latency requirement?**
> - Model optimization (quantization, pruning, distillation)
> - Efficient serving (TensorRT, ONNX)
> - Caching frequent predictions
> - Edge deployment
> - Batching requests

**Q50: Design a real-time pricing system.**
> - Feature computation: demand, supply, time features
> - Model: gradient boosting or neural network
> - Online learning for adaptation
> - A/B testing for price optimization
> - Guard rails for minimum/maximum prices

---

## Section 20 — Scenario-Based Questions

### Scenario 1: Low Model Performance

**Situation**: Your model accuracy is only 65% on test set.

**Systematic Debugging**:
1. **Check data quality**: Missing values, outliers, labeling errors
2. **Check for data leakage**: Is test performance much lower than training?
3. **Try baseline**: Is 65% actually good for this problem?
4. **Feature engineering**: Are features informative?
5. **Model complexity**: Underfitting (try complex model) or overfitting?
6. **Hyperparameter tuning**: Use GridSearch/Optuna
7. **Ensemble methods**: Combine multiple models

---

### Scenario 2: Model Works Locally, Fails in Production

**Common Causes**:
1. **Training-serving skew**: Different preprocessing
2. **Data distribution shift**: Production data different from training
3. **Feature computation**: Same features computed differently
4. **Missing values**: Handled differently
5. **Version mismatch**: Library versions

**Solutions**:
- Use consistent pipelines (sklearn Pipeline, TFX)
- Feature stores for consistency
- Shadow deployment to compare
- Monitor input distributions

---

### Scenario 3: Real-Time vs Batch Prediction

**When to use Batch**:
- Predictions not time-sensitive
- Large volume, periodic updates
- Complex models acceptable
- Example: Nightly churn predictions

**When to use Real-Time**:
- Immediate response needed
- Per-request predictions
- Latency constraints
- Example: Fraud detection, recommendations

**Hybrid Approach**:
- Precompute what you can (batch)
- Real-time for dynamic features
- Cache frequently requested predictions

---

### Scenario 4: Imbalanced Classification (1% Positive)

**Approaches in order**:
1. **Baseline with class weights**: `class_weight='balanced'`
2. **Evaluation metrics**: Use AUC-ROC, Precision-Recall AUC, not accuracy
3. **SMOTE**: Synthetic oversampling
4. **Threshold adjustment**: Lower threshold to catch more positives
5. **Cost-sensitive learning**: Higher penalty for missing positives
6. **Anomaly detection**: Treat as anomaly detection problem
7. **Ensemble with sampling**: BalancedRandomForest

---

### Scenario 5: Model Degradation Over Time

**Detection**:
- Monitor prediction distributions
- Track performance on labeled samples
- Compare with baseline model

**Response**:
1. Identify cause (data drift vs concept drift)
2. Collect new labeled data
3. Retrain on recent data
4. Consider online learning
5. Implement automated retraining pipeline

---

### Scenario 6: Explaining Black-Box Model to Business

**Techniques**:
- **SHAP values**: Feature contribution per prediction
- **LIME**: Local interpretable explanations
- **Feature importance**: Global understanding
- **Partial dependence plots**: Feature effect visualization
- **Counterfactual explanations**: "If X were different, prediction would be..."

**Communication Tips**:
- Focus on business implications
- Use concrete examples
- Visualize whenever possible
- Highlight actionable insights

---

### Scenario 7: Cold Start Problem in Recommendations

**For New Users**:
- Ask preferences during onboarding
- Use demographic-based recommendations
- Popular/trending items
- Explore/exploit strategies

**For New Items**:
- Content-based features
- Use metadata similarities
- Promote to subset for feedback
- Time-decay for older items

---

### Scenario 8: High Cardinality Categorical Feature

**Feature**: City with 50,000 unique values

**Solutions**:
1. **Target encoding**: Mean target per city (with regularization)
2. **Frequency encoding**: Count of occurrences
3. **Grouping**: Map to larger regions, clusters
4. **Hash encoding**: Hash to fixed number of bins
5. **Entity embeddings**: Learn representations in neural network
6. **Leave out encoding**: Leave-one-out target mean

---

### Scenario 9: Time Series Forecasting with Multiple Seasonalities

**Approach**:
1. **Decomposition**: Trend + seasonal + residual
2. **Model selection**:
   - ARIMA/SARIMA for single seasonality
   - Prophet for multiple seasonalities
   - LSTM/Transformer for complex patterns
3. **Feature engineering**:
   - Lag features
   - Rolling statistics
   - Fourier terms for seasonality
4. **Validation**: Time-based split (no shuffle!)

---

### Scenario 10: Deploying Large Language Model

**Challenges**:
- Model size (7B-70B parameters)
- Latency requirements
- Cost per inference

**Solutions**:
1. **Quantization**: FP16 → INT8 → INT4
2. **Model distillation**: Train smaller student model
3. **Caching**: Cache common responses
4. **Batching**: Process multiple requests together
5. **Specialized hardware**: GPUs, TPUs
6. **API services**: Use OpenAI, Anthropic APIs

---

## Section 21 — Key Terminologies & Glossary

### A-D

| Term | Definition |
|:---|:---|
| **Activation Function** | Non-linear function applied after linear transformation (ReLU, sigmoid) |
| **Attention** | Mechanism allowing model to focus on relevant parts of input |
| **Autoencoder** | Neural network that learns compressed representation then reconstructs |
| **Backpropagation** | Algorithm to compute gradients by chain rule, flowing backward |
| **Batch Normalization** | Normalizing layer inputs during training for stability |
| **Beam Search** | Decoding strategy keeping top-k candidates at each step |
| **BERT** | Bidirectional Encoder Representations from Transformers |
| **Bias (ML)** | Systematic error from assumptions; also prejudice in training data |
| **Boosting** | Ensemble method training models sequentially on errors |
| **Categorical Variable** | Variable with discrete categories (color, country) |
| **CNN** | Convolutional Neural Network for spatial data |
| **Cosine Similarity** | Similarity measure based on angle between vectors |
| **Cross-Entropy** | Loss function for classification (negative log likelihood) |
| **Curse of Dimensionality** | Problems arising in high-dimensional spaces (sparse data) |
| **Data Augmentation** | Creating variations of training data to increase dataset size |
| **Decoder** | Part of model that generates output from representation |
| **Dimensionality Reduction** | Reducing number of features while preserving information |
| **Dropout** | Regularization by randomly zeroing neurons during training |

### E-L

| Term | Definition |
|:---|:---|
| **Embedding** | Dense vector representation of discrete objects (words, users) |
| **Encoder** | Part of model that creates representation from input |
| **Ensemble** | Combining multiple models for better performance |
| **Epoch** | One complete pass through training data |
| **Feature Engineering** | Creating informative features from raw data |
| **Feature Importance** | Measure of how much each feature contributes to prediction |
| **Fine-tuning** | Adjusting pre-trained model weights on new task |
| **F1-Score** | Harmonic mean of precision and recall |
| **GAN** | Generative Adversarial Network (generator vs discriminator) |
| **Gradient** | Vector of partial derivatives, direction of steepest ascent |
| **Gradient Descent** | Optimization by iteratively moving against gradient |
| **Ground Truth** | Actual correct labels in supervised learning |
| **Hallucination** | LLM generating false but plausible-sounding information |
| **Hyperparameter** | Configuration set before training (learning rate, layers) |
| **Imputation** | Filling in missing values |
| **Inference** | Using trained model to make predictions |
| **Latent Space** | Hidden representation learned by model |
| **Learning Rate** | Step size in gradient descent |
| **LSTM** | Long Short-Term Memory, RNN variant for long sequences |
| **Loss Function** | Objective function measuring prediction error |

### M-R

| Term | Definition |
|:---|:---|
| **MAE** | Mean Absolute Error |
| **Mini-batch** | Subset of training data used per gradient update |
| **MSE** | Mean Squared Error |
| **Multicollinearity** | High correlation between predictor variables |
| **NER** | Named Entity Recognition (extracting entities from text) |
| **Neural Network** | Computing system inspired by biological neural networks |
| **NLP** | Natural Language Processing |
| **One-hot Encoding** | Binary vector representation of categories |
| **Overfitting** | Model memorizes training data, poor generalization |
| **Parameter** | Value learned during training (weights, biases) |
| **Perceptron** | Simplest neural network unit |
| **Perplexity** | Measure of how well model predicts text (lower is better) |
| **Pipeline** | Sequence of data processing steps |
| **Pooling** | Downsampling operation in CNNs |
| **Precision** | True positives / (True positives + False positives) |
| **Pre-training** | Initial training on large dataset before fine-tuning |
| **Prompt Engineering** | Crafting effective inputs for LLMs |
| **RAG** | Retrieval Augmented Generation |
| **Recall** | True positives / (True positives + False negatives) |
| **Regularization** | Techniques to prevent overfitting (L1, L2, dropout) |
| **ReLU** | Rectified Linear Unit: max(0, x) |
| **RMSE** | Root Mean Squared Error |
| **RNN** | Recurrent Neural Network for sequential data |
| **ROC Curve** | Receiver Operating Characteristic (TPR vs FPR) |

### S-Z

| Term | Definition |
|:---|:---|
| **Semantic Search** | Search based on meaning, not keywords |
| **Seq2Seq** | Sequence-to-sequence models (encoder-decoder) |
| **SHAP** | SHapley Additive exPlanations (model interpretability) |
| **Softmax** | Function converting scores to probabilities |
| **Stochastic** | Random, involving randomness |
| **Stop Words** | Common words filtered out (the, a, is) |
| **Stride** | Step size when sliding kernel in convolution |
| **Supervised Learning** | Learning from labeled data (input-output pairs) |
| **SVM** | Support Vector Machine |
| **Temperature** | Parameter controlling randomness in sampling |
| **TF-IDF** | Term Frequency-Inverse Document Frequency |
| **Tokenization** | Breaking text into tokens |
| **Transfer Learning** | Using pre-trained model for new task |
| **Transformer** | Architecture based on self-attention |
| **Underfitting** | Model too simple to capture patterns |
| **Unsupervised Learning** | Learning patterns without labels (clustering) |
| **Upsampling** | Increasing minority class samples |
| **Vanishing Gradient** | Gradients becoming too small in deep networks |
| **Vector Database** | Database optimized for similarity search on embeddings |
| **Word Embedding** | Dense vector representation of words |
| **Zero-shot Learning** | Making predictions without task-specific training |

---

## Section 22 — Mathematical Notations Cheat Sheet

| Notation | Meaning |
|:---|:---|
| x, y | Scalars |
| **x**, **y** | Vectors |
| **X** | Matrix |
| xᵢ | i-th element of vector |
| Xᵢⱼ | Element at row i, column j |
| X⊤ | Transpose of X |
| X⁻¹ | Inverse of X |
| ‖x‖ | Norm (magnitude) of vector |
| x · y | Dot product |
| ∇f | Gradient of function f |
| ∂f/∂x | Partial derivative |
| Σ | Summation |
| Π | Product |
| E[X] | Expected value |
| Var(X) | Variance |
| P(A\|B) | Conditional probability |
| argmax | Value that maximizes function |
| softmax | Probability distribution over classes |

---
