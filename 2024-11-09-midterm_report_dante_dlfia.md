---
id: 2024-11-09-midterm_report_dante_dlfia
aliases:
  - Midterm_Report_Dante_DLfIA
tags: []
---

# Midterm Report: Deep Learning for Image Analysis

GUILLEMAIN Dante 711382799

## Introduction

This project focuses on handwritten digit recognition, a foundational problem in image analysis that has practical applications in areas such as automated postal sorting, bank check precessing and document digitization. The objective is to classify handwritten digits using machine learning models, specifically leveraging deep learning for high accuracy and efficiency. In this project, like the 2nd assignment, we will be using the MNIST dataset, which is a benchmark for digit classification containing 70,000 images of handwritten digits from 0 to 9.

For the MNIST dataset, while it is relatively clean and standardized, 28x28 grayscale images with centered digits, applying certain pre-processing techniques can still improve model performance. Here's why pre-processing techniques can be beneficial even for a dataset like MNIST:

- **Normalization**: MNIST images have pixel values that range from 0 to 255. Normalizing these values to a range of 0 to 1 allows the neural network to process inputs more efficiently and stabilize the learning process. This leads to faster convergence during training, as neural networks perform better with inputs on a consistent scale.
- **Data Augmentation**: Although MNIST digits are centered, in real world applications, handwritten digits may vary in position, rotation, or size. By augmenting the data with slight rotations, shifts, or scaling, we can simulate these variations, making the model more robust.
- **Contrast Adjustment and Noise Reduction**: While MNIST images are clean, contrast enhancement can improve digit visibility, particularly for faint strokes that might otherwise be misinterpreted. Noise reduction isn't strictly necessary for MNIST but can still aid in removing subtle inconsistencies, further refining feature clarity for more precise recognition.

While MNIST is well prepared, pre-processing still enhances the model's robustness and generalization, leading to measurable imrovements in performance and efficiency even for an "easy" dataset like MNIST.

##### Sources

- **LeCun**, Y. (n.d.). The MNIST Database of Handwritten Digits. Retrieved from <https://yann.lecun.com/exdb/mnist/>

- **GeeksforGeeks**. (n.d.). MNIST Dataset. Retrieved from <https://www.geeksforgeeks.org/mnist-dataset/>

## Dataset Exploration and Pre-processing

### Dataset Analysis

The MNIST dataset consists of 70,000 grayscale images of handwritten digits 0 to 9, divided into 60,000 training images and 10,000 test images. Each image is standardized to a 28x28 pixel resolution, which maintains a consistent image quality across samples. The dataset has a balanced class distribution, with roughly equal representation of each digit, which help mitigate class imbalance issues that can bias the model.

#### Challenges in the MNIST Dataset

- **Intra-Class Variability**: Different handwriting styles lead to signifiant variations in how the same digit is written, introducing complexity in classification.
- **Inter-Class Similarity**: Certain digits, such as 1 and 7 or 3 and 8, can appear similar, making it challenging for models to distinguish between them.
- **Noise and Artifacts**: Despite being relatively clean, some images contain noise or artifacts that can affect model performance.
- **Limited Resolution**: The 28x28 pixel size may not capture fine details, potentially reducing the model's ability to discern subtle differences between digits.
