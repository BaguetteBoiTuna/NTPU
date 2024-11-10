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

#### 4. Contrast Adjustment

Enhancing contrast can make features more distinguishable. Using Contrast Limited Adaptive Histogram Equalization (CLAHE) is effective for this purpose.

```python
import cv2
import numpy as np

def enhance_contrast(image):
    image_array = np.array(image)
    # Convert to LAB color space
    lab = cv2.cvtColor(image_array, cv2.COLOR_RGB2LAB)
    l, a, b = cv2.split(lab)
    # Apply CLAHE to the L-channel
    clahe = cv2.createCLAHE(clipLimit=2.0, tileGridSize=(8, 8))
    cl = clahe.apply(l)
    # Merge channels and convert back to RGB
    merged_lab = cv2.merge((cl, a, b))
    enhanced_image = cv2.cvtColor(merged_lab, cv2.COLOR_LAB2RGB)
    # Convert back to PIL image
    enhanced_image_pil = Image.fromarray(enhanced_image)
    return enhanced_image_pil
```

DIFFERENCE BETWEEN ORIGINAL AND PRE-PROCESSED IMAGES WILL GO HERE

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

| Metric             | Model A    | Model B    |
| ------------------ | ---------- | ---------- |
| Training Time (s)  | 251.315995 | 279.854320 |
| Inference Time (s) | 3.647679   | 4.169815   |
| Memory Usage (MB)  | 90.359375  | 123.796875 |
| Loss               | 10.476001  | 41.222492  |
| Accuracy           | 0.189844   | 0.105469   |
