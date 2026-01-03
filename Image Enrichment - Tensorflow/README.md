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
| MNIST | 0.9894 | +0.20% | +0.03% | MixUp (L2) | 0.9920 | +0.26 | L2 Best |
| Fashion-MNIST | 0.9118 | −0.89% | −0.16% | CutMix (L2) | 0.9197 | +0.79 | L2 Best |
| CIFAR-10 | 0.6940 | +0.81% | +0.74% | Translation (L1) | 0.7362 | +4.22 | L1 Best |
| SVHN | 0.8969 | +1.10% | +0.80% | Translation (L1) | 0.9251 | +2.82 | L1 Best |
| STL-10 | 0.6215 | +3.69% | −0.29% | Translation (L1) | 0.6881 | +6.66 | L1 Best |



```python

```
