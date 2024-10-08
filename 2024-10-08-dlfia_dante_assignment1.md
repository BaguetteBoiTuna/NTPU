---
id: 2024-10-08-dlfia_dante_assignment1
aliases:
  - DLfIA_Dante_Assignment1
tags: []
---

# DLfIA_Dante_Assignment1

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

1. **Keras**

   - **Ease of Use**: Keras is known for its simplicity and user-friendly interface. It provides a high-level API that makes it ideal for beginners who want to quickly prototype deep learning models. It runs on top of TensorFlow and other backends like Theano.
   - **Performance**: Keras is slower compared to TensorFlow and PyTorch for complex models due to its higher-level abstractions.
   - **Deployment**: Integrated with TensorFlow, it benefits from TensorFlow's production-level tools like TensorFlow Serving and TensorFlow Lite, making it easier to deploy in real-world applications.

2. **TensorFlow**

   - **Flexibility**: TensorFlow offers both low-level control for complex neural networks and high-level APIs (via Keras), giving developers flexibility in model building. It's suited for large-scale models and production environments.
   - **Scalability**: TensorFlow is optimized for scalability, making it a strong choice for enterprise-level applications where performance and deployment are critical.
   - **Visualization**: TensorBoard, a TensorFlow tool, provides powerful visualization features for monitoring and debugging models, which is a unique advantage over PyTorch.

3. **PyTorch**
   - **Dynamic Computation Graph**: PyTorch is often favored by researchers and beginners due to its dynamic computation graph, allowing for real-time changes during model training. This makes it more flexible and easier to debug.
   - **Pythonic Syntax**: PyTorch’s code structure closely follows Python's conventions, making it intuitive for developers who are already familiar with Python.
   - **Research and Experimentation**: PyTorch is widely used in academia and research. It allows quick experimentation with new models and is often used for tasks involving natural language processing and computer vision.
   - **Beginner-Friendly**: Because of its simpler syntax and dynamic graph execution, PyTorch is often considered easier for beginners to pick up compared to TensorFlow.

- **Sources**:
  - UnfoldAI on Keras vs PyTorch.
  - DataCamp on PyTorch vs TensorFlow.
  - OpenCV’s AI Framework Comparison.
