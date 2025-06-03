

## ✅ Final Trust Score Formula with Decaying Penalties and Ban Threshold

```math
\text{TrustScore}(t) = 
\begin{cases}
0, & \text{if } P(t) \geq P_{\text{ban}} \\
S_0 + \alpha \cdot N_{\text{genuine}} - \beta \cdot P(t), & \text{if } P(t) < P_{\text{ban}}
\end{cases}
```

---

### 🔍 Where:

* **`TrustScore(t)`**: Trust score of the user at time `t`
* **`S₀`**: Base trust score (e.g., 50)
* **`α`**: Bonus weight per genuine review
* **`N₍genuine₎`**: Total number of genuine reviews
* **`β`**: Penalty weight for fake reviews
* **`P(t)`**: Active penalty score at time `t`
* **`P₍ban₎`**: Ban threshold (e.g., 5)

---

## 🔻 Penalty Score Formula

```math
P(t) = \sum_{i=1}^{N_{\text{fake}}} \mathbb{1}_{[0 \leq t - t_i < T_{\text{decay}}]} \cdot e^{-\lambda (t - t_i)}
```

---

### 🔍 Penalty Term Breakdown:

* **`N₍fake₎`**: Number of fake reviews
* **`tᵢ`**: Timestamp of the *i-th* fake review (in days)
* **`𝟙[0 ≤ t - tᵢ < T₍decay₎]`**: Indicator function — 1 if within penalty lifetime, else 0
* **`T₍decay₎`**: Penalty lifetime (e.g., 90 days)
* **`λ`**: Decay rate constant

  * Suggested: `λ = ln(2)/45` → Half-life of 45 days

---

## 🧠 Intuition

* Trust score **increases** with genuine reviews
* Fake reviews **penalize**, but penalty **decays over time**
* Penalties **disappear** after `T₍decay₎`
* If `P(t) ≥ P₍ban₎`, user is **banned** (Trust Score = 0)

---

## 📘 Normalized Trust Score (Optional)

```math
\text{TrustScore}_{\text{norm}}(t) = \max\left(0, \min\left(100, \text{TrustScore}(t)\right)\right)
```

---

## 🧪 Example Parameters

| Symbol     | Value    | Meaning                   |
| ---------- | -------- | ------------------------- |
| `S₀`       | 50       | Initial trust             |
| `α`        | 2        | Points per genuine review |
| `β`        | 1        | Penalty per fake score    |
| `λ`        | ln(2)/45 | Half-life decay constant  |
| `T₍decay₎` | 90 days  | Penalty window            |
| `P₍ban₎`   | 5        | Ban if penalty ≥ 5        |

---

### 📝 Notes:

* All times (`t`, `tᵢ`) should be in the **same unit** (e.g., days).
* You can compute this in Python, R, or any backend for reputation tracking.
* Useful for trust systems in **review platforms**, **marketplaces**, or **content moderation**.

