# CNN Performance Optimization with ResNet50 (CIFAR-10)

This project explores CNN performance improvement through a combination of **data-centric optimization**, **cost-sensitive learning**, and **model-level regularization** using a fine-tuned ResNet50 on CIFAR-10.

---

## 🚀 Overview
Rather than relying solely on architectural changes, this project systematically improves performance through three stages:

1. **Baseline model (no augmentation)**
2. **Data-centric optimization (augmentation + oversampling + class weights)**
3. **Model-level optimization (MLP head + regularization)**

The goal is to analyze how each strategy impacts both overall accuracy and class-specific performance.

---

## 🧠 Methodology

### 1. Model Architecture
- Backbone: **ResNet50 (ImageNet pre-trained)**
- Two-stage training:
  - Feature Extraction (freeze backbone)
  - Fine-tuning (unfreeze last layers)

---

### 2. Baseline Setup
- No augmentation (only resizing to 224×224)
- Balanced dataset (5,000 samples)
- No class weights, no label smoothing
- Purpose: establish a performance baseline

---

## 📊 Optimization Strategy

### 🔹 Stage 1: Data-Centric Optimization
Focused on improving the **underperforming 'cat' class**

#### Techniques:
- **Oversampling:** 500 → 1,000 samples
- **Data Augmentation:**
  - Random Horizontal Flip & Rotation
  - Random Resized Crop
  - Color Jitter
- **Class Weights:** 3.0× for 'cat'

👉 Goal: improve class-specific recall and robustness

---

### 🔹 Stage 2: Model & Regularization Optimization

#### Improvements:
- **MLP Classification Head**
  - BatchNorm1d
  - Dropout (0.25)
  - Hidden layer (512 units)

- **Label Smoothing (0.02)**
  - Reduces overconfidence
  - Improves generalization

---

## 📈 Results & Analysis

### Performance Summary
- Baseline Accuracy: **83.32%**
- After Data Optimization: **88.01%**
- Final Model: **86.46%**

### Key Observations

- **Cat Class Performance**
  - Improved from **69.3% → 86.1%**
  - Significant gain from data-centric strategies

- **Trade-off**
  - Strong class weighting + MLP head led to **over-focus on 'cat'**
  - Slight drop in overall accuracy in final stage

---

## 💡 Key Insights

- Data-centric approaches (augmentation + oversampling) have **the largest impact**
- Class weights significantly affect model behavior
- Increasing model capacity can amplify bias toward weighted classes
- Label smoothing helps generalization but may reduce peak accuracy

---

## 🛠️ Tech Stack
- Python
- PyTorch
- Jupyter Notebook

---

## 📂 File
- `resnet50_finetuning_cifar10.ipynb`

---

## 🔮 Conclusion

This project demonstrates that:

- **Data optimization is often more impactful than architectural changes**
- There is a **trade-off between class-specific performance and overall accuracy**
- The best model depends on the deployment objective:
  - Maximize target class → Final Model
  - Balanced performance → Data-optimized model (Stage 2)

---

## 👩‍💻 Author
Jinhee Kim
