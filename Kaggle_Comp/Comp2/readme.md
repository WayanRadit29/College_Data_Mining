# 🧠 **Kaggle Competition Post-Mortem – AUC Classification Challenge**

## ⚙️ **Problem Summary**

| Issue                                   | Root Cause                                      | Consequence                                       |
| --------------------------------------- | ----------------------------------------------- | ------------------------------------------------- |
| **1. Model Overfit**                    | Tidak ada regularisasi + validasi kurang stabil | Score AUC tinggi di training tapi turun di test   |
| **2. Konfigurasi sulit diubah**         | Notebook tidak modular (banyak kode manual)     | Sulit eksplor ide baru saat waktu menipis         |
| **3. Running lambat (CPU Kaggle)**      | Model berat + one-hot besar + CV berlebihan     | Waktu habis sebelum dapat eksperimen optimal      |
| **4. Metric AUC belum familiar**        | Baru belajar sebelum lomba                      | Fokus salah (akurasi, bukan probabilitas ranking) |
| **5. Pemahaman dataset belum dalam**    | EDA terlalu luas, tidak fokus ke sinyal kuat    | Gagal spotting fitur paling prediktif             |
| **6. Ketergantungan AI Prompting**      | Tanpa struktur prompting system                 | Output AI sering tidak sinkron antar cell         |
| **7. Submission error (predict_proba)** | Tidak baca format submission                    | Nilai leaderboard tidak valid meski AUC tinggi    |

---

## 💡 **Key Insights**

1. **AUC menilai kemampuan model membedakan peringkat probabilitas antar kelas**, bukan prediksi keras (0/1).
2. **Probabilitas yang halus dan terkalibrasi** jauh lebih penting daripada “prediksi benar”.
3. **Feature engineering sederhana (flags, ratio, log transform)** sering memberi lonjakan besar ke AUC.
4. **CV disiplin + calibration + soft blending** adalah *meta-combo* paling Pareto untuk kompetisi berbasis AUC.
5. **Prompting chaos = eksekusi chaos.** Struktur prompting wajib dijaga agar notebook tetap modular.

---

## 🔧 **Immediate Fixes**

| Area            | Fix                                             | Impact                            |
| --------------- | ----------------------------------------------- | --------------------------------- |
| Validation      | Gunakan **Stratified K-Fold (5x)**              | AUC stabil dan realistik          |
| Model           | Tambahkan **regularisasi** + **early stopping** | Kurangi overfit                   |
| Calibration     | Gunakan `CalibratedClassifierCV`                | Probabilitas lebih smooth         |
| Feature Scaling | `StandardScaler()` atau `RobustScaler()`        | Model lebih peka terhadap ranking |
| Runtime         | `tree_method='hist'` + LightGBM CPU             | 2–3x lebih cepat                  |
| Pipeline        | Tambah config dict (`CFG`) untuk semua setting  | Fleksibilitas tinggi              |
| Prompting       | Terapkan **Structured Prompting System**        | Hilangkan panic-prompt            |

---

## 🧩 **Ideas for Next Version**

1. **Config-Driven Template** – Semua hyperparameter, imputer, scaler, dan model diatur lewat satu `CFG` dictionary.
2. **Multiple Template Variants** – Binary AUC, Multiclass F1, Regression (log target).
3. **Experiment Logger** – CSV otomatis (`version, model, FE, CV_AUC, notes`).
4. **Feature Engineering Scratchpad** – Sel khusus untuk eksperimen fitur tanpa ganggu pipeline utama.
5. **Recovery Kit Cell** – Sekali jalan: train LogReg, RF, XGB (calibrated) + blend probabilities.

---

## 🧭 **Next To-Do List**

### 📘 *Before Next Competition*

1. Refactor notebook ke **config-based system**.
2. Tambah **calibration utility** untuk semua model.
3. Siapkan fungsi **soft blending** (average `predict_proba`).
4. Buat **experiment logger** (CSV append).
5. Tambahkan **EDA Pareto cell (5 plots)** otomatis.
6. Buat **submission guard** (`check_submission(schema)`).
7. Siapkan **prompt macro** (3 template cepat: preprocessing, model swap, speed optimize).
8. Integrasikan **Structured Prompting System.md** di project folder.

---

### ⚔️ *During Competition (09:00–12:00)*

| Time        | Focus                                        | Output                 |
| ----------- | -------------------------------------------- | ---------------------- |
| 09:00–09:25 | EDA Pareto + FE 3 fitur                      | Baseline AUC ≥ 0.70    |
| 09:25–10:15 | Train XGB-Hist (calibrated)                  | CV AUC stabil          |
| 10:15–10:55 | Tambah LogReg & RF (calibrated) → soft blend | AUC naik 0.02–0.05     |
| 10:55–11:25 | Full train + validation                      | AUC akhir              |
| 11:25–11:45 | Submission + guard check                     | File valid             |
| 11:45–12:00 | Backup + reflection                          | Log experiment selesai |

---

## ⚡ **Pareto Formula for AUC Competitions**

| Lever                   | What It Improves           | Rule                                       |
| ----------------------- | -------------------------- | ------------------------------------------ |
| **Calibration**         | Probability smoothness     | `CalibratedClassifierCV(method='sigmoid')` |
| **Feature Scaling**     | Relative ranking stability | `StandardScaler()`                         |
| **Soft Blending**       | Reduces variance           | Mean of predict_proba()                    |
| **Stratified CV**       | True generalization        | 5-fold, same label ratio                   |
| **Boosting Models**     | Core discrimination power  | XGBoost / LightGBM                         |
| **Feature Engineering** | Adds ranking signal        | Ratios, flags, log transform               |

---

## 🧩 **Closing Notes**

> “AUC bukan soal benar atau salah —
> tapi seberapa konsisten lo bisa mengenali siapa yang lebih mungkin benar.”

**Next goal:**
Bangun *template, mindset, dan sistem* yang membuat setiap kompetisi bukan lagi adu kecepatan, tapi adu struktur, clarity, dan kontrol diri.


