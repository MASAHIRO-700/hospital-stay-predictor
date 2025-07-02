# 入院日数および入院有無の予測モデル  
**Prediction of Hospital Stay Duration and Admission Status**

本プロジェクトでは、ワクチン接種後に発生した有害事象に関するデータ（VAERS）を用いて、  
**入院日数の予測（回帰）** および **入院有無の予測（分類）** を行う機械学習モデルを構築・評価しました。  
*This project uses data on adverse events after vaccination (VAERS) to build and evaluate machine learning models for predicting hospital stay duration (regression) and admission status (classification).*

---

## プロジェクト概要 / Project Overview

- **目的 / Objectives**：
  - 入院日数（HOSPDAYS）を予測 → 医療リソースの事前準備・配分に活用  
    *Predict hospital stay duration (HOSPDAYS) → To support preparation and allocation of medical resources*
  - 入院の有無（HOSPITAL）を予測 → 医師の判断支援やベッド稼働率の調整に貢献  
    *Predict hospitalization status (HOSPITAL) → To assist clinical decision-making and bed occupancy management*

- **使用データ / Dataset**：  
  - 米国のワクチン有害事象報告システム（VAERS: Vaccine Adverse Event Reporting System）  
    *U.S. Vaccine Adverse Event Reporting System (VAERS)*  
  - 年齢・性別・接種日・発症日・症状・救急受診歴などを含む  
    *Includes age, sex, vaccination date, onset date, symptoms, ER visit history, etc.*

- **手法 / Methods**：
  - 回帰：線形回帰、LightGBM  
    *Regression: Linear Regression, LightGBM*
  - 分類：ランダムフォレスト、LightGBM（＋SHAPによる解釈）  
    *Classification: Random Forest, LightGBM (with SHAP interpretation)*

- **評価指標 / Evaluation Metrics**：
  - 回帰：R²、MAE、RMSE  
    *Regression: R², MAE, RMSE*
  - 分類：Accuracy、Recall、F1スコア  
    *Classification: Accuracy, Recall, F1 Score*

---

## ファイル構成 / File Structure

| ファイル名 / File Name | 説明 / Description |
|------------------------|---------------------|
| `vaccine_hospitalization_prediction_jp.ipynb` | 日本語によるノートブック（前処理・モデル構築・可視化・解釈までを日本語で記述）<br>*Notebook written in Japanese, including preprocessing, modeling, visualization, and interpretation* |
| `vaccine_hospitalization_prediction_en.ipynb` | 英語によるノートブック（内容は日本語版と同様だが、コメント・出力・可視化すべて英語表記）<br>*English version of the notebook with the same content as the Japanese version; all comments, outputs, and visualizations are in English* |
| `README.md`            | この説明ファイル（日本語と英語を併記）<br>*This README file with both Japanese and English explanations* |


---

## 主な結果 / Main Results

### 入院日数（回帰）/ Hospital Stay Duration (Regression)

- 線形回帰およびLightGBMともに **R²は0.05未満** と低く、有効な予測モデルの構築には至らず。  
  *Both linear regression and LightGBM resulted in an R² below 0.05, indicating poor predictive performance.*
- 入院日数に影響する重要な情報（既往歴や病態など）が不足していた可能性。  
  *Key features such as patient history or underlying conditions may have been missing.*

### 入院有無（分類）/ Hospital Admission Status (Classification)

- LightGBMモデルで **F1スコア：0.83、再現率：0.83** を達成。  
  *LightGBM achieved F1 score: 0.83 and Recall: 0.83.*
- SHAP分析により、重要な特徴量は以下の通り：  
  *SHAP analysis revealed the following important features:*
  - `ONSET_LAG`（発症までの期間 / Duration to onset）
  - `ER_ED_VISIT`（救急処置室での受診有無 / ER visit status）
  - `AGE_YRS`（年齢 / Age）

---

## 今後の展望 / Future Outlook

- 患者の**基礎疾患・介護状況・社会的背景**などを追加することで、入院日数予測の精度向上が期待される。  
  *Adding information on pre-existing conditions, caregiving status, and social background could improve regression accuracy.*

- 分類モデルについては、さらに異なるアルゴリズムの導入・アンサンブル化も検討。  
  *For classification models, exploring alternative algorithms or ensemble methods is recommended.*

---

## 使用技術 / Technologies Used

- Python, Pandas, NumPy, Scikit-learn, LightGBM, XGBoost, SHAP, Matplotlib, imbalanced-learn

---

## お問い合わせ / Contact

- Author: Masahiro Okada  
- GitHub: [@MASAHIRO-700](https://github.com/MASAHIRO-700)
