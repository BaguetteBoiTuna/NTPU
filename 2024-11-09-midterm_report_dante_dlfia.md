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

1. **Normalization**: MNIST images have pixel values that range from 0 to 255. Normalizing these values to a range of 0 to 1 allows the neural network to process inputs more efficiently and stabilize the learning process. This leads to faster convergence during training, as neural networks perform better with inputs on a consistent scale.
2. **Data Augmentation**: Although MNIST digits are centered, in real world applications, handwritten digits may vary in position, rotation, or size. By augmenting the data with slight rotations, shifts, or scaling, we can simulate these variations, making the model more robust.
3. **Contrast Adjustment and Noise Reduction**: While MNIST images are clean, contrast enhancement can improve digit visibility, particularly for faint strokes that might otherwise be misinterpreted. Noise reduction isn't strictly necessary for MNIST but can still aid in removing subtle inconsistencies, further refining feature clarity for more precise recognition.

While MNIST is well prepared, pre-processing still enhances the model's robustness and generalization, leading to measurable imrovements in performance and efficiency even for an "easy" dataset like MNIST.

##### Sources

- **LeCun**, Y. (n.d.). The MNIST Database of Handwritten Digits. Retrieved from <https://yann.lecun.com/exdb/mnist/>

- **GeeksforGeeks**. (n.d.). MNIST Dataset. Retrieved from <https://www.geeksforgeeks.org/mnist-dataset/>
