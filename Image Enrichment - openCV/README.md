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


### Evaluation Standard (Baseline-aware, Complete Version)

The evaluation is based on validation accuracy, using the baseline (no augmentation)
as the primary reference.
Comparison between Level-1 (L1) and Level-2 (L2) methods is secondary.

- **L2 Best**
  - Condition:
    Best Level-2 accuracy > Best Level-1 accuracy
    and Best Level-2 accuracy > Baseline.
  - Meaning:
    TensorFlow-based augmentation achieves the best overall performance.

- **L1 Best (L2 Strong Improvement)**
  - Condition:
    Best Level-1 accuracy > Best Level-2 accuracy,
    and Best Level-2 accuracy shows a clear and non-trivial improvement over Baseline.
  - Meaning:
    Geometric augmentation is optimal, while TensorFlow-based augmentation
    provides strong and meaningful gains.

- **L1 Best (L2 Limited Improvement)**
  - Condition:
    Best Level-1 accuracy > Best Level-2 accuracy,
    and Best Level-2 accuracy shows only a small but positive improvement over Baseline.
  - Meaning:
    Geometric augmentation is clearly superior, and TensorFlow-based augmentation
    provides limited benefit.

- **L1 Best (L2 No Improvement)**
  - Condition:
    Best Level-1 accuracy > Best Level-2 accuracy,
    and Best Level-2 accuracy does not improve over Baseline
    or results in performance degradation.
  - Meaning:
    Geometric augmentation is effective, while TensorFlow-based augmentation
    is ineffective or harmful in this setting.

- **No Clear Gain**
  - Condition:
    Neither Best Level-1 nor Best Level-2 shows a meaningful improvement over Baseline.
  - Meaning:
    Data augmentation provides no clear benefit under this setting.


| Dataset | Dataset Feature Phrase | Baseline Acc | Best L1 (Δ vs Baseline, pp) | Best L2 (Δ vs Baseline, pp) | Best Method (Overall) | Evaluation |
|---|---|---:|---|---|---|---|
| MNIST | Simple structure | 0.9894 | Geom-Combined (+0.25) | MixUp (+0.26) | MixUp (L2) | L2 Best (Limited Improvement) |
| Fashion-MNIST | Ambiguous class boundaries | 0.9118 | Translation (+0.21) | CutMix (+0.79) | CutMix (L2) | L2 Best |
| CIFAR-10 | Position variability in natural scenes | 0.6940 | Translation (+4.22) | MixUp (+1.88) | Translation (L1) | L1 Best (L2 Strong Improvement) |
| SVHN | Structure-sensitive labels | 0.8969 | Translation (+2.82) | CutMix (+1.16) | Translation (L1) | L1 Best (L2 Strong Improvement) |
| STL-10 | Objects with varying positions, orientations, and scales | 0.6215 | Translation (+6.66) | RandAugment (+0.50) | Translation (L1) | L1 Best (L2 Limited Improvement) |



```python

```
