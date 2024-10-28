---
id: 2024-10-28-dlfia_dante_assignment2
aliases:
  - DLfIA_Dante_Assignment2
tags: []
---

# DLfIA_Dante_Assignment2

ID: 711382799

## Question 1

### What specific model configuration lead to underfitting the best fit, and overfitting when training on the MNIST dataset? Demonstrate these scenarios and print the results

Here are 3 different model configurations that lead to underfitting, best fit, and overfitting the best fit when training on the MNIST dataset.

```python
# Underfitting Model
underfit_model = Sequential(
    [
        Input(shape=(28, 28)),
        Flatten(),
        Dense(32, activation="relu"),
        Dense(10, activation="softmax"),
    ]
)
underfit_history = compile_and_train(underfit_model)

# Optimal Fit Model
optimal_model = Sequential(
    [
        Input(shape=(28, 28)),
        Flatten(),
        Dense(128, activation="relu"),
        Dense(64, activation="relu"),
        Dense(10, activation="softmax"),
    ]
)
optimal_history = compile_and_train(optimal_model)

# Overfitting Model
overfit_model = Sequential(
    [
        Input(shape=(28, 28)),
        Flatten(),
        Dense(1024, activation="relu"), # This is overkill but for some reason
        Dense(512, activation="relu"),  # I could not get the model to overfit
        Dense(256, activation="relu"),
        Dense(128, activation="relu"),
        Dense(10, activation="softmax"),
    ]
)
overfit_history = compile_and_train(overfit_model)
```

I had issues Where the Overfitting Model would strangely be very close to the optimal model while having 2 more layers. This is the reason why i went a bit overkill. I also used a smaller subset to get the model to overfit.
Here are the results i got from testing the models:
![[answer1.png]]![[answer1_2.png]]![[me struggling.png]]![[finally overfitting.png]]

We can see on the last image that the Underfit Model (Blue) needs alot of training and the validation loss does not improve much. The Optimal Model (Orange) has a good balance between training, validation loss and is stable. The Overfit Model (Green) has a higher validation loss than the other models and a lower training loss. This is a sign of overfitting.

here is the entire source code used for this question:

```python

import tensorflow as tf
from tensorflow.keras.datasets import mnist
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Dense, Flatten, Input
from tensorflow.keras.optimizers import Adam
import matplotlib.pyplot as plt
from tensorflow.keras.mixed_precision import set_global_policy

# Making things faster (rip my GPU)
set_global_policy("mixed_float16")

# Load MNIST dataset
(x_train, y_train), (x_test, y_test) = mnist.load_data()
x_train, x_test = x_train / 255.0, x_test / 255.0  # Normalize data

# Had issues with overfitting not really showing so im using a smaller subset
x_train, y_train = x_train[:500], y_train[:500]

# Function to compile and train a model
def compile_and_train(model, epochs=20):
    model.compile(
        optimizer=Adam(), loss="sparse_categorical_crossentropy", metrics=["accuracy"]
    )
    history = model.fit(
        x_train, y_train, validation_data=(x_test, y_test), epochs=epochs, verbose=2
    )
    return history


# Underfitting Model
underfit_model = Sequential(
    [
        Input(shape=(28, 28)),
        Flatten(),
        Dense(32, activation="relu"),
        Dense(10, activation="softmax"),
    ]
)
underfit_history = compile_and_train(underfit_model)

# Optimal Fit Model
optimal_model = Sequential(
    [
        Input(shape=(28, 28)),
        Flatten(),
        Dense(128, activation="relu"),
        Dense(64, activation="relu"),
        Dense(10, activation="softmax"),
    ]
)
optimal_history = compile_and_train(optimal_model)

# Overfitting Model
overfit_model = Sequential(
    [
        Input(shape=(28, 28)),
        Flatten(),
        Dense(1024, activation="relu"), # This is overkill but for some reason
        Dense(512, activation="relu"),  # I could not get the model to overfit
        Dense(256, activation="relu"),
        Dense(128, activation="relu"),
        Dense(10, activation="softmax"),
    ]
)
overfit_history = compile_and_train(overfit_model)


# Plot results
def plot_history(histories, title):
    plt.figure(figsize=(10, 6))
    colors = ["#1f77b4", "#ff7f0e", "#2ca02c", "#d62728", "#9467bd", "#8c564b"]
    markers = ["o", "s", "D", "^", "v", "p"]
    for idx, (label, history) in enumerate(histories.items()):
        # Plot validation loss with solid line
        plt.plot(
            history.history["val_loss"],
            label=f"{label} val_loss",
            color=colors[idx % len(colors)],
            linestyle="-",
            marker=markers[idx % len(markers)],
            markersize=5,
        )
        # Plot training loss with dashed line
        plt.plot(
            history.history["loss"],
            label=f"{label} loss",
            color=colors[idx % len(colors)],
            linestyle="--",
            marker=markers[idx % len(markers)],
            markersize=5,
        )

    plt.title(title, fontsize=16)
    plt.xlabel("Epochs", fontsize=12)
    plt.ylabel("Loss", fontsize=12)
    plt.legend(loc="upper right", fontsize=10, frameon=True, shadow=True)
    plt.grid(True, linestyle="--", alpha=0.6)
    plt.show()


# Plot Losses
plot_history(
    {
        "Underfit": underfit_history,
        "Optimal": optimal_history,
        "Overfit": overfit_history,
    },
    "Training and Validation Loss",
)
```

---

## Question 2

### What are the fundamental differences between the Sigmoid, Tanh, ReLU, and Leaky ReLU activation functions? Additionally, illustrate how these different activation functions impact the overall performance of neural networks in digit recognition tasks using the MNIST dataset

Here are the differences between them:

1. **Sigmoid**: Good for probabilities (outputs between 0 and 1), but can slow down training due to small gradients. Not zero-centered, which affects convergence.
2. **Tanh**: Outputs between -1 and 1, which helps in training speed. Still suffers from small gradients at extreme values.
3. **ReLU**: Fast and avoids small gradients, but can lead to “dead neurons” where some neurons stop learning.
4. **Leaky ReLU**: Similar to ReLU but fixes the “dead neuron” issue by allowing a small gradient for negative inputs.

_source_: [OpenCV Activation Functions](https://learnopencv.com/understanding-activation-functions-in-deep-learning/)

Did 2 clean little Plots to visually show the differences between them:

![[ModelAccuracy.png]]![[ModelLoss.png]]

Here is the source code used for this question:

```python
import tensorflow as tf
from tensorflow.keras.datasets import mnist
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Dense, Flatten, Input
from tensorflow.keras.optimizers import Adam
import matplotlib.pyplot as plt

(x_train, y_train), (x_test, y_test) = mnist.load_data()
x_train, x_test = x_train / 255.0, x_test / 255.0


# Define a function to create and compile the model with a given activation function
def create_model(activation):
    model = Sequential(
        [
            Input(shape=(28, 28)),
            Flatten(),
            Dense(128, activation=activation),
            Dense(64, activation=activation),
            Dense(10, activation="softmax"),
        ]
    )
    model.compile(
        optimizer=Adam(), loss="sparse_categorical_crossentropy", metrics=["accuracy"]
    )
    return model


# Function to train and return history
def train_model(model):
    history = model.fit(
        x_train, y_train, validation_data=(x_test, y_test), epochs=10, verbose=2
    )
    return history


# Train models with different activation functions
activations = ["sigmoid", "tanh", "relu", "leaky_relu"]
histories = {}

for activation in activations:
    if activation == "leaky_relu":
        model = create_model(
            tf.keras.layers.LeakyReLU(alpha=0.1)
        )  # Saw on StackOverflow I had to do this with Leaky ReLU
    else:
        model = create_model(activation)
    histories[activation] = train_model(model)


def plot_results(histories, metric="loss"):
    plt.figure(figsize=(12, 6))
    colors = ["#1f77b4", "#ff7f0e", "#2ca02c", "#d62728"]
    markers = ["o", "s", "^", "D"]

    for idx, (activation, history) in enumerate(histories.items()):
        # Plot validation metric with solid line and marker
        plt.plot(
            history.history[f"val_{metric}"],
            label=f"{activation.capitalize()} Validation {metric.capitalize()}",
            color=colors[idx % len(colors)],
            linestyle="-",
            marker=markers[idx % len(markers)],
            markersize=6,
        )

        # Plot training metric with dashed line and same color
        plt.plot(
            history.history[metric],
            label=f"{activation.capitalize()} Training {metric.capitalize()}",
            color=colors[idx % len(colors)],
            linestyle="--",
            marker=markers[idx % len(markers)],
            markersize=4,
            alpha=0.7,
        )

    plt.title(
        f"Model {metric.title()} with Different Activation Functions", fontsize=16
    )
    plt.xlabel("Epochs", fontsize=12)
    plt.ylabel(metric.title(), fontsize=12)
    plt.legend(loc="upper right", fontsize=10, frameon=True, shadow=True)
    plt.grid(True, linestyle="--", alpha=0.6)
    plt.tight_layout()
    plt.show()


# Plot Loss and Accuracy
plot_results(histories, "loss")
plot_results(histories, "accuracy")
```

---

## Question 3

### Why might ReLU and Leaky ReLU perform better than Sigmoid and Tanh in deep networks? Please provide results to support your explanation

Using the same [source](https://learnopencv.com/understanding-activation-functions-in-deep-learning/) than the previous question:

1. Gradiant Saturation

   - Sigmoid and Tanh can cause the gradients to become very small. Vanishing gradients in deeper layers, can slow down the learning.
   - ReLU and Leaky ReLU do not have this issue.

2. Computation Efficiency

   - ReLU and Leaky ReLU are computationally simpler so more efficient than Sigmoid and Tanh.

3. Sparse Activation
   - ReLU has only a subset of neurons activated at a time. It reduces dependencies and enhances model interpretability and computational efficiency.

Tried showing this visually but its quite hard to notice:

![[question3.png]]

here is the source code used for this question:

```python
import tensorflow as tf
from tensorflow.keras.datasets import mnist
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Dense, Flatten, Input
from tensorflow.keras.optimizers import Adam
import matplotlib.pyplot as plt

(x_train, y_train), (x_test, y_test) = mnist.load_data()
x_train, x_test = x_train / 255.0, x_test / 255.0


# Define a function to create and compile the model with a given activation function
def create_deep_model(activation):
    model = Sequential(
        [
            Input(shape=(28, 28)),
            Flatten(),
            Dense(512, activation=activation),
            Dense(256, activation=activation),
            Dense(128, activation=activation),
            Dense(10, activation="softmax"),
        ]
    )
    model.compile(
        optimizer=Adam(), loss="sparse_categorical_crossentropy", metrics=["accuracy"]
    )
    return model


# Function to train and return history
def train_model(model, epochs=10):
    history = model.fit(
        x_train, y_train, validation_data=(x_test, y_test), epochs=epochs, verbose=2
    )
    return history


activations = ["sigmoid", "tanh", "relu", "leaky_relu"]
histories = {}

for activation in activations:
    if activation == "leaky_relu":
        model = create_deep_model(tf.keras.layers.LeakyReLU(alpha=0.1))
    else:
        model = create_deep_model(activation)
    histories[activation] = train_model(model)


# Plot the results for loss and accuracy
def plot_results(histories, metric="loss"):
    plt.figure(figsize=(12, 6))
    colors = ["#1f77b4", "#ff7f0e", "#2ca02c", "#d62728"]
    markers = ["o", "s", "^", "D"]
    for idx, (activation, history) in enumerate(histories.items()):
        # Plot validation metric with solid line and marker
        plt.plot(
            history.history[f"val_{metric}"],
            label=f"{activation.capitalize()} Validation {metric.capitalize()}",
            color=colors[idx % len(colors)],
            linestyle="-",
            marker=markers[idx % len(markers)],
            markersize=6,
        )
        # Plot training metric with dashed line
        plt.plot(
            history.history[metric],
            label=f"{activation.capitalize()} Training {metric.capitalize()}",
            color=colors[idx % len(colors)],
            linestyle="--",
            marker=markers[idx % len(markers)],
            markersize=4,
            alpha=0.7,
        )

    plt.title(
        f"Model {metric.title()} with Different Activation Functions", fontsize=16
    )
    plt.xlabel("Epochs", fontsize=12)
    plt.ylabel(metric.title(), fontsize=12)
    plt.legend(loc="upper right", fontsize=10, frameon=True, shadow=True)
    plt.grid(True, linestyle="--", alpha=0.6)
    plt.tight_layout()
    plt.show()


# Plot Loss and Accuracy
plot_results(histories, "loss")
plot_results(histories, "accuracy")
```

---

## Question 4

### What indicators in the loss and accuracy plots suggest underfitting, the best fit, and overfitting? Please visualize these indicators and explain their significance

