# Image Cleaning - OpenCV

This is an overview of the performance of the image cleaning pre-processing steps across all 5 datasets.

## Methods

The five classical pre-processing methods compared here are listed below:
- No pre-processing
- MinMaxScaler
- StandardScaler
- QuantileTransform
- PCA

## Datasets

The five datasets involved in this comparison, along with some relevant details regarding them, are listed in the table below:

| Dataset           | Domain          | Resolution  | Channels | Dataset Size |
| ----------------- | --------------- | ----------- | -------- | ------------ |
| MNIST             | Digits          | 28×28       | Grey     | 70,000       |
| Fashion-MNIST     | Clothing        | 28×28       | Grey     | 70,000       |
| CIFAR-10          | Objects         | 32×32       | RGB      | 60,000       |
| SVHN              | Street digits   | 32×32       | RGB      | 600,000      |
| STL-10            | Natural objects | 96×96       | RGB      | 105,000      |

The accuracy graphs obtained for each dataset, across the 5 pre-processing methods, are given below:

### MNIST

<img width="567" height="583" alt="image" src="https://github.com/user-attachments/assets/4b0a7801-cf2c-4fe4-b70b-5c35277793d1" />


### Fashion-MNIST

<img width="584" height="583" alt="image" src="https://github.com/user-attachments/assets/c6b3f55d-10f6-42bc-8497-e9284aa410e5" />


### CIFAR-10

<img width="576" height="583" alt="image" src="https://github.com/user-attachments/assets/7c537c1d-b5fc-4563-a722-711912ec3d49" />


### SVHN

<img width="567" height="583" alt="image" src="https://github.com/user-attachments/assets/deccc612-8764-4299-a458-2d48d7fce629" />


### STL-10

<img width="576" height="583" alt="image" src="https://github.com/user-attachments/assets/06498139-7bf9-4e73-a57d-97d38b912319" />


## Comparison of Performance

An overview:
- The overall best-performing dataset across all 5 pre-processing methods is MNIST, while the dataset with the lowest accuracies across all methods is STL-10.
- Fashion-MNIST also performed decently.
- CIFAR-10 had relatively low performance, while the performances of the methods fluctuated significantly when it came to SVHN.
- Looking into why this may have been the case, it appears that all pre-processing methods seem to work better on the MNIST-related datasets due to their relative simplicity (grayscale, smaller size, etc.)
- Fashion-MNIST performed slightly worse than regular MNIST since images of clothing include folds, textures, and ambiguous edges that could affect the pre-processing.
- The scaling methods seem to generalise a bit better than distribution-based methods (QuantileTransform, PCA).
- Notably, QuantileTransform was frequently among the poorer performers (QuantileTransform seems to exaggerate background noise).
- The comparison proves that classical preprocessing works well when foreground/background separation is clean (MNIST) but breaks down under real-world variability (STL-10).

In conclusion:
- Classical image preprocessing is dataset-dependent.
- Methods that work on MNIST do not generalize.
- Real-world images require learned representations.
- Increasing resolution does not guarantee better preprocessing outcomes.

The following table depicts the ideal decision-making for the classical pre-processing methods:

| Dataset       | Flowchart Path             | Selected Method |
| ------------- | -------------------------- | --------------- |
| MNIST         | Greyscale → simple         | Any             |
| Fashion-MNIST | Greyscale → complex        | PCA             |
| CIFAR-10      | RGB → small                | StandardScaler  |
| SVHN          | RGB → large → less noisy   | PCA             |
| STL-10        | RGB → large → more noisy   | StandardScaler  |

This can also be seen in the below flowchart:

<img width="1870" height="746" alt="image" src="https://github.com/user-attachments/assets/f80c2842-9841-4b65-a5e0-e52824bbea9a" />
