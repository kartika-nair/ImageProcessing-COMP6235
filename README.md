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

### Scikit-Learn
- The codes available in [this directory](https://github.com/kartika-nair/ImageProcessing-COMP6235/tree/main/Image%20Cleaning%20-%20Scikit-Learn) contain the implementation of the aforementioned cleaning methods in Scikit-Learn.
- - The predictions were done via an CNN, which performed greatly on CIFAR-10.
  
- For MNIST, MinMaxScaler provides the best performance. Raw data without preprocessing also performs decently due to the simplicity of the dataset. PCA, though useful for dimensionality reduction, shows lower performance as it eliminates some important features for classification.
- For CIFAR-10, StandardScaler,QuantileTransformer and MinMaxScaler offer modest improvements, but PCA fail to provide significant benefits, with PCA reducing performance dramatically due to the loss of important spatial information in the images. Raw pixel data (after normalization) performs good, as the CNN model benefits from the full, unaltered image data.

### OpenCV
- The codes available in [this directory](https://github.com/kartika-nair/ImageProcessing-COMP6235/tree/main/Image%20Cleaning%20-%20OpenCV) contain the implementation of the aforementioned cleaning methods in OpenCV.
- The predictions were done via an RNN, which performed poorly on CIFAR-10 as expected (RNNs are designed to handle sequential data and are good with 1D data, but CIFAR-10 requires 2D handling for optimum performance).
- It was observed that, for the MNIST dataset, PCA was the best performer, while QuantileTransformation was the worst by far:
<img width="567" height="583" alt="Untitled" src="https://github.com/user-attachments/assets/9231fd0f-6be0-4e87-8d30-f39368ac8558" />

- It was also observed that, for the CIFAR-10 dataset, MinMaxScaler was the worst performer, while StandardScaler was the best. Interestingly, in this case, PCA and Quantile Transformation seem to perform similarly:
<img width="576" height="583" alt="Untitled" src="https://github.com/user-attachments/assets/a4bb889a-7aee-4493-b35f-1cdfbf277e94" />
