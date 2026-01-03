### Method Definition

- **Baseline**
  - No augmentation  
  - **Method 0**

- **Level 1 (L1, OpenCV-style geometric augmentation)**
  - RandomRotation — **Method 1**
  - RandomTranslation — **Method 2**
  - RandomZoom — **Method 3**
  - Geometric-Combined (Rotation + Translation + Zoom) — **Method 4**

- **Level 2 (L2, TensorFlow-based augmentation)**
  - MixUp — **Method 5**
  - CutMix — **Method 6**
  - RandAugment — **Method 7**


### Evaluation Remark Standard

> The evaluation remark is assigned strictly based on validation accuracy
> comparison among three values:
> **Baseline**, **Best Level-1**, and **Best Level-2**.
>  
> No average values, trends, or subjective interpretations are used.

- **L2 Best**  
  - Condition:  
    **Best L2 accuracy > Best L1 accuracy**
  - Interpretation:  
    TensorFlow-based augmentation achieves the best performance on this dataset.

- **L2 Helpful**  
  - Condition:  
    **Best L2 accuracy > Baseline**  
    and  
    **Best L2 accuracy ≤ Best L1 accuracy**
  - Interpretation:  
    TensorFlow-based augmentation improves over no augmentation,
    but does not surpass the best geometric method.

- **L1 Best**  
  - Condition:  
    **Best L1 accuracy > Best L2 accuracy**
  - Interpretation:  
    OpenCV-style geometric augmentation is more effective on this dataset.

- **No Clear Gain**  
  - Condition:  
    Neither **Best L1** nor **Best L2** shows a meaningful improvement over **Baseline**.
  - Interpretation:  
    Data augmentation does not provide a clear benefit under this setting.


| Dataset | Baseline Acc | L1 Avg ΔAcc | L2 Avg ΔAcc | Best Method (Overall) | Best Acc | Δ vs Baseline (pp) | Evaluation |
|---|---:|---:|---:|---|---:|---:|---|
| MNIST | 0.9899 | +0.15% | +0.11% | Rotation (L1) | 0.9930 | +0.31 | No Clear Gain |
| Fashion-MNIST | 0.9181 | −2.85% | −0.89% | MixUp (L2) | 0.9184 | +0.03 | L2 Best |
| CIFAR-10 | 0.7073 | −2.07% | −0.31% | RandAugment (L2) | 0.7109 | +0.36 | L2 Best |
| SVHN | 0.9015 | −0.04% | −1.09% | Translation (L1) | 0.9152 | +1.37 | L1 Best |
| STL-10 | 0.6077 | +2.21% | +1.09% | Translation (L1) | 0.6804 | +7.27 | L1 Best |


## Dataset-wise Best Method Analysis

This section analyzes the best-performing augmentation method for each dataset and explains why it is suitable.  
Explanations are strictly based on validation accuracy results and dataset characteristics.

---

### MNIST

**Best method:**  
- RandomRotation (Level 1) — 0.9930  
- Best Level-2 result (CutMix): 0.9920

**Why this method is suitable:**  
MNIST consists of centered, low-variance handwritten digits with simple structures.  
Small rotations introduce limited but realistic variations without changing digit identity.  
Since the baseline accuracy is already near saturation (≈99%), neither stronger geometric transformations nor sample-level mixing provides meaningful additional gains.

**Why Level-2 is not advantageous:**  
Level-2 methods introduce stronger regularization (e.g., sample mixing), which does not address any real generalization bottleneck in MNIST.  
As a result, Level-2 performs similarly to Level-1 but does not surpass it.

---

### Fashion-MNIST

**Best method:**  
- MixUp (Level 2) — 0.9184 (global best)

**Why this method is suitable:**  
Fashion-MNIST contains classes with high intra-class variability and ambiguous class boundaries (e.g., shirt vs. pullover).  
MixUp performs sample-level interpolation, smoothing decision boundaries and reducing overconfident predictions without distorting object geometry.  
This allows MixUp to outperform all geometric (Level-1) methods.

**Why Level-1 performs worse:**  
Geometric transformations often distort clothing silhouettes, which are critical discriminative features.  
As a result, Level-1 methods consistently reduce validation accuracy.

---

### CIFAR-10

**Best method:**  
- RandAugment (Level 2) — 0.7109 (global best)

**Why this method is suitable:**  
CIFAR-10 consists of small natural images with complex backgrounds and diverse object appearances.  
RandAugment introduces stochastic, training-integrated perturbations that increase data diversity without enforcing fixed geometric invariances.  
This flexibility allows it to outperform all single geometric transformations.

**Why Level-1 fails relative to Level-2:**  
All Level-1 methods underperform the baseline, indicating that fixed geometric assumptions do not align well with CIFAR-10’s visual variability.  
Level-2 methods are the only ones capable of surpassing the baseline in this setting.

---

### SVHN

**Best method:**  
- RandomTranslation (Level 1) — 0.9152

**Why this method is suitable:**  
In SVHN, class identity is tightly coupled with precise digit structure, while real-world variation mainly comes from spatial shifts and cropping.  
Translation directly models this variation without altering digit shape, leading to the highest validation accuracy.

**Why Level-2 performs poorly:**  
Level-2 methods such as MixUp and CutMix introduce sample mixing or partial occlusion, which disrupts digit structure.  
Since SVHN already generalizes well, this additional regularization becomes harmful rather than beneficial.

---

### STL-10

**Best method:**  
- RandomTranslation (Level 1) — 0.6804

**Why this method is suitable:**  
STL-10 contains high-resolution images but very limited labeled data, resulting in severe overfitting.  
Translation substantially increases effective data diversity while preserving object identity, leading to the largest performance gain.

**Why Level-2 is not optimal (but still effective):**  
Level-2 methods such as CutMix (0.6527) significantly improve over the baseline (+4.50pp), demonstrating the effectiveness of sample-level regularization.  
However, mixed semantics introduced by these methods may be less aligned with the small labeled set, preventing them from surpassing the best geometric method.

---

## Summary: When and Why Level-2 Underperforms

Based strictly on the experimental results:

- **Level-2 underperforms on:**
  - MNIST (no generalization bottleneck)
  - SVHN (structure-sensitive semantics)
  - STL-10 (geometric diversity is more beneficial)

- **Common characteristics of Level-2-unfavorable datasets:**
  - Highly structure-sensitive classes  
  - Near-saturated baseline performance  
  - Scenarios where realistic variation is predominantly geometric  

---

## Takeaway

Level-2 TensorFlow-based augmentations are most effective when class boundaries are ambiguous and fixed geometric assumptions fail,  
while they offer limited or negative benefits for structure-sensitive or near-saturated classification tasks.



```python

```
