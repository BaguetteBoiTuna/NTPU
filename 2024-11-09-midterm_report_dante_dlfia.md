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
