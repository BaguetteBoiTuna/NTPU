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

## Dataset Exploration and Pre-processing

### Dataset Exploration

The [Animals-10](https://www.kaggle.com/datasets/alessiocorrado99/animals10?resource=download) dataset includes approximately 28,000 images of 10 animal categories, sourced from various online environments, which introduces challenges:

1. **Image Quality**: The dataset contains "medium quality" images, meaning they vary in resolution, lighting and clarity, which could impact classification accuracy.
2. **Background Noise and Clutter**: Since these images were collected from the internet, they often contain background elements like grass, trees objects or other animals, which can distract the model from focusing on the primary subject. This noise makes it harder for the model to identify key features of the animals.
3. **Variability in Lighting and Shadows**: Due to different environments and lighting conditions, images may have inconsistent brightness and shadows. This can make it challenging for the model to generalize, as certain features may be obscured in low light conditions or overexposed in high light settings.
4. **Natural Camouflage and Animal Positioning**: Many animals blend naturally into their environments due to camouflage. This makes it difficult for the model to distinguish between the subject and its background, particularly when animals are partially hidden or positioned in a way that obscures key features.

These challenges make pre-processing essential for improving the clarity and consistency of the images, enhancing model performance.

### Pre-processing Steps

All the code snippets shown in this section are for demonstration purposes only and will be changed according to the actual implementation requirements.

#### 1. Resizing with Aspect Ratio Preservation and Padding

To resize images to a uniform size without distorting their aspect ratios, we can add padding after resizing. This method maintains the original aspect ratio and fills the remaining space with a solid color.

Here's how to implement this using [Pillow](https://pillow.readthedocs.io/en/stable/):

```python
from PIL import Image, ImageOps

def resize_with_padding(image_path, target_size=(128, 128), padding_color=(0, 0, 0)):
    image = Image.open(image_path)

    # Calculate the aspect ratio
    aspect_ratio = image.width / image.height

    # Determine new dimensions to fit within the target size
    if aspect_ratio > 1:  # Wider than tall
        new_width = target_size[0]
        new_height = int(new_width / aspect_ratio)
    else:  # Taller than wide
        new_height = target_size[1]
        new_width = int(new_height * aspect_ratio)

    # Resize the image while maintaining aspect ratio
    resized_image = image.resize((new_width, new_height), Image.ANTIALIAS)

    # Create a new image with the target size and padding color
    new_image = Image.new("RGB", target_size, padding_color)

    # Paste the resized image onto the center of the new image
    paste_position = ((target_size[0] - new_width) // 2, (target_size[1] - new_height) // 2)
    new_image.paste(resized_image, paste_position)

    return new_image
```

#### 2. Normalization

Normalization scales pixel values to a range of 0 to 1, which helps stabilize and speed up the training process.

```python
import numpy as np

def normalize_image(image):
    image_array = np.array(image)
    normalized_array = image_array / 255.0
    return normalized_array
```

#### 3. Noise Reduction

Applying a Gaussian blur can help reduce minor noise in the images.

```python
from PIL import ImageFilter

def reduce_noise(image):
    blurred_image = image.filter(ImageFilter.GaussianBlur(radius=1))
    return blurred_image
```
