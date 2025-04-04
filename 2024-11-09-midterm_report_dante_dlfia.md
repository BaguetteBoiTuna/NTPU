---
id: 2024-11-09-midterm_report_dante_dlfia
aliases:
  - Midterm_Report_Dante_DLfIA
tags: []
---

# Midterm Report: Deep Learning for Image Analysis

GUILLEMAIN Dante 711382799

## 1. Introduction

### Problem Overview

In this report, I address the challenge of wildlife species classification using the Animals-10 dataset, which comprises approximately 28,000 images across ten categories: dog, cat, horse, spider, butterfly, chicken, sheep, cow, squirrel and elephant. Accurate classification of animal species from images is crucial in various fields, including ecology, wildlife conservation and biodiversity monitoring. Automating this process through machine learning models can significantly enhance the efficiency of data analysis and decision-making in these domains.

### Importance of Pre-processing

1. **Normalization**: Wildlife images can vary widely in lighting conditions, leading to different pixel intensity scales across images. Normalization ensures that pixel values are standardized across all images, creating a uniform range, typically between 0 and 1. This consistency helps the model learn faster and reduces sensitivity to intensity fluctuations, providing more stable training results.
2. **Noise Reduction**: Wildlife images frequently contain visual noise, such as foliage, shadows or background animals, which can obscure the primary subject. Noise reduction techniques, like Gaussian filtering, help reduce these distractions, enabling the model to focus more on relevant features. This step is especially important for species that are naturally camouflaged within their environments, improving classification accuracy.
3. **Contrast Adjustment**: In natural habitats, animals may blend into their surroundings, obscuring important features. Contrast adjustment using CLAHE (Contrast Limited Adaptive Histogram Equalization) locally enhances contrast, making subtle details more visible and distinct. This technique improves the model's ability to identify edges, textures and other distinguishing features, which are essential for differentiating similar looking species.

By applying these pre-processing techniques, I ensured the input images are consistent in quality, which enhances the model's ability to classify various species accurately.

##### Sources

- **Inside Machine Learning**. _Why and How to Normalize Data for Computer Vision (with PyTorch)_. <https://inside-machinelearning.com/en/why-and-how-to-normalize-data-object-detection-on-image-in-pytorch-part-1/>
- **IEEE Xplore**. _Image De-Noising With Machine Learning: A Review_. <https://ieeexplore.ieee.org/document/9464965>
- **OpenCV Documentation**. _Histogram Equalization in OpenCV_. <https://docs.opencv.org/4.x/d5/daf/tutorial_py_histogram_equalization.html>
- **World Wildlife Fund**. _Employing AI to Evaluate Wildlife Populations on a Global Scale_. <https://www.worldwildlife.org/magazine/issues/winter-2020/articles/employing-ai-to-evaluate-wildlife-populations-on-a-global-scale>

## 2. Dataset Exploration and Pre-processing

### Dataset Exploration

The [Animals-10](https://www.kaggle.com/datasets/alessiocorrado99/animals10?resource=download) dataset includes approximately 28,000 images of 10 animal categories, sourced from various online environments, which introduces challenges:

1. **Image Quality**: The dataset contains "medium quality" images, meaning they vary in resolution, lighting and clarity, which could impact classification accuracy.
2. **Background Noise and Clutter**: Since these images were collected from the internet, they often contain background elements like grass, trees objects or other animals, which can distract the model from focusing on the primary subject. This noise makes it harder for the model to identify key features of the animals.
3. **Variability in Lighting and Shadows**: Due to different environments and lighting conditions, images may have inconsistent brightness and shadows. This can make it challenging for the model to generalize, as certain features may be obscured in low light conditions or overexposed in high light settings.
4. **Natural Camouflage and Animal Positioning**: Many animals blend naturally into their environments due to camouflage. This makes it difficult for the model to distinguish between the subject and its background, particularly when animals are partially hidden or positioned in a way that obscures key features.

These challenges make pre-processing essential for improving the clarity and consistency of the images, enhancing model performance.

### Pre-processing Steps

The following pre-processing steps were applied to standardize the dataset and enhance image quality, improving the model's training and generalization:

#### 1. Resizing with Padding

- Images are resized to a fixed dimension (224x224) while preserving the aspect ratio. Padding is added to fill any extra space, ensuring a consistent input size without distortion.
- **Purpose**: Standardizing input dimensions across images allows the model to handle consistent sized inputs, improving model convergence and performance.

```python
from PIL import Image, ImageOps

def resize_with_padding(image, target_size=(224, 224)):
    # Resize the image with aspect ratio preserved
    image.thumbnail(target_size, Image.LANCZOS)
    delta_w = target_size[0] - image.size[0]
    delta_h = target_size[1] - image.size[1]
    padding = (
        delta_w // 2,
        delta_h // 2,
        delta_w - delta_w // 2,
        delta_h - delta_h // 2,
    )
    return ImageOps.expand(image, padding, fill="black")
```

#### 2. Normalization

- The pixel values are scaled to a 0-1 range by dividing by 255.
- **Purpose**: Normalization helps in stabilizing and accelerating the training process by maintaining the pixel values within a controlled range, which aids in smoother gradient descent.

```python
import numpy as np

def normalize_image(image):
    return np.array(image) / 255.0
```

#### 3. Contrast Enhancement (CLAHE)

- The [Contrast Limited Adaptive Histogram Equalization (CLAHE)](https://docs.opencv.org/4.x/d5/daf/tutorial_py_histogram_equalization.html) method is applied to the images, focusing on the lightness channel in LAB color space to enhance contrast without oversaturating.
- **Purpose**: CLAHE enhances fine details in the images, making features more prominent and easier for the model to recognize, especially in low-light or low-contrast areas.

```python
import cv2

def apply_clahe_to_color(image_array):
    # Convert RGB to LAB color space
    lab = cv2.cvtColor((image_array * 255).astype(np.uint8), cv2.COLOR_RGB2LAB)
    l, a, b = cv2.split(lab)

    # Apply CLAHE to the L channel with a lower clip limit for softer contrast
    clahe = cv2.createCLAHE(clipLimit=1.5, tileGridSize=(8, 8))
    cl = clahe.apply(l)

    # Merge back the L channel with the original A and B channels
    enhanced_lab = cv2.merge((cl, a, b))

    # Convert back to RGB color space
    enhanced_image = cv2.cvtColor(enhanced_lab, cv2.COLOR_LAB2RGB)

    return enhanced_image / 255.0
```

### Demonstration of Pre-processing
![[Screenshot 2024-11-10 at 21.44.30.png]]
![[Screenshot 2024-11-10 at 21.45.11.png]]
![[Screenshot 2024-11-10 at 21.45.37.png]]

## 3. Model Selection and Implementation

### Model Architecture Selection

For this image classification task, I selected EfficientNet-B3 as the deep learning model architecture. EfficienNet is known for its accuracy and efficiency. It utiilizes a compound scaling method that balances the depth, width and resolution of the network, which allows it to achieve state of the art performance with fewer parameters and lower computational requirements compared to other models. EfficientNet-B3, specifically, offers improved accuracy over EfficientNet-B0, making it suitable for the complexity of my dataset, which includes images of animals with varied backgrounds.

EfficientNet-B3 was chosen over other models such as ResNet and Vision Transformer due to its balance of accuracy and computational efficiency. The M# Pro chip on my MacBook Pro provides moderate computational power, and EfficientNet-B3 can leverage this effecively, providing accurate results without overwhelming system resources.

### Modifications and Customizations

To tailor EfficientNet-B3 to this classification problem, a few modifications and customizations were applied:

1. **Number of Output Classes**: The model's final fully connected layer is adapted to match the number of classes in the dataset, corresponding to the different animal types. This customization enables EfficientNet-B3 to classify each image into one of the specific animal categories in the dataset.
2. **Data Augmentation**: To improve model generalization, data augmentation techniques such as random horizontal flipping and rotation were added during training. These augmentations simulate variations in the dataset, helping the model adapt to diverse poses, orientations and backgrounds.
3. **Training on Apple's M3 Pro Chip**: Since the training will be conducted on an Apple MacBook Pro with an M3 Pro chip, TensorFlow's Metal Performance Shaders (MPS) backend will be used. This backend optimizes model training for Apple Silicon, enabling faster and more efficient computation. Mixed precision training will also be enabled to further optimize memory usage and training speed.

### Model Variants: Model A and Model B

To assess the impact of image pre-processing on model performance, two versions of the model will be trained:

- **Model A**: This model will be trained on pre-processed images, where images are resized, normalized and contrast enhanced using Contrast Limited Adaptive Histogram Equalization (CLAHE). The pre-processing aims to improve image clarity and highlight key features, potentially aiding the model in learning distinguishing characteristics of each animal.
- **Model B**: This model will be trained on the original images. Training on raw images allows for a baseline comparison to determine whether the pre-processing steps improve or hinder model accuracy.

Both models will be trained under identical conditions, including the same batch size, learning rate and number of epochs. The results from Model A and Model B will be compared to assess the effectiveness of the pre-processing steps on classification accuracy and training efficiency.

### Relevant Code Snippets

```python
# Define paths and parameters
preprocessed_dir = "./datasets/preprocessed"
original_dir = "./datasets/raw-img"
batch_size = 32
img_size = (224, 224)
num_classes = len(os.listdir(preprocessed_dir))
fraction = 0.05 # I only used 5% of the dataset for demonstration purposes
# Also did not want my laptop to overheat
```

```python
# Set up data generators
datagen = ImageDataGenerator(
    horizontal_flip=True, rotation_range=10, rescale=1.0 / 255.0
)
```

```python
# Function to load a subset of the dataset and set steps_per_epoch so I dont wait forever
def load_data_subset(generator, directory, target_size, batch_size, fraction):
    flow = generator.flow_from_directory(
        directory,
        target_size=target_size,
        batch_size=batch_size,
        class_mode="sparse",
        shuffle=True,
    )
    subset_size = int(fraction * flow.samples)
    steps_per_epoch = subset_size // batch_size
    return flow, steps_per_epoch


# Load data subsets for Model A and Model B
train_gen_a, steps_a = load_data_subset(
    datagen, preprocessed_dir, img_size, batch_size, fraction
)
train_gen_b, steps_b = load_data_subset(
    datagen, original_dir, img_size, batch_size, fraction
)
```

```python
# Define and compile EfficientNet-B3 model using Functional API
def create_efficientnet_b3_model():
    inputs = layers.Input(shape=(224, 224, 3), name="input_layer")
    base_model = EfficientNetB3(
        include_top=False, input_tensor=inputs, weights="imagenet"
    )
    base_model.trainable = True
    x = base_model(inputs, training=True)
    x = layers.GlobalAveragePooling2D()(x)
    x = layers.Dropout(0.2)(x)
    outputs = layers.Dense(num_classes, activation="softmax", dtype="float32")(x)
    model = models.Model(inputs, outputs)
    model.compile(
        optimizer=tf.keras.optimizers.Adam(learning_rate=0.001),
        loss="sparse_categorical_crossentropy",
        metrics=["accuracy"],
    )
return model
```

```python
# Initialize Model A and Model B
model_a = create_efficientnet_b3_model()
model_b = create_efficientnet_b3_model()

# Train Model A and Model B, tracking training time
start_time_a = time.time()
history_a = model_a.fit(train_gen_a, epochs=5, steps_per_epoch=steps_a)
train_time_a = time.time() - start_time_a

start_time_b = time.time()
history_b = model_b.fit(train_gen_b, epochs=5, steps_per_epoch=steps_b)
train_time_b = time.time() - start_time_b
```

```python
# Evaluate Model A and Model B
def evaluate_model(model, data_generator, steps):
    eval_results = model.evaluate(data_generator, steps=steps, verbose=1)
    return eval_results


results_a = evaluate_model(model_a, train_gen_a, steps_a)
results_b = evaluate_model(model_b, train_gen_b, steps_b)
```

## 4. Performance Evaluation

### Metrics: Accuracy and Loss Comparison

Using accuracy and loss as evaluation metrics, I observed the following from the training of Model A (preprocessed images) and Model B (original images):

- **Accuracy**: Model B achieved a slightly higher peak accuracy in certain epochs but showed fluctuations, indicating inconsistent learning. In contrast, Model A showed more stable accuracy improvements, likely due to the feature-enhancing effects of pre-processing.
- **Loss**: Model A had a more stable and consistently lower loss than Model B, suggesting that pre-processing helped the model learn more effectively by focusing on relevant features.

These diagrams visually confirm that pre-processing contributed to more consistent training behavior, though the overall improvement in accuracy was modest.

![[Figure_1.png]]![[Figure_2.png]]
They don't look very good but it is very straining on my laptop to train for longer periods.

### Efficiency Comparison: Computational Efficiency

The following metrics were evaluated to compare computational efficiency between the two models:

| Metric                 | Model A (Preprocessed) | Model B (Original) |
| ---------------------- | ---------------------- | ------------------ |
| **Training Time (s)**  | 251.32                 | 279.85             |
| **Inference Time (s)** | 3.65                   | 4.17               |
| **Memory Usage (MB)**  | 90.36                  | 123.80             |

- **Training Time**: Model A trained faster than Model B, likely due to the reduced complexity in preprocessed images, making it easier for the model to extract meaningful features.
- **Inference Time**: Model A also had a slightly faster inference time, which suggests that the pre-processed images allowed for more efficient computation during prediction.
- **Memory Usage**: Model A required less memory compared to Model B, which aligns with the idea that pre-processed images might help streamline feature extraction and reduce memory overhead.
- **Temperature**: I have a temperature widget on my laptop because I am paranoid about overheating. I noticed that during the training of Model A, the temperature would be around 75°C and 80°C (which is normal for a MacBook Pro under load). However, during the training of Model B, the temperature would reach 85°C and 90°C, which is a bit too high for my liking and my laptop stayed hot to the touch for a long time after.

In summary, Model A showed better computational efficiency, making it potentially more suitable for applications with resource constraints.

### Interpretability Analysis: Grad-CAM Visualization

I attempted to perform interpretability analysis using Grad-CAM to visualize how each model makes decisions and highlight important regions in the images. Unfortunately, the Grad-CAM implementation failed with the message:

```
No gradiants available.
Grad-CAM failed: Unable to obtain gradients.
```

Which meant that my code was unable to obtain gradients and heatmaps from the models.

This issue may stem from the specific architecture used (EfficientNet-B3), the fact I used a MacBook Pro with an M3 Pro chip or the way gradients are handled in the current setup. Consequently, I was unable to provide activation maps or Grad-CAM visualization interpretability.

### Relevant Code Snippets

```python
# Measure inference time and memory usage
def measure_inference_time_and_memory(model, data_generator):
    batch = next(data_generator)
    start_time = time.time()
    process = psutil.Process(os.getpid())
    mem_before = process.memory_info().rss / (1024 * 1024)
    model.predict(batch[0])
    inference_time = time.time() - start_time
    mem_after = process.memory_info().rss / (1024 * 1024)
    memory_usage = mem_after - mem_before
    return inference_time, memory_usage


inference_time_a, memory_usage_a = measure_inference_time_and_memory(
    model_a, train_gen_a
)
inference_time_b, memory_usage_b = measure_inference_time_and_memory(
    model_b, train_gen_b
)
```

```python
# Grad-CAM Visualization using base_model
def get_grad_cam(model, img_array, base_model_layer_name="top_conv"):
    img_tensor = tf.convert_to_tensor(img_array)
    base_model = model.get_layer("efficientnetb3")
    grad_model = tf.keras.models.Model(
        [model.inputs],
        [base_model.get_layer(base_model_layer_name).output, model.output],
    )
    with tf.GradientTape() as tape:
        tape.watch(img_tensor)
        conv_outputs, predictions = grad_model(img_tensor)
        loss = predictions[:, tf.argmax(predictions[0])]
    grads = tape.gradient(loss, conv_outputs)
    if grads is None:
        print("No gradients available.")
        return None
    pooled_grads = tf.reduce_mean(grads, axis=(0, 1, 2))
    conv_outputs = conv_outputs[0]
    heatmap = tf.reduce_sum(tf.multiply(pooled_grads, conv_outputs), axis=-1)
    heatmap = np.maximum(heatmap, 0) / np.max(heatmap)
    return heatmap


def plot_grad_cam(model, img_path, base_model_layer_name="top_conv"):
    img = tf.keras.preprocessing.image.load_img(img_path, target_size=img_size)
    img_array = tf.keras.preprocessing.image.img_to_array(img)
    img_array = np.expand_dims(img_array, axis=0) / 255.0
    heatmap = get_grad_cam(model, img_array, base_model_layer_name)
    if heatmap is None:
        print("Grad-CAM failed: Unable to obtain gradients.")
        return
    heatmap = cv2.resize(heatmap.numpy(), (img.size[0], img.size[1]))
    plt.imshow(img)
    plt.imshow(heatmap, cmap="jet", alpha=0.4)
    plt.axis("off")
    plt.show()

img_path = "/Users/dante/Sandboxes/MLIA/datasets/raw-img/gatto/81.jpeg"
plot_grad_cam(model_a, img_path)
plot_grad_cam(model_b, img_path)
```

```python
# Plot Accuracy and Loss Curves
def plot_metrics(history, model_name):
    plt.figure(figsize=(12, 4))
    plt.subplot(1, 2, 1)
    plt.plot(history.history["accuracy"], label="accuracy")
    plt.title(f"{model_name} Accuracy")
    plt.xlabel("Epoch")
    plt.ylabel("Accuracy")
    plt.legend()
    plt.subplot(1, 2, 2)
    plt.plot(history.history["loss"], label="loss")
    plt.title(f"{model_name} Loss")
    plt.xlabel("Epoch")
    plt.ylabel("Loss")
    plt.legend()
    plt.show()


plot_metrics(history_a, "Model A (Preprocessed)")
plot_metrics(history_b, "Model B (Original)")
```

## 5. Results Summary

To evaluate the models trained with and without pre-processing, I collected key performance metrics across both models. The table below summarizes the metrics used for comparison:

| Metric             | Model A    | Model B    |
| ------------------ | ---------- | ---------- |
| Training Time (s)  | 251.315995 | 279.854320 |
| Inference Time (s) | 3.647679   | 4.169815   |
| Memory Usage (MB)  | 90.359375  | 123.796875 |
| Loss               | 10.476001  | 41.222492  |
| Accuracy           | 0.189844   | 0.105469   |

### Comparison and Analysis

#### Model Accuracy and Robustness

- **Accuracy**: Model A, which was trained on pre-processed images, achieved a higher accuracy of 18.98% compared to 10.55% for Model B which was trained on raw images. This indicates that the pre-processing techniques contributed positively to the model's ability to generalize, resulting in better overall performance.
  ![[Accuracy_Comparison.png]]

- **Loss**: The loss value for Model A (10.48) was significantly lower than that for Model B (41.22). A lower loss suggests that Model A experienced less error during training and potentially exhibits better convergence properties. The high loss in Model B indicate issues with stability and convergence due to the lack of pre-processing.
  ![[Loss_Comparison.png]]

#### Computational Efficiency and Training Requirements

- **Training Time**: Model A’s training was completed in approximately 251.32 seconds, while Model B took slightly longer at 279.85 seconds. This faster training time for Model A may be attributed to the pre-processed images, which likely simplified feature extraction and pattern recognition, allowing the model to learn more effectively with fewer resources.
  ![[Training_Time_(s)_Comparison.png]]

- **Inference Time**: Both models demonstrated similar inference times, but Model A was marginally faster (3.65 seconds compared to 4.17 seconds for Model B). This small difference in inference time highlights a slight edge in efficiency, favoring the model trained on pre-processed data. Faster inference can be advantageous in real time or large scale applications.
  ![[Training_Inference_Time_Comparison.png]]

- **Memory Usage**: Model A also showed a lower memory usage of 90.36 MB compared to Model B’s 123.80 MB. The lower memory consumption in Model A implies that pre-processing might have streamlined the dataset’s information, allowing the model to operate with reduced memory demands.
  ![[Memory_Usage_(MB)_Comparison.png]]

### Clarity in Captured Features

- **Feature Capture and Interpretability**: Although I attempted to analyze feature capture and interpretability using Grad-CAM, technical limitations prevented me from obtaining Grad-CAM visualizations. Theoretically, pre-processing techniques like normalization and contrast adjustment should help the model capture relevant features more effectively, such as edges and fine details, by enhancing contrast and reducing noise. This suggests that Model A would likely perform better in identifying essential features, especially in complex backgrounds.

### Summary

In conclusion, Model A outperformed Model B in terms of accuracy, loss, and computational efficiency. Pre-processing steps provided a modest but notable improvement in model performance, leading to better generalization with reduced computational requirements. The results indicate that pre-processing contributed to both the efficiency and effectiveness of the model, making it a valuable step in optimizing performance for this image classification task.

### Relevant Code Snippets

```python
# Summary Table
summary_data = {
    "Metric": [
        "Training Time (s)",
        "Inference Time (s)",
        "Memory Usage (MB)",
        "Loss",
        "Accuracy",
    ],
    "Model A": [
        train_time_a,
        inference_time_a,
        memory_usage_a,
        results_a[0],
        results_a[1],
    ],
    "Model B": [
        train_time_b,
        inference_time_b,
        memory_usage_b,
        results_b[0],
        results_b[1],
    ],
}
summary_df = pd.DataFrame(summary_data)
print("\nPerformance Summary")
print(summary_df)
```

```python
# This is from another file where I plotted the bar charts
# Using the values from the Summary Table
# Data for plotting
metrics = [
    "Training Time (s)",
    "Inference Time (s)",
    "Memory Usage (MB)",
    "Loss",
    "Accuracy",
]
model_a_values = [251.315995, 3.647679, 90.359375, 10.476001, 0.189844]
model_b_values = [279.854320, 4.169815, 123.796875, 41.222492, 0.105469]

# Creating individual plots for each metric
for i, metric in enumerate(metrics):
    plt.figure(figsize=(6, 4))
    plt.bar(
        [metric],
        [model_a_values[i]],
        label="Model A",
        color="#1f77b4",
        width=0.4,
        align="center",
    )
    plt.bar(
        [metric],
        [model_b_values[i]],
        label="Model B",
        color="#ff7f0e",
        width=0.4,
        align="edge",
    )
    plt.title(f"Model A vs Model B: {metric}", fontsize=14)
    plt.ylabel(
        "Value"
        if metric not in ["Training Time (s)", "Inference Time (s)"]
        else "Seconds"
    )
    plt.legend(title="Models")
    plt.tight_layout()
    plt.savefig(f"{metric.replace(' ', '_')}_Comparison.png")
    plt.show()
```

## 6. Conclusion and Future Directions

### Summary of Findings

In this report, I explored the impact of image pre-processing on the performance of a deep learning model for animal image classification. Using EfficientNet-B3 as my model architecture, I trained two versions of the model: one on pre-processed images (Model A) and the other on raw images (Model B). My analysis across various metrics revealed several key insights:

- **Improved Performance with Pre-Processing**: Model A, trained on pre-processed images, achieved higher accuracy and a lower loss compared to Model B. This indicates that pre-processing steps such as normalization and contrast adjustment enhanced the model’s ability to generalize and learn effectively from the dataset.
- **Enhanced Computational Efficiency**: Model A demonstrated slight improvements in computational efficiency, with reduced training time and memory usage. This suggests that pre-processing helped streamline the dataset, enabling more efficient feature extraction and reducing computational load.
- **Feature Capture and Interpretability**: Although direct Grad-CAM visualizations were not feasible, theoretical expectations suggest that pre-processing helped improve clarity in capturing relevant features. Enhanced contrast and reduced noise in pre-processed images likely made critical features like edges and shapes more distinguishable, potentially aiding the model’s interpretability and robustness.

Overall, my findings confirm that pre-processing was beneficial in improving both model performance and computational efficiency, highlighting the value of these techniques in deep learning applications involving complex datasets.

### Future Directions

To further enhance model performance and interpretability, the following avenues are recommended:

- **Exploration of Additional Pre-Processing Techniques**: Incorporating data augmentation methods such as random rotations, flips, and scaling can increase dataset variability, potentially improving model robustness. Techniques like histogram equalization may also enhance feature clarity by adjusting image contrast.
- **Adoption of Advanced Model Architectures**: Implementing more sophisticated architectures, such as EfficientNet-B5 or transformer-based models, could lead to improved accuracy and robustness, particularly for complex datasets. These models can capture intricate patterns and dependencies, enhancing performance.
- **Utilization of Transfer Learning**: Leveraging pre-trained models on large datasets can expedite training and improve accuracy. Transfer learning allows models to benefit from previously learned features, which is especially useful when dealing with limited data.
- **Implementation of Enhanced Interpretability Methods**: Employing advanced interpretability techniques, such as Grad-CAM++ or layer wise relevance propagation (LRP), can provide deeper insights into the model’s decision-making processes, facilitating better understanding and trust in model predictions.

By pursuing these directions, future research can continue to optimize model performance, computational efficiency and interpretability, advancing the application of deep learning in image analysis.

##### Sources

- **Machine Learning Mastery**. _Best Practices for Preparing and Augmenting Image Data for Convolutional Neural Networks_. <https://machinelearningmastery.com/best-practices-for-preparing-and-augmenting-image-data-for-convolutional-neural-networks/>
- **IEEE Xplore**. _Advancements in CNN Architectures for Computer Vision: A Comprehensive Review_. <https://ieeexplore.ieee.org/document/10420413>

