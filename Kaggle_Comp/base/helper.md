
# 🧠 **Structured AI Prompting System**

## 📘 Overview

This document defines a **structured prompting framework** designed to help maintain focus and composure during high-pressure tasks — such as Kaggle competitions, debugging, or coding under time constraints.

It prevents “panic prompting” and ensures every AI interaction has a clear **goal, context, constraint, and output**.

> 🎯 **Objective:**
> Stay calm, think precisely, and command the AI — not be controlled by it.

---

## ⚙️ **Prompt Template (Base Structure)**

### 🧩 **Prompt Format**

Use this 4-section format **every time you ask AI for code or strategy help.**


🎯 GOAL:
[Describe exactly what you want to achieve, not what you want to see.]

📍 CONTEXT:
[Explain the current situation — what variables, files, or stages exist.
Mention what you’ve already tried.]

⚙️ CONSTRAINTS:
[List what must NOT be changed or what must remain consistent.
Example: “Don’t rename variables” or “Keep same function structure.”]

🧾 EXPECTED OUTPUT:
[Explain what kind of result you expect — code, explanation, step-by-step plan, etc.]

---

### 🧠 **Example (Kaggle Modeling Stage)**

🎯 GOAL:
Improve model performance from 0.78 → 0.82 F1-score using tree-based ensemble.

📍 CONTEXT:
I already have `X_train`, `y_train`, `X_val`, `y_val` from the preprocessing pipeline.  
Models currently available: RandomForest, XGBoost, GradientBoosting.  
Evaluation metric = weighted F1-score.

⚙️ CONSTRAINTS:
Don’t modify the preprocessing code or feature_engineering() function.  
Model training time must stay under 10 minutes.  
Keep outputs compatible with evaluate_model().

🧾 EXPECTED OUTPUT:
Modular Python code that builds a StackingClassifier using the three base models.  
Include evaluation step and print weighted F1-score.


---

### 🧩 **Example (Debugging Under Pressure)**

🎯 GOAL:
Fix error “ValueError: could not convert string to float” that appears when predicting.

📍 CONTEXT:
I used a preprocessing pipeline with OneHotEncoder and trained a LinearRegression model.  
`X_train` works fine, but `X_test` prediction fails with that error.

⚙️ CONSTRAINTS:
Don’t rewrite the entire pipeline — only modify the test transformation part.  
Must keep the same model and variable names (`regressor`, `preprocessor`).

🧾 EXPECTED OUTPUT:
Short Python fix (1–2 lines) that correctly preprocesses `X_test` before prediction,  
and brief explanation why the error happened.

---

## 🧭 **Usage Flow (War-Time Prompt Discipline)**

| Step | Action                      | Purpose                                                   |
| ---- | --------------------------- | --------------------------------------------------------- |
| 1️⃣  | **Stop. Breathe.**          | Interrupt panic mode before typing random questions.      |
| 2️⃣  | **Write your GOAL.**        | Forces clarity — what are you *actually* trying to solve? |
| 3️⃣  | **Add CONTEXT.**            | Helps AI give relevant, not generic responses.            |
| 4️⃣  | **Set CONSTRAINTS.**        | Prevents the AI from breaking your notebook.              |
| 5️⃣  | **Define EXPECTED OUTPUT.** | Keeps result usable and directly actionable.              |

---

## 📋 **Common Prompt Patterns**

### 🧱 **1. Code Request**

For generating specific code blocks.


🎯 GOAL: Create preprocessing pipeline for mixed numeric and categorical data.
📍 CONTEXT: Dataset = df_train, target = 'price'.  
⚙️ CONSTRAINTS: Don’t rename variables or import unnecessary libraries.  
🧾 EXPECTED OUTPUT: Scikit-learn pipeline code using ColumnTransformer.


### 🧠 **2. Concept Understanding**

For asking theoretical or strategic help.

🎯 GOAL: Understand when to use log transform on target variable.
📍 CONTEXT: My model underfits (R² = 0.7) and target distribution is right-skewed.  
⚙️ CONSTRAINTS: Keep explanation short, intuitive, and use dataset-related examples.  
🧾 EXPECTED OUTPUT: Concise explanation + rule of thumb for applying log transform.


### ⚙️ **3. Error Fix**

For debugging AI-generated or competition code.

🎯 GOAL: Fix "shape mismatch" during ensemble stacking.
📍 CONTEXT: Using RandomForest, XGB, and LogisticRegression in StackingClassifier.  
⚙️ CONSTRAINTS: Don’t remove any base model. Keep same variable names.  
🧾 EXPECTED OUTPUT: Short fix + reason of error.


### 🧩 **4. Strategy / Reflection**

For when lo bingung ambil keputusan.


🎯 GOAL: Decide whether to drop high-cardinality feature `model_name`.
📍 CONTEXT: Feature has 3,000 unique values and increases training time.
⚙️ CONSTRAINTS: Assume this is a classification task.
🧾 EXPECTED OUTPUT: Logical reasoning + simple rule of thumb (keep or drop).

---

## 🧰 **Mini Prompts Library (Quick Copy-Paste)**

| Scenario               | Ready-to-Use Prompt                                                                                                             |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| ⚙️ Preprocessing       | “Generate modular code for preprocessing mixed data (num + cat) using sklearn pipelines. Don’t modify existing variable names.” |
| 🧩 Feature Engineering | “Suggest 3 new feature ideas based on EDA insights where target distribution differs across groups.”                            |
| 🧠 Model Tuning        | “Optimize RandomForest parameters to improve F1-score under 10 min runtime.”                                                    |
| 🚨 Error Debug         | “Explain and fix error `could not convert string to float` during prediction step, without changing model logic.”               |
| 📊 Evaluation          | “Add cross-validation scoring (weighted F1) to my current evaluate_model() function.”                                           |
| ⚔️ Strategy            | “Compare pros/cons of stacking vs soft-voting ensemble for multiclass classification.”                                          |

---

## 🧩 **Optional: Quick Prompt Template (for daily use)**

Keep this pinned on top of your notebook or Notion page:

🎯 GOAL:
📍 CONTEXT:
⚙️ CONSTRAINTS:
🧾 EXPECTED OUTPUT:

---

## 💡 **Best Practices**

1. **Never prompt emotionally.** Pause before typing — logic first, emotions later.
2. **Write the prompt in 2–4 lines max.** Clarity beats verbosity.
3. **Always include constraints.** This is what separates structured engineers from chaotic coders.
4. **Treat the AI as a junior assistant** — *you lead, it executes.*
5. **Save good prompts** — reuse them for future competitions (build your prompt bank).

---

## 🏁 Closing Note

> “In chaos, structure wins.
> In pressure, precision wins.
> In competition, clarity wins.”

This system isn’t about writing better prompts —
it’s about building the **mental algorithm** that keeps you calm, strategic, and in full command of your AI assistant.
