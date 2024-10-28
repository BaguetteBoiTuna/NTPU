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

