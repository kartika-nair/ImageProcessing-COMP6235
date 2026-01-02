# A Comparison of Image Processing Techniques

The aim of this project is to analyse how image processing techniques perform in terms of image cleaning, image enrichment, and image integration. 

## Image Cleaning
The image cleaning techniques implemented via both Scikit-Learn and OpenCV were:
- **No Cleaning**: no alterations were performed on the data.
- **MinMaxScaler**: the pixel values were scaled between 0 and 1.
- **StandardScaler**: the pixel values were normalised (mean=0, unit variance).
- **QuantileTransformation**: the pixel values were normalised based on the quantiles.
- **PCA**: this involves the projection of the principal components that account for maximum variance.

The datasets used here are the MNIST, CIFAR-10, Fashion-MNIST, SVHN, and STL-10 datasets.

A breakdown of the performance in each implementation is provided below.

### OpenCV
- The codes available in [this directory](https://github.com/kartika-nair/ImageProcessing-COMP6235/tree/main/Image%20Cleaning%20-%20OpenCV) contain the implementation of the aforementioned cleaning methods in OpenCV.
- The predictions were done via an RNN, and further details have been provided within the repository.
- The results were as follows:
<img width="1870" height="746" alt="image" src="https://github.com/user-attachments/assets/33e4c698-73b1-4c05-b514-bc6d62a70917" />


### Scikit-Learn
- The codes available in [this directory](https://github.com/kartika-nair/ImageProcessing-COMP6235/tree/main/Image%20Cleaning%20-%20Scikit-Learn) contain the implementation of the aforementioned cleaning methods in Scikit-Learn.
- The predictions were done via a CNN, and further details have been provided within the repository.
- The results were as follows:
```mermaid
flowchart TD
    Start([START]) --> ModelType{Is the model<br/>Traditional ML or<br/>Deep Learning CNN?}
    
    ModelType -->|Traditional ML<br/>Logistic Regression| SimpleData{Is the data simple<br/>with clean<br/>foreground/background<br/>separation?}
    SimpleData -->|Yes| MinMax1[MINMAX SCALER<br/>Best for MNIST]
    SimpleData -->|No| MinMaxStd1[MINMAX SCALER<br/>or STANDARD SCALER]
    
    ModelType -->|Deep Learning<br/>CNN| ColorType{Is the dataset<br/>Greyscale or RGB?}
    
    ColorType -->|Greyscale<br/>Fashion-MNIST| StdRaw1[STANDARD SCALER<br/>or RAW DATA<br/>CNNs are robust]
    
    ColorType -->|RGB| DatasetSize{Is the dataset<br/>small<br/>&lt; 100k images?}
    
    DatasetSize -->|Yes<br/>CIFAR-10| StdRaw2[STANDARD SCALER<br/>or RAW DATA]
    
    DatasetSize -->|No| NoisyData{Is the dataset<br/>very noisy and<br/>non-uniform?}
    
    NoisyData -->|Yes<br/>STL-10| StdRaw3[STANDARD SCALER<br/>or RAW DATA]
    
    NoisyData -->|No<br/>SVHN| StdRaw4[STANDARD SCALER<br/>or RAW DATA]
    
    style MinMax1 fill:#90EE90
    style StdRaw1 fill:#87CEEB
    style StdRaw2 fill:#87CEEB
    style StdRaw3 fill:#87CEEB
    style StdRaw4 fill:#87CEEB
    style MinMaxStd1 fill:#FFD700
```

## Image Integration
The image integration techniques implemented were:
- Pillow
- Scikit-Image
- OpenCV

The codes available in [this directory](https://github.com/kartika-nair/ImageProcessing-COMP6235/tree/main/%E6%95%B0%E6%8D%AE%E6%95%B4%E5%90%88) contain the implementation of the same. This was performed on the SVHN, MNIST, and USPS datasets.

The results were as follows:
```mermaid
flowchart TD
    Start([Start: Image Integration Task]) --> CheckSize{"<b>Condition 1:</b><br/>Are all input images<br/>already the same size?"}
    
    CheckSize -->|Yes<br/>Homogeneous Data| Numpy["<b>NumPy Stacking</b><br/>Zero Overhead"]
    
    CheckSize -->|No<br/>Heterogeneous Data| RealTime{"<b>Condition 2:</b><br/>Is Real-time Performance<br/>Critical? <br/>(> 1000 IPS)"}
    
    RealTime -->|Yes<br/>Industrial/Web App| PillowChoice["<b>PILLOW (PIL)</b><br/>~1800 IPS<br/>Best for Speed"]
    
    RealTime -->|No<br/>Research/Offline| QualityCheck{"<b>Condition 3:</b><br/>Is Anti-aliasing /<br/>High Fidelity Required?"}
    
    QualityCheck -->|Yes<br/>e.g. Low-Res Upscaling| SkimageChoice["<b>SCIKIT-IMAGE</b><br/>High Precision<br/>Best for Quality"]
    
    QualityCheck -->|No<br/>Standard Thumbnails| PillowChoice
    
    %% Styling
    style Start fill:#f9f,stroke:#333,stroke-width:2px
    style PillowChoice fill:#90EE90,stroke:#333,stroke-width:2px
    style SkimageChoice fill:#87CEEB,stroke:#333,stroke-width:2px
    style Numpy fill:#FFD700,stroke:#333,stroke-width:2px
```
