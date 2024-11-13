---
id: 2024-11-13-last_details_dlfia
aliases:
  - Last_Details_DLfIA
tags: []
---

# Last_Details_DLfIA

## Topics Covered

- Revisiting image processing
- Image sensing and acquisition
- Digital image acquisition
- Image sampling and Quantization
- Representing digital image
- Spatial and intensity image resolution

---

## Revisiting image processing

![[Tldraw Image.png]]

---

## Image sensing and acquisition

Many of the images we study or analyze are produced through the interplay of an "illumination" source and the "reflection" or absorption of energy from this source by the elements comprising the "scene" under observation.

The illumination source can vary and may include electromagnetic energy sources like radar, infrared, X-ray systems, ultrasound or even computer generated illumination patterns.

---

## Digital image acquisition

Physical Devices -> Image Sensors -> Digitizer/Film roll

---

## Image sampling and Quantization

In Digital Image Processing, signals captured from the physical world need to be translated into digital form through the process called Digitization. To make an image function f(x, y) suitable for digital processing, it must be digitized both spatially and in amplitude. This digitization process involves those steps:
Analog image -> Sampling -> Quantization -> Digital Image

1. **Analog Image**: An analog image is a continuous representation of an image, typically in the form of light or other electromagnetic waves, such as those captured by traditional film cameras. Analog images vary smoothly without discrete steps or interruptions, meaning they are theoretically infinite levels of detail and are not represented by discrete pixels.
2. **Sampling**: Sampling is the process of converting an analog image into a digital format by capturing a finite number of points from the continuous image. This is done by dividing the image into a grid and measure the intensity (color or brightness) at each point on the grid. The density of these sampling points affects the resolution of the resulting digital image: higher sampling rates capture more details and yield higher resolution images.
3. **Quantization**: Quantization is the process that follows sampling, where each sampled point's continuous intensity value is mapped to a finite set of discrete levels. In digital imaging, this often means assigning each sampled point a specific color or grayscale value, represented in binary. The number of quantization levels (e.g., 256 for an 8-bit grayscale image) determines the depth of detail in brightness or color that the image can represent.
4. **Digital Image:** A digital image is the result of the sampling and quantization processes. It is a discrete representation of the original analog image, stored as a grid of pixels where each pixel has a specific intensity or color value. Digital images can be displayed, processed and stored on digital devices like computers and are commonly represented in file formats like JPEG, PNG or BMP.

---

## Representing digital images

Digital images are represented through a function, \( f(x, y) \), where \( x \) and \( y \) define spatial locations within the image. This function assigns each point (or pixel) a specific intensity or color value, forming a structured grid that represents the image in digital form.

The spatial axes, \( x \) (horizontal) and \( y \) (vertical), mark the position of each pixel. The function \( f(x, y) \) indicates how intensity or color varies across these positions, allowing each \( (x, y) \) coordinate in the digital grid to match a pixel on a display or printed output. The pixel values indicate the color or brightness at each location, creating an accurate digital representation that can be stored, processed, and displayed effectively.

---

## Representing digital images in a matrix

In digital image processing, images are often represented as matrices, where each element in the matrix corresponds to a pixel in the image. This matrix structure allows for efficient storage and manipulation of images using mathematical operations.

### 1. Grayscale Image Matrix

For a grayscale image, each pixel has a single intensity value, representing shades from black to white. The image is represented as a 2D matrix, where each element \( M\_{i,j} \) corresponds to the intensity at position \( (i, j) \) in the image.

For example, a grayscale matrix could look like this:

$$
\begin{bmatrix}
0 & 50 & 100 \\
150 & 200 & 255 \\
\end{bmatrix}
$$

Here, the values range from 0 (black) to 255 (white) for an 8-bit grayscale image.

### 2. Color Image Matrix (RGB)

Color images are represented by combining three matrices, one for each color channel: Red, Green, and Blue (RGB). Each pixel has three intensity values, forming a 3D matrix where each channel matrix represents the intensity values for that color.

For example:

- **Red Channel**:
  $$
  \begin{bmatrix}
  255 & 0 & 0 \\
  128 & 0 & 0 \\
  \end{bmatrix}
  $$
- **Green Channel**:
  $$
  \begin{bmatrix}
  0 & 255 & 0 \\
  0 & 128 & 0 \\
  \end{bmatrix}
  $$
- **Blue Channel**:
  $$
  \begin{bmatrix}
  0 & 0 & 255 \\
  0 & 0 & 128 \\
  \end{bmatrix}
  $$

Each pixel’s RGB values combine to create the final color image.

### 3. Matrix Dimensions and Image Resolution

The dimensions of the matrix correspond to the resolution of the image. For example, a 1920x1080 image has a 1920x1080 matrix for grayscale or three 1920x1080 matrices for RGB color images. Higher resolution images have larger matrices, requiring more storage and processing power.

### 4. Advantages of Matrix Representation

- **Manipulation**: Matrix operations (e.g., filtering, transformation) can be applied to modify images efficiently.
- **Storage and Compression**: Matrix formats allow images to be compressed and stored effectively.
- **Computational Efficiency**: Algorithms can leverage matrix operations for fast processing.

---

## Dynamic intensity range

In digital imaging, **Dynamic Intensity Range** (also called **dynamic range**) refers to the range of intensity values an imaging system can represent, from the darkest (minimum intensity) to the brightest (maximum intensity) parts of an image. This range determines how well an image can capture contrast, detail, and tonal variations.

### 1. Definition and Calculation

The dynamic intensity range of an image can be defined as the ratio between the maximum and minimum intensity values that the system can capture:

$$
\text{Dynamic Range} = \frac{I_{\text{max}}}{I_{\text{min}}}
$$

Where:

- \( I \) (maximum intensity) represents the highest intensity level.
- \( I \) (minimum intensity) represents the lowest non-zero intensity level.

### 2. Bit Depth and Dynamic Range

In digital images, the **bit depth** of each pixel affects the dynamic range. Bit depth defines the number of discrete intensity levels that each pixel can represent. Common bit depths include:

- **8-bit**: Can represent 256 intensity levels, giving a dynamic range ratio of up to \( 255:1 \).
- **16-bit**: Can represent 65,536 intensity levels, giving a much higher dynamic range.

The higher the bit depth, the more levels of intensity can be represented, and thus, the greater the dynamic range.

### 3. Importance of Dynamic Intensity Range

A higher dynamic range allows for:

- **Greater Detail in Shadows and Highlights**: With more intensity levels, subtle details in dark and bright areas are preserved.
- **Better Contrast Representation**: The full range of intensities from dark to light can be accurately depicted, enhancing the perceived contrast of the image.
- **Improved Realism**: A high dynamic range can capture more lifelike images, especially in high-contrast scenes.

### 4. Example: Calculating Dynamic Range

For an 8-bit image, if the minimum intensity value is 1 and the maximum intensity value is 255, the dynamic range is calculated as:

$$
\text{Dynamic Range} = \frac{255}{1} = 255:1
$$

This means the system can distinguish between 255 different intensity levels, from darkest to brightest.

For a 16-bit image:

$$
\text{Dynamic Range} = \frac{65535}{1} = 65535:1
$$

This much larger range allows for far more tonal detail.

### 5. Dynamic Range in High Dynamic Range (HDR) Imaging

**HDR Imaging** is a technique that uses a higher dynamic range to capture and display images with greater contrast. HDR systems capture multiple exposures of a scene to combine into a single image, allowing it to retain details in both shadows and highlights. This is particularly useful in photography, video, and medical imaging, where capturing fine details across varying light levels is crucial.

### Summary

Dynamic intensity range is a critical factor in image quality, as it determines the contrast, detail, and realism of an image. Higher bit depths and HDR techniques can help achieve greater dynamic ranges, which improve image clarity and depth.

---

## Spatial Resolution

**Spatial resolution** refers to the level of detail an imaging system can capture, measured by the smallest distinguishable elements within an image. In digital imaging, spatial resolution defines the clarity or fineness of the image, usually based on the pixel density or the number of pixels per unit area.

### 1. Definition

Spatial resolution is determined by the number of pixels in an image. Higher spatial resolution means more pixels are used to represent the image, resulting in finer details and a clearer image. Lower spatial resolution means fewer pixels, resulting in a more pixelated or blurred appearance.

### 2. Measuring Spatial Resolution

Spatial resolution is commonly measured in:

- **Pixels per inch (PPI)**: Often used for screens and monitors, it defines the number of pixels displayed per inch of screen.
- **Dots per inch (DPI)**: Commonly used for printing, it measures the density of printed dots within a linear inch.

For example, an image with 300 PPI will have higher spatial resolution than an image with 72 PPI, as it has more pixels per unit area, offering better detail.

### 3. Impact on Image Quality

- **High Spatial Resolution**: Provides greater detail, making it ideal for applications requiring precision, such as medical imaging and satellite imagery.
- **Low Spatial Resolution**: Reduces detail, which can make images appear blurry or pixelated. This is often used for thumbnail images or cases where storage space needs to be minimized.

### 4. Examples

- **Standard Screen Resolution**: A common screen resolution of 1920x1080 pixels on a 15-inch screen has a spatial resolution of approximately 146 PPI.
- **High-Resolution Imaging**: A 4K display with 3840x2160 pixels on the same screen size has a spatial resolution of about 293 PPI, allowing for finer image details.

### 5. Importance in Digital Imaging

Spatial resolution is a critical factor in determining image clarity and is chosen based on the needs of the application. Higher resolution images require more storage and processing power but provide better detail, which is essential in fields like digital photography, medical imaging, and remote sensing.

> **Note**: Increasing spatial resolution improves image clarity but also increases file size, which can impact storage and performance requirements.

---
