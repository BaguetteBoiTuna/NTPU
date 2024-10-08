---
id: 2024-10-08-dlfia_dante_assignment1
aliases:
  - DLfIA_Dante_Assignment1
tags: []
---

# DLfIA_Dante_Assignment1

ID: 711382799

## Question 1

### Set up a coding environment for deep learning in Google Colab do the following tasks

#### Install Required Libraries

![[Pasted image 20241008103648.png]]

#### Import the Libraries

![[Pasted image 20241008103808.png]]

#### Verify Installation

![[Pasted image 20241008103824.png]]

#### GPU Configuration

![[Pasted image 20241008103848.png]]

---

## Question 2

### What are the primary differences among deep learning frameworks: Keras, TensorFlow and PyTorch?

#### Keras

- **Easy to Use**: Keras is designed to be simple and user-friendly, making it ideal for beginners who want to quickly build and test models.
- **Works with TensorFlow**: Keras is integrated with TensorFlow, which helps in deploying models in production environments.

#### TensorFlow

- **Flexible**: TensorFlow is a powerful framework that provides more control over building complex models, suitable for both research and production.
- **Scalable**: It is optimized for handling large datasets and models, often used in industries and enterprise-level applications.

#### PyTorch

- **Beginner-Friendly**: PyTorch is considered more intuitive due to its simpler syntax and real-time execution, which makes it easy for beginners to learn and experiment.
- **Great for Research**: PyTorch is widely used in academia because it allows flexibility for experimenting with new ideas and models.

##### Sources

- [UnfoldAI on Keras vs PyTorch](https://unfoldai.com/keras-vs-pytorch-in-2024/).
- [DataCamp on PyTorch vs TensorFlow](https://www.datacamp.com/tutorial/pytorch-vs-tensorflow-vs-keras).
- [OpenCV’s AI Framework Comparison](https://opencv.org/blog/pytorch-vs-tensorflow/).

### Which framework do you prefer and why? Explain with an example

At this stage, I don’t really have a strong preference for any framework since I haven’t used any of them extensively. However, based on what I've heard, PyTorch seems to be more beginner-friendly compared to TensorFlow. PyTorch is often praised for its simpler syntax and dynamic computation graph, which makes it easier to learn and experiment with, especially when starting with deep learning.

Here is an example of a basic linear regression model I found on internet for both PyTorch and TensorFlow:

#### PyTorch Example

```py
import torch

# Define a simple linear regression model in PyTorch
model = torch.nn.Linear(1, 1)

# Input and output tensors
x = torch.tensor([[1.0], [2.0], [3.0], [4.0]])
y = torch.tensor([[2.0], [4.0], [6.0], [8.0]])

# Loss function and optimizer
loss_fn = torch.nn.MSELoss()
optimizer = torch.optim.SGD(model.parameters(), lr=0.01)

# Training loop
for epoch in range(100):
    # Forward pass
    y_pred = model(x)
    loss = loss_fn(y_pred, y)

    # Backward pass and optimization
    optimizer.zero_grad()
    loss.backward()
    optimizer.step()

print(f"Final loss: {loss.item()}")
```

#### TensorFlow Example

```py
import tensorflow as tf

# Define a simple linear regression model in TensorFlow
model = tf.keras.Sequential([
    tf.keras.layers.Dense(1, input_shape=(1,))
])

# Compile the model
model.compile(optimizer='sgd', loss='mse')

# Input and output tensors
x = [[1.0], [2.0], [3.0], [4.0]]
y = [[2.0], [4.0], [6.0], [8.0]]

# Train the model
model.fit(x, y, epochs=100, verbose=0)

# Print the final loss
loss = model.evaluate(x, y)
print(f"Final loss: {loss}")
```

While looking at the two different code snippets you can clearly see that TensorFlow has a shorter and "easier" approach compared to PyTorch, but too much abstraction you're trying to understand the basics of deep learning is not always good.

PyTorch breaks down the steps into more detail, which can be beneficial for beginners to understand the underlying concepts better. It might be a bit more verbose compared to TensorFlow but for someone like me that is just getting started it is a good thing and feels more intuitive.

---

## Question 3

### What is digital image processing and demonstrate common digital image processing at least five functions in Python using the OpenCV library?

Digital Image Processing involves the manipulation and analysis of digital images using computer algorithms to enhance the image or extract useful information from it.

For this question, I will use my laptop instead of Google Colab since i have already everything setup (and I rather code on my own machine using NeoVim, also its easier for testing since i have a debugger).
![[Pasted image 20241008113231.png]]
I will be using this picture of a colorful bird for the demonstration:
![[colorful_bird_474x338.jpg]]

#### Reading and Displaying an Image

```py
import cv2

# Read the image from the file
image = cv2.imread("./colorful_bird_474x338.jpg")

# Display the image
cv2.imshow("Image", image)

# Wait for a key press then close the window
cv2.waitKey(0)
cv2.destroyAllWindows()
```

![[Pasted image 20241008114427.png]]

#### Converting to GrayScale

```py
import cv2

# Read the image from the file
image = cv2.imread("./colorful_bird_474x338.jpg")

# Convert the image to grayscale
grayscale_image = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

# Display the image
# cv2.imshow("Image", image)
cv2.imshow("Grayscale Image", grayscale_image)

# Wait for a key press then close the window
cv2.waitKey(0)
cv2.destroyAllWindows()
```

![[Pasted image 20241008114810.png]]

#### Blurring the Image

```py
import cv2

# Read the image from the file
image = cv2.imread("./colorful_bird_474x338.jpg")

# Convert the image to grayscale
# grayscale_image = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

# Apply GaussianBlur to the image
gaussian_blur = cv2.GaussianBlur(image, (15, 15), 0)

# Display the image
# cv2.imshow("Image", image)
# cv2.imshow("Grayscale Image", grayscale_image)
cv2.imshow("Gaussian Blur", gaussian_blur)


# Wait for a key press then close the window
cv2.waitKey(0)
cv2.destroyAllWindows()
```

![[Pasted image 20241008115210.png]]

#### Edge Detection Using Canny

```py
import cv2

# Read the image from the file
image = cv2.imread("./colorful_bird_474x338.jpg")

# Convert the image to grayscale
# grayscale_image = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

# Apply GaussianBlur to the image
# gaussian_blur = cv2.GaussianBlur(image, (15, 15), 0)

# Apply Canny edge detection to the image
edges = cv2.Canny(image, 100, 200)

# Display the image
# cv2.imshow("Image", image)
# cv2.imshow("Grayscale Image", grayscale_image)
# cv2.imshow("Gaussian Blur", gaussian_blur)
cv2.imshow("Edges", edges)

# Wait for a key press then close the window
cv2.waitKey(0)
cv2.destroyAllWindows()
```

![[Pasted image 20241008115519.png]]

#### Resizing the Image

```py
import cv2

# Read the image from the file
image = cv2.imread("./colorful_bird_474x338.jpg")

# Convert the image to grayscale
# grayscale_image = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

# Apply GaussianBlur to the image
# gaussian_blur = cv2.GaussianBlur(image, (15, 15), 0)

# Apply Canny edge detection to the image
# edges = cv2.Canny(image, 100, 200)

# Resize the image to half of its original size
resized_image = cv2.resize(image, (0, 0), fx=0.5, fy=0.5)

# Display the image
# cv2.imshow("Image", image)
# cv2.imshow("Grayscale Image", grayscale_image)
# cv2.imshow("Gaussian Blur", gaussian_blur)
# cv2.imshow("Edges", edges)
cv2.imshow("Resized Image", resized_image)

# Wait for a key press then close the window
cv2.waitKey(0)
cv2.destroyAllWindows()
```

![[Pasted image 20241008115849.png]]

