# An Analysis of Image Processing Performance

The aim of this project is to analyse how image processing techniques perform in terms of image cleaning, image enrichment, and image integration. The datasets used here are the Keras MNIST and CIFAR-10 in-built datasets.

## Image Cleaning
The image cleaning techniques implemented via both Scikit-Learn and OpenCV were:
- **No Cleaning**: no alterations were performed on the data.
- **MinMaxScaler**: the pixel values were scaled between 0 and 1.
- **StandardScaler**: the pixel values were normalised (mean=0, unit variance).
- **QuantileTransformation**: the pixel values were normalised based on the quantiles.
- **PCA**: this involves the projection of the principal components that account for maximum variance.

A breakdown of the performance in each implementation is provided below.

### OpenCV
- The codes available in [this directory](https://github.com/kartika-nair/ImageProcessing-COMP6235/tree/main/Image%20Cleaning%20-%20OpenCV) contain the implementation of the aforementioned cleaning methods in OpenCV.
- The predictions were done via an RNN, and further details have been provided within the repository.
- The results were as follows:
<img width="1870" height="746" alt="image" src="https://github.com/user-attachments/assets/33e4c698-73b1-4c05-b514-bc6d62a70917" />


### Scikit-Learn
- The codes available in [this directory](https://github.com/kartika-nair/ImageProcessing-COMP6235/tree/main/Image%20Cleaning%20-%20Scikit-Learn) contain the implementation of the aforementioned cleaning methods in Scikit-Learn.
- The predictions were done via an CNN, which performed greatly on CIFAR-10.
- For MNIST, MinMaxScaler provides the best performance. Raw data without preprocessing also performs decently due to the simplicity of the dataset. PCA, though useful for dimensionality reduction, shows lower performance as it eliminates some important features for classification.
   <img width="1018" height="983" alt="image" src="https://github.com/user-attachments/assets/94771e07-9e3c-4797-91ab-9da0417e9a48" />

- For CIFAR-10, StandardScaler,QuantileTransformer and MinMaxScaler offer modest improvements, but PCA fail to provide significant benefits, with PCA reducing performance dramatically due to the loss of important spatial information in the images. Raw pixel data (after normalization) performs good, as the CNN model benefits from the full, unaltered image data.
  <img width="1001" height="983" alt="image" src="https://github.com/user-attachments/assets/915088eb-3196-4341-a95f-39d43045cd3f" />
