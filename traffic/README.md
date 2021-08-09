# CS50-AI Traffic

Write an AI to identify which traffic sign appears in a photograph.

## Experiment
The baseline model is the model from the [lecture](https://cs50.harvard.edu/ai/2020/notes/5/#convolutional-neural-networks) : 
```
model = tf.keras.models.Sequential([

# Convolutional layer. Learn 32 filters using a 3x3 kernel
tf.keras.layers.Conv2D(
    32, (3, 3), activation="relu", input_shape=(IMG_WIDTH, IMG_HEIGHT, 3)
),

# Max-pooling layer, using 2x2 pool size
tf.keras.layers.MaxPooling2D(pool_size=(2, 2)),

# Flatten units
tf.keras.layers.Flatten(),

# Add a hidden layer with dropout
tf.keras.layers.Dense(128, activation="relu"),
tf.keras.layers.Dropout(0.5),

 # Add an output layer with output units for all 10 digits
tf.keras.layers.Dense(NUM_CATEGORIES, activation="softmax")
])

# Train neural network
model.compile(
    optimizer="adam",
    loss="categorical_crossentropy",
    metrics=["accuracy"]
)
```
### Convolution and Max Pooling layer
Later on, I played around with the **Convolution and Max Pooling layer** 
1. Add another convolution and max pooling layer. 
Surprisingly, this change dramatically improve the accuracy form `0.0558` to `0.9646`.
![image](https://user-images.githubusercontent.com/65888725/128693936-b2b2b9a7-f07f-402d-9ec9-98ef7df77af0.png)
```
tf.keras.layers.Conv2D(
    32, (3, 3), activation="relu", input_shape=(IMG_WIDTH, IMG_HEIGHT, 3)
),

# Max-pooling layer, using 2x2 pool size
tf.keras.layers.MaxPooling2D(pool_size=(2, 2)),
```


## Experiment Results

| #  | Version                                                                                              | Accuracy             |
| :--| :----------------------------------------------------------------------------------------------------| :------------------- |
| 1  | Baseline                                                                                             | `0.0558`             |
| 2  | Add another Conv2D and MaxPooling2D  layer, identical to the first pair                                | `0.9646`             |
| 3  | Change the first Conv2D layer's filters to 16                                                        | `0.8631`             |
| 4  | Change the first Conv2D layer's filters to 64                                                        | `0.9514`             |
| 5  | Triple the initial Conv2D and MaxPooling2D                                                           | `0.9454`             |
| 6  | Change the 1st Conv2D filters to 16 / 2st Conv2D filters to 32 / 3rd Conv2D filters to 64            | `0.9535`             |
| 7  | Add BatchNormalization between the Conv2D and Conv2D and MaxPooling2D layer from 6th version         | `0.9823`             |
| 8  | Add BatchNormalization between the Conv2D and Conv2D and MaxPooling2D layer from 2nd version         | `0.9891`             |
| 9  | Add Dense NUM_CATEGORIES * 16 and dropout rate to 0.2 and dense NUM_CATEGORIES * 32 from 8th version | `0.9833`             |
| 10 | Change the 1st Conv2D filters to 64 from 9th version                                                 | `0.9804`             |


## Conclusion

In the experiment, I have tried 3 main distinct changes :
1. Conv2D and MaxPooling2D layer
2. BatchNormalization
3. Dense Layers

The model with 2 Conv2D, BatchNormalization, MaxPooling2D layers outperform all other model with the accuracy of `0.9891`. By adding another Conv2D and another MaxPooling2D layer distinctly improve the model's accuracy above `0.96`. The BatchNormalization layer has a very promising results that always rise the accuracy up to `0.98`. The Dense layer doesn't improve the accuracy score.
