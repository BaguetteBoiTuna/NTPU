---
id: 2024-11-09-midterm_report_dante_dlfia
aliases:
  - Midterm_Report_Dante_DLfIA
tags: []
---

# Midterm Report: Deep Learning for Image Analysis

GUILLEMAIN Dante 711382799

## Introduction

### Problem Overview

In this report, we address the challenge of wildlife species classification using the Animals-10 dataset, which comprises approximately 28,000 images across ten categories: dog, cat, horse, spider, butterfly, chicken, sheep, cow, squirrel and elephant. Accurate classification of animal species from images is crucial in various fields, including ecology, wildlife conservation and biodiversity monitoring. Automating this process through machine learning models can significantly enhance the efficiency of data analysis and decision-making in these domains.

### Importance of Pre-processing

1. **Normalization**: Wildlife images can vary widely in lighting conditions, leading to different pixel intensity scales across images. Normalization ensures that pixel values are standardized across all images, creating a uniform range, typically between 0 and 1. This consistency helps the model learn faster and reduces sensitivity to intensity fluctuations, providing more stable training results.
2. **Noise Reduction**: Wildlife images frequently contain visual noise, such as foliage, shadows or background animals, which can obscure the primary subject. Noise reduction techniques, like Gaussian filtering, help reduce these distractions, enabling the model to focus more on relevant features. This step is especially important for species that are naturally camouflaged within their environments, improving classification accuracy.
3. **Contrast Adjustment**: In natural habitats, animals may blend into their surroundings, obscuring important features. Contrast adjustment using CLAHE (Contrast Limited Adaptive Histogram Equalization) locally enhances contrast, making subtle details more visible and distinct. This technique improves the model's ability to identify edges, textures and other distinguishing features, which are essential for differentiating similar looking species.

By applying these pre-processing techniques, we ensure the input images are consistent in quality, which enhances the model's ability to classify various species accurately.

##### Sources

- **Inside Machine Learning**. _Why and How to Normalize Data for Computer Vision (with PyTorch)_. <https://inside-machinelearning.com/en/why-and-how-to-normalize-data-object-detection-on-image-in-pytorch-part-1/>
- **IEEE Xplore**. _Image De-Noising With Machine Learning: A Review_. <https://ieeexplore.ieee.org/document/9464965>
- **OpenCV Documentation**. _Histogram Equalization in OpenCV_. <https://docs.opencv.org/4.x/d5/daf/tutorial_py_histogram_equalization.html>
- **World Wildlife Fund**. _Employing AI to Evaluate Wildlife Populations on a Global Scale_. <https://www.worldwildlife.org/magazine/issues/winter-2020/articles/employing-ai-to-evaluate-wildlife-populations-on-a-global-scale>
