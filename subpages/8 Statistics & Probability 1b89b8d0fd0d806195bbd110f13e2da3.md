# 8. Statistics & Probability

Understanding statistics is crucial for **interpreting data** correctly.

# Descriptive Statistics

Descriptive statistics summarize and **describe** datasets.

## Mean, Median, and Mode

- **Mean (Average):** Sum of all values divided by the count.
- **Median (Middle Value):** The middle number when sorted.
- **Mode (Most Frequent Value):** The most common value.

```python
import numpy as np
import scipy.stats as stats

data = [10, 20, 30, 40, 50, 50, 60, 70, 80, 90]

mean_value = np.mean(data)
median_value = np.median(data)
mode_value = stats.mode(data, keepdims=True)

print("Mean:", mean_value)
print("Median:", median_value)
print("Mode:", mode_value.mode[0] if mode_value.mode.ndim > 0 else mode_value.mode)
```

```
Mean: 50.0
Median: 50.0
Mode: 50
```

## Variance & Standard Deviation

- **Variance:** Measures how spread out numbers are from the mean.
- **Standard Deviation (STD):** Square root of variance.

```python
variance_value = np.var(data, ddof=1)  # ddof=1 for sample variance
std_value = np.std(data, ddof=1)

print("Variance:", variance_value)
print("Standard Deviation:", std_value)
```

```
Variance: 666.6666666666666
Standard Deviation: 25.81988897471611
```

# Probability

Probability quantifies **uncertainty.**

## Independent vs. Dependent Events

- **Independent Event:** Outcome of one does NOT affect the other (e.g., coin flips).
- **Dependent Event:** Outcome of one **affects** the probability of another (e.g., drawing cards without replacement).

## Probability Rules

- **Rule 1:** `P(A) = (Favorable Outcomes) / (Total Outcomes)`
- **Rule 2:** `P(A or B) = P(A) + P(B) - P(A and B)` (*Addition Rule)*
- **Rule 3:** `P(A and B) = P(A) * P(B)` (*Multiplication Rule for Independent Events)*

```python
# Probability of rolling a 3 or a 5 on a 6-sided die
p_3 = 1/6
p_5 = 1/6
p_3_or_5 = p_3 + p_5  # Since they are mutually exclusive

print("P(3 or 5):", p_3_or_5)
```

```
P(3 or 5): 0.3333333333333333
```

# Common Probability Distributions

Probability distributions describe **how data is distributed.**

## Normal Distribution (Bell Curve)

The **normal distribution** is commonly seen in real-world data (e.g., heights, IQ scores).

```python
import matplotlib.pyplot as plt
import seaborn as sns

data = np.random.normal(loc=50, scale=15, size=1000)  # Mean=50, STD=15
sns.histplot(data, bins=30, kde=True)
plt.title("Normal Distribution")
plt.show()
```

![image.png](8%20Statistics%20&%20Probability%201b89b8d0fd0d806195bbd110f13e2da3/image.png)

- A bell-shaped **normal distribution.**
- **Properties:**
    - **68% of data** falls within **1 standard deviation** of the mean.
    - **95% of data** falls within **2 standard deviations** of the mean.

## Binomial Distribution (Yes/No Outcomes)

Used for events with two possible outcomes (e.g., pass/fail, heads/tails).

```python
from scipy.stats import binom

n, p = 10,0.5  # 10 trials, 50% probability of success
binomial_dist = binom.rvs(n, p, size=1000)

sns.histplot(binomial_dist, bins=10, kde=False)
plt.title("Binomial Distribution")
plt.show()
```

![image.png](8%20Statistics%20&%20Probability%201b89b8d0fd0d806195bbd110f13e2da3/image%201.png)

# Statistical Inference

Making **predictions** based on **sample data.**

## Confidence Intervals

A **confidence interval** provides a range of values **likely to contain the true population mean.**

```python
import scipy.stats as stats

sample_data = np.random.normal(loc=50, scale=15, size=30)
mean = np.mean(sample_data)
std_err = stats.sem(sample_data)  # Standard error
confidence_interval = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)

print("95% Confidence Interval:", confidence_interval)
```

```
95% Confidence Interval: (np.float64(46.71316946017841), np.float64(55.925196388321915))
```

## Hypothesis Testing (T-Test)

Used to check if **two groups are significantly different.**

- **Null Hypothesis ($H_o$):** No difference between means.
- **Alternative Hypothesis ($H_1$):** A significant difference exists.

```python
group1 = np.random.normal(50, 10, 30)
group2 = np.random.normal(55, 10, 30)

t_stat, p_value = stats.ttest_ind(group1, group2)
print("T-statistic:", t_stat)
print("P-value:", p_value)
```

```
T-statistic: -2.953703849680537
P-value: 0.004529227048416641
```

If p-value < 0.05, we **reject the null hypothesis (significant difference exists).**

# Correlation vs. Causation

- **Correlation:** Two variables are **related** but one does NOT cause the other.
- **Causation:** One variable **directly influences** another.

**Example:**

- **Correlation:** Ice cream sales **increase** as downing incidents increase → But one **does NOT** cause the other (seasonal effect).
- **Causation:** Smoking **causes** lung cancer.

```python
df = pd.DataFrame({"X": np.random.rand(50), "Y": np.random.rand(50)})

print("Correlation Coefficient:", df.corr().iloc[0,1])
```

```
Correlation Coefficient: 0.16615443780353997
```

# Practice Problems

## **Descriptive Statistics**

Compute **mean, median, mode, variance, standard deviation** for a dataset.

```python
sample_data = [12, 15, 20, 21, 22, 24, 30, 35, 40, 50]

print("Mean:", np.mean(sample_data))

print("Median:", np.median(sample_data))

mode_result = stats.mode(sample_data, keepdims=True)
print("Mode:", mode_result.mode[0] if mode_result.mode.ndim > 0 else mode_result.mode)

print("Variance:", np.var(sample_data, ddof=1))  # Sample variance

print("Standard Deviation:", np.std(sample_data, ddof=1))  # Sample standard deviation
```

```
Mean: 26.9
Median: 23.0
Mode: 12
Variance: 139.87777777777777
Standard Deviation: 11.826993606905255
```

## **Probability Rules**

Calculate **P(A or B)** for rolling a die.

```python
p_2 = 1 / 6  # Probability of rolling a 2
p_4 = 1 / 6  # Probability of rolling a 4
p_2_or_4 = p_2 + p_4  # P(A or B) for mutually exclusive events

print("P(2 or 4):", p_2_or_4)
```

```
P(2 or 4): 0.3333333333333333
```

The probability of rolling a **2 or 4** on a fair die is **33.3%.**

## **Distributions**

Generate **normal & binomial distributions** and visualize them.

```python
# Normal distribution
normal_data = np.random.normal(loc=50, scale=15, size=1000)
plt.figure(figsize=(12, 5))
plt.subplot(1, 2, 1)
sns.histplot(normal_data, bins=30, kde=True, color="blue")
plt.title("Normal Distribution")

# Binomial Distribution
n, p = 10, 0.5 # 10 trials, 50% success probability
binomial_data = binom.rvs(n, p, size=1000)
plt.subplot(1, 2, 2)
sns.histplot(binomial_data, bins=10, kde=False, color="red")
plt.title("Binomial Distribution")
plt.show()
```

![image.png](8%20Statistics%20&%20Probability%201b89b8d0fd0d806195bbd110f13e2da3/image%202.png)

## **Confidence Intervals**

Compute a **95% confidence interval** for a sample dataset.

```python
sample_conf_data = np.random.normal(loc=50, scale=15, size=30)
mean_conf = np.mean(sample_conf_data)
std_err = stats.sem(sample_conf_data)  # Standard error
confidence_interval = stats.t.interval(0.95, len(sample_conf_data)-1, loc=mean_conf, scale=std_err)

print("Confidence Interval:", confidence_interval)
```

```
Confidence Interval: (np.float64(37.353364616920494), np.float64(47.33231371284378))
```

We are **95% confident** the **true population mean** lies between **37.4 and 47.3.**

## **Hypothesis Testing**

Compare two groups using a **T-test** and determine statistical significance.

```python
group1 = np.random.normal(50, 10, 30)
group2 = np.random.normal(55, 10, 30)

t_stat, p_value = stats.ttest_ind(group1, group2)

print("t-test:", t_stat)
print("p-value:", p_value)
```

```
t-test: -1.692060091859256
p-value: 0.09600089575981824
```

- **P-value (0.096) > 0.05**, meaning we **fail to reject the null hypothesis.**
- There is **no significant difference** between the two groups.

## **Correlation Analysis**

Find correlation between **two random variables.**

```python
df_corr = pd.DataFrame({"X": np.random.rand(50) * 100,
												"Y": np.random.rand(50) * 100})
												
correlation_coefficient = df_corr.corr().iloc[0, 1]
print("Correlation Coefficient:", correlation_coefficient)										
```

```
Correlation Coefficient: 0.20901854288336075
```

**Weak positive correlation (0.21)** means no strong relationship between **X and Y.**