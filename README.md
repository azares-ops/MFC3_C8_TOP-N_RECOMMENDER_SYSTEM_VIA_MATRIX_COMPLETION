#  📃 Top-N Recommender System via Matrix Completion

![MATLAB](https://img.shields.io/badge/MATLAB-Used-orange)
![Algorithm](https://img.shields.io/badge/ADMM-Optimization-blue)
![Model](https://img.shields.io/badge/Matrix%20Completion-LogDet-green)

## 📌 Overview

This project implements a **Top-N Recommender System** using **Matrix Completion with LogDet optimization**.

The goal is to predict missing entries in a sparse **user–item matrix** and generate accurate recommendations.

Recommender systems are widely used in platforms like Netflix, Amazon, and Spotify.

## 🧠 Key Highlights

- LogDet surrogate instead of Nuclear Norm  
- ADMM optimization for efficient solving  
- Handles highly sparse datasets  
- Evaluated using HR@N and ARHR@N

## 👥 Team C-8

| Name | Roll No |
|------|--------|
| Sai Reddy | CB.SC.U4AIE24205 |
| Devana | CB.SC.U4AIE24213 |
| Tharappel Manas | CB.SC.U4AIE24257 |
| Zahwa K | CB.SC.U4AIE24261 |

## 🎯 Problem Statement

- User–item matrices are sparse  
- Many ratings are missing  
- Need to predict missing values for Top-N recommendations  

### Challenges:
- Rank minimization is NP-hard  
- Nuclear norm over-penalizes  
- LogDet provides better approximation

## ⚙️System Architecture

```mermaid
graph LR
A[Input Matrix] --> B[Mask]
B --> C[ADMM Optimization]
C --> D[Completed Matrix]
D --> E[Top-N Recommendation]
E --> F[Evaluation - HR/ARHR]

```
---

## 🧮 Methodology

We aim to recover the completed matrix **X** from the observed matrix **M**.

---

### 🔹 Objective Function

The optimization problem is:

minimize:  
log det (XᵀX + I) + (μ / 2) || PΩ(X − M) ||²_F

Where:

- X → Completed matrix  
- M → Observed matrix  
- Ω → Set of observed indices  
- PΩ → Projection onto observed entries  
- μ → Regularization parameter  
- ||·||_F → Frobenius norm  

---

### 🔹 Optimization Technique

We solve the problem using **ADMM (Alternating Direction Method of Multipliers)**.

---

### 🔹 Update Steps

**1. X Update (Low-rank approximation)**  
- Perform Singular Value Decomposition (SVD):  
X = U Σ Vᵀ  
- Apply LogDet-based shrinkage  

---

**2. Y Update (Constraint enforcement)**  
Y = max(0, X + Z)

---

**3. Z Update (Dual variable update)**  
Z = Z + (X − Y)

---

### 🔹 Generating Top-N Recommendations

Once the completed matrix X is obtained:

1. For each user u, take row Xu  
2. Remove already observed items:  
   Xu(i) = 0 for all i ∈ Ωu  
3. Sort remaining items in descending order  
4. Select top N items  

Top-Nᵤ = argsort(Xu, descending)[:N]

---

### 🔹 Final Output

- Completed matrix X  
- Personalized Top-N recommendation list for each user  

## 📊 Datasets

| Dataset | Domain | Users | Items | Density |
|--------|--------|------|------|--------|
| MovieLens | Movies | 943 | 1682 | 6.3% |
| LastFM | Music | 1892 | 17632 | 0.28% |
| Delicious | Bookmark | 2078 | 12096 | 0.20% |
| BX | Books | 2078 | 9300 | 0.50% |
| Netflix | Movies | 5000 | 17000 | 0.35% |

## 📈 Performance Metrics

### 🔹 Hit Ratio (HR@N)

Measures whether the correct item appears in the Top-N recommendations.

HR@N = (Number of Hits) / (Total Users)

Where:
- A "hit" occurs if the test item is present in the Top-N list

---

### 🔹 Average Reciprocal Hit Rank (ARHR@N)

Rewards higher-ranked correct recommendations.

ARHR@N = (1 / |U|) × Σ (1 / rankᵤ)

Where:
- U → Set of users  
- rankᵤ → Position of the correct item in Top-N list for user u  
- If item is not in Top-N, contribution = 0  

---

### 🔹 Interpretation

- Higher HR → better coverage  
- Higher ARHR → better ranking quality  

## 📊 Results

| Dataset | HR@10 | ARHR@10 |
|--------|------|--------|
| MovieLens | 0.9466 | 0.4197 |
| LastFM | 0.2573 | 0.1100 |
| Delicious | 0.2366 | 0.0943 |
| BX | 0.7365 | 0.2976 |
| Netflix | 0.3597 | 0.0721 |

## 📂 Project Structure

Project contents: :contentReference[oaicite:0]{index=0}

## 🛠️ How to Run

```bash
1. Open MATLAB
2. Load .mlx file
3. Run preprocessing
4. Execute ADMM model
5. Evaluate results

```
---

# 📚 REFERENCES
```md


- Ning & Karypis — SLIM Recommender Systems  
- Shi & Yu — Matrix Completion Limitations  
- Kang et al. — LogDet Rank Minimization

```
---
## 🌟 Conclusion

- LogDet improves rank approximation  
- ADMM ensures efficient optimization  
- Strong performance on sparse datasets

