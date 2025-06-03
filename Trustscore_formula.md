Here's a complete and **scientific trust score formula** based on all your requirements:

---

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
* $\alpha$: Bonus weight for genuine reviews
* $N_{\text{genuine}}$: Total number of genuine reviews submitted
* $\beta$: Penalty weight factor for fake reviews
* $P(t)$: Active penalty score at time $t$ (defined below)
* $P_{\text{ban}}$: Ban threshold (you specified **5**)

---

### 🔻 **Penalty Score $P(t)$ Definition:**

$$
P(t) = \sum_{i=1}^{N_{\text{fake}}} \mathbb{1}_{[0 \leq t - t_i < T_{\text{decay}}]} \cdot e^{-\lambda (t - t_i)}
$$

---

### 🔍 **Penalty Term Breakdown:**

* $N_{\text{fake}}$: Total number of fake reviews by the user
* $t_i$: Timestamp (in days or weeks) of the $i^{\text{th}}$ fake review
* $\mathbb{1}_{[0 \leq t - t_i < T_{\text{decay}}]}$: Indicator function that **includes only active penalties**
* $T_{\text{decay}}$: Lifetime of a penalty (e.g., **90 days or 3 months**)
* $\lambda$: Decay rate (e.g., $\lambda = \ln 2 / 45$, so penalty halves every 45 days)

---

### 🧠 Intuition:

* The score **increases** with genuine reviews.
* The score **decreases** with fake reviews, but **old penalties decay** over time.
* The user is **banned (score = 0)** when active penalty score $P(t)$ reaches or exceeds **5**.

---

### 📘 Optional: Normalize Trust Score (e.g., 0–100)

$$
\text{TrustScore}_{\text{norm}}(t) = \max\left(0, \min\left(100, \text{TrustScore}(t)\right)\right)
$$

---

Let me know if you'd like:

* A visual plot of how a penalty decays over time
* An example calculation
* A table-based breakdown of penalties and trust score over time
