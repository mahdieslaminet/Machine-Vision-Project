## 🗒️ README

### Introduction

This project involves using Google Colab for data augmentation and training a Convolutional Neural Network (CNN) for binary classification tasks. The dataset used is composed of COVID-19 X-ray images.

### Prerequisites

- A Google account
- Basic knowledge of Google Colab
- Familiarity with Python and TensorFlow

### Getting Started

#### Google Colab Setup

If you are unfamiliar with using Colab, you can use the following guide:
[Colab Guide](https://www.aparat.com/v/u751kb9)

#### Loading Code and Dataset

- **Code Link**: [Google Drive - code](https://drive.google.com/file/d/1txtIL0QpKRPoHn4Fjun5Jw6Vmmkdab95/view?usp=drive_link)
- **Dataset Link**: [Google Drive - Dataset](https://drive.google.com/drive/folders/1rlP31T042SLtQNhlomgoHJrpDu8cXCsY?usp=drive_link)
- **NedaSefandarmaz Google Drive**: [Google Drive](https://drive.google.com/drive/mobile/folders/1rtfq3zcwlIEamjakQAHJ3Wbvfui3rvlq?usp=drive_link)

### Data Augmentation

#### Function: `data_augment`

This function takes the directory of the original data and the output directory for storing the augmented data. It performs the following operations:

1. **Flipping**: Images are flipped using a random number generator.
2. **Rotations**: Images are rotated by 90, 180, and 270 degrees.

#### Steps:

1. **First Stage**: Flip 90 X-ray images to obtain 90 new images.
2. **Second Stage**: Rotate the original 90 images by 90 degrees to obtain 90 additional images.
3. **Third Stage**: Rotate the original images by 180 degrees to obtain another 90 images.
4. **Fourth Stage**: Rotate the original 90 images by 270 degrees to obtain 90 more images.

This results in a dataset consisting of 450 COVID-19 X-ray images.

### Data Preparation

1. **Rescaling**: Rescale the training and test data.
2. **Validation Data**: Create a subset of the training data (25%) and rescale.

### Model Architecture

A CNN architecture is used, consisting of 38 layers, including:

- **Convolutional Layers (Conv2D)** with a 3×3 kernel
- **Max Pooling** (2×2 size)
- **Dropout** (20% rate)
- **Batch Normalization** (along axis 1)
- **ReLU Activation Function**
- **Fully Connected Layers**

#### Output

- **Binary Classification**: Uses binary cross-entropy (BCE) loss function and sigmoid activation function.
- **Optimizer**: Adam optimizer with a learning rate of 0.006.

### Training

- **Epochs**: 50
- **Validation**: Use validation data generated in previous steps.

### Evaluation

1. **Loss and Accuracy Graphs**: Plot graphs for training and validation data.
2. **Model Comparison**: Evaluate models with 1, 2, 3, 4, and 5 convolutional layers using augmented data.

### Conclusion

The implemented network is trained and evaluated for binary classification tasks using augmented data. The performance is compared across different architectures.

### Written by:
  Neda Sefandarmaz
  n.sefandarmaz@gmail.com
  @Nedseeee

### References

- [Google Colab - Notebook Loading Error](https://stackoverflow.com/questions/59751151/google-colab-errors-notebook-loading-error)
- [Google Drive - View & Open Files](https://support.google.com/drive/answer/2423485?hl=en)
- [AWS - What is Data Augmentation?](https://aws.amazon.com/what-is/data-augmentation/)
- [GitHub - Illegal Code on Colab](https://github.com/TheLastBen/fast-stable-diffusion/issues/2013)
- [Google Drive - Download](https://www.google.com/drive/download/)
- [DataScientest - Data Augmentation](https://datascientest.com/en/data-augmentation-what-is-it-whats-it-for)
