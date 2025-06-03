## ✅ **Final Trust Score Formula with Decaying Penalties and Ban Threshold**

$$
\text{TrustScore}(t) = 
\begin{cases}
0, & \text{if } P(t) \geq P_{\text{ban}} \\
S_0 + \alpha \cdot N_{\text{genuine}} - \beta \cdot P(t), & \text{if } P(t) < P_{\text{ban}}
\end{cases}
$$

---

### 🔍 **Where:**

* $\text{TrustScore}(t)$: Trust score of the user at time $t$
* $S_0$: Base trust score (e.g., 50)
* $\alpha$: Bonus weight per genuine review
* $N_{\text{genuine}}$: Total number of genuine reviews
* $\beta$: Penalty weight factor for fake reviews
* $P(t)$: Active penalty score at time $t$ (defined below)
* $P_{\text{ban}}$: Ban threshold (e.g., 5)

---

### 🔻 **Penalty Score $P(t)$ Definition:**

$$
P(t) = \sum_{i=1}^{N_{\text{fake}}} \mathbb{1}_{[0 \leq t - t_i < T_{\text{decay}}]} \cdot e^{-\lambda (t - t_i)}
$$

---

### 🔍 **Penalty Term Breakdown:**

* $N_{\text{fake}}$: Number of fake reviews
* $t_i$: Timestamp (e.g., in days) of the $i^\text{th}$ fake review
* $\mathbb{1}_{[0 \leq t - t_i < T_{\text{decay}}]}$: Indicator function — active only for reviews in the past $T_{\text{decay}}$
* $T_{\text{decay}}$: Penalty lifetime (e.g., 90 days)
* $\lambda$: Decay rate constant, e.g., $\lambda = \frac{\ln 2}{45}$ ⇒ half-life = 45 days

---

### 🧠 **Intuition:**

* Trust score grows with genuine reviews
* Fake review penalties decay over time
* Penalty disappears after 3 months
* If penalty score reaches 5 or more, trust score is **zeroed (banned)**

---

### 📘 **Optional Normalized Trust Score:**

$$
\text{TrustScore}_{\text{norm}}(t) = \max\left(0, \min\left(100, \text{TrustScore}(t)\right)\right)
$$

