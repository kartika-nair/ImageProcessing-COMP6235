## **Data Enrichment - OpenCV**

This is the overview of the performance of data enrichment via OpenCV in these 5 datasets： 
- CIFAR-10
- MNIST
- STL10
- SVHN
- fashionMNIST

All datasets are tested using the same six augmentation strategies:
- No Processing
- Rotation
- Translation
- Scaling
- Noise
- Blur

Each dataset is analysed under its best-performing cleaning strategy (e.g. PCA or Standard Scaling), determined in earlier experiments.

## **Analysis of Enrichment Suitability via OpenCV**

### **Suitability Metric**

Augmentation suitability is quantified using the change in test accuracy relative to the No Processing baseline.

Let:

- Acc_none = test accuracy without augmentation
- Acc_aug = test accuracy after augmentation
  
The performance difference is defined as:

- ΔAcc = Acc_aug − Acc_none

Positive and stable ΔAcc values indicate higher suitability for OpenCV-based augmentation.

### **MNIST**

**Test Accuracy Results**

<img width="1768" height="1102" alt="image" src="https://github.com/user-attachments/assets/c9ec2130-c6ff-4128-9482-0cb452806f30" />

- No Processing: 0.964
- Rotation: 0.953 (−1.1%)
- Translation: 0.942 (−2.2%)
- Scaling: 0.964 (≈ 0%)
- Noise: 0.965 (+0.1%)
- Blur: 0.954 (−1.0%)

**Average ΔAcc ≈ −0.4%**

**Analysis**
- MNIST consists of clean, centred grayscale digit images with limited real-world variation.
- Most OpenCV enrichments introduce distortions that do not reflect genuine digit variability, particularly geometric transformations that break digit alignment.
**Conclusion****Conclusion*
  
OpenCV-based enrichment is poorly suited to MNIST, providing no consistent performance improvement.

### **fashionMNIST**

**Test Accuracy Results**

<img width="1284" height="946" alt="image" src="https://github.com/user-attachments/assets/8d4d771a-7640-4407-96fc-591fb332f63b" />

- No Processing: 0.840
- Rotation: 0.811 (−2.9%)
- Translation: 0.788 (−5.2%)
- Scaling: 0.831 (−0.9%)
- Noise: 0.830 (−1.0%)
- Blur: 0.824 (−1.6%)

**Average ΔAcc ≈ −0.6% - −1.0%**

**Analysis**

- FashionMNIST images rely on global shape features for classification.
- Geometric distortions often remove discriminative cues rather than enriching variability.

**Conclusion**

FashionMNIST shows low suitability for OpenCV enrichment, with most methods degrading performance.

### **CIFAR-10**

**Test Accuracy Results**

<img width="1822" height="1092" alt="image" src="https://github.com/user-attachments/assets/228da380-1bf4-404e-bc2f-12192a1206a8" />

- No Processing: 0.372
- Rotation: 0.380 (+0.8%)
- Translation: 0.335 (−3.7%)
- Scaling: 0.376 (+0.4%)
- Noise: 0.100 (−27.0%)
- Blur: 0.372 (≈ 0%)

**Average ΔAcc ≈ +0.2%**

**Analysis**

- CIFAR-10 contains natural RGB images where augmentation is theoretically beneficial.
- However, the SimpleRNN model lacks spatial inductive bias, limiting its ability to exploit spatial transformations.

**Conclusion**

CIFAR-10 demonstrates moderate enrichment suitability, constrained primarily by model architecture.

### **SVHN**

**Test Accuracy Results**

<img width="1478" height="948" alt="image" src="https://github.com/user-attachments/assets/a564b110-8617-48dc-bf18-2a385e53dc66" />

- No Processing: 0.694
- Rotation: 0.676 (−1.8%)
- Translation: 0.677 (−1.7%)
- Scaling: 0.661 (−3.3%)
- Noise: 0.698 (+0.4%)
- Blur: 0.701 (+0.7%)
  
**Average ΔAcc ≈ +0.5%**

**Analysis**

- SVHN images originate from real-world street scenes and naturally contain noise and blur.
- Enrichment that mirror these conditions improve robustness, while geometric transformations distort digit structure.

**Conclusion**

SVHN exhibits high suitability for selective OpenCV augmentation, particularly noise and blur.

### **STL-10**

**Test Accuracy Results**

<img width="1434" height="946" alt="image" src="https://github.com/user-attachments/assets/4e11f44b-70c5-4461-8706-093ebd75117d" />

- No Processing: 0.151
- Rotation: 0.175 (+2.4%)
- Translation: 0.170 (+1.9%)
- Scaling: 0.205 (+5.4%)
- Noise: 0.143 (−0.8%)
- Blur: 0.180 (+2.9%)
  
**Average ΔAcc ≈ +1.5% - +2.0%**

**Analysis**
- STL-10 contains high-resolution natural images with limited labelled data.
- Enrichment effectively increases training diversity and reduces overfitting, especially through scaling and blur.

**Conclusion**

STL-10 shows moderate to high augmentation suitability, despite overall accuracy being constrained by model capacity.
