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

## Revisiting image processing

![[Tldraw Image.png]]

## Image sensing and acquisition

Many of the images we study or analyze are produced through the interplay of an "illumination" source and the "reflection" or absorption of energy from this source by the elements comprising the "scene" under observation.

The illumination source can vary and may include electromagnetic energy sources like radar, infrared, X-ray systems, ultrasound or even computer generated illumination patterns.

## Digital image acquisition

Physical Devices -> Image Sensors -> Digitizer/Film roll

## Image sampling and Quantization

In Digital Image Processing, signals captured from the physical world need to be translated into digital form through the process called Digitization. To make an image function f(x, y) suitable for digital processing, it must be digitized both spatially and in amplitude. This digitization process involves those steps:
Analog image -> Sampling -> Quantization -> Digital Image

1. **Analog Image**: An analog image is a continuous representation of an image, typically in the form of light or other electromagnetic waves, such as those captured by traditional film cameras. Analog images vary smoothly without discrete steps or interruptions, meaning they are theoretically infinite levels of detail and are not represented by discrete pixels.
2. **Sampling**: Sampling is the process of converting an analog image into a digital format by capturing a finite number of points from the continuous image. This is done by dividing the image into a grid and measure the intensity (color or brightness) at each point on the grid. The density of these sampling points affects the resolution of the resulting digital image: higher sampling rates capture more details and yield higher resolution images.
3. **Quantization**: Quantization is the process that follows sampling, where each sampled point's continuous intensity value is mapped to a finite set of discrete levels. In digital imaging, this often means assigning each sampled point a specific color or grayscale value, represented in binary. The number of quantization levels (e.g., 256 for an 8-bit grayscale image) determines the depth of detail in brightness or color that the image can represent.
4. **Digital Image:** A digital image is the result of the sampling and quantization processes. It is a discrete representation of the original analog image, stored as a grid of pixels where each pixel has a specific intensity or color value. Digital images can be displayed, processed and stored on digital devices like computers and are commonly represented in file formats like JPEG, PNG or BMP.

## Representing digital images

Digital images are represented through a function, \( f(x, y) \), where \( x \) and \( y \) define spatial locations within the image. This function assigns each point (or pixel) a specific intensity or color value, forming a structured grid that represents the image in digital form.

The spatial axes, \( x \) (horizontal) and \( y \) (vertical), mark the position of each pixel. The function \( f(x, y) \) indicates how intensity or color varies across these positions, allowing each \( (x, y) \) coordinate in the digital grid to match a pixel on a display or printed output. The pixel values indicate the color or brightness at each location, creating an accurate digital representation that can be stored, processed, and displayed effectively.
