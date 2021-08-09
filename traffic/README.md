# CS50-AI Traffic

Write an AI to identify which traffic sign appears in a photograph.

## Experiment
The baseline model is the model from the lecture : 
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



## Experiment Results

| #  | Version                                                                                      | Accuracy             |
| :--| :------------------------------------------------------------------------------------------- | :------------------- |
| 1  | Baseline                                                                                     | `0.0558`             |
| 2  | Add second convolutional layer, identical to the first                                       | `0.9708`             |
| 3  | Add second maxpooling layer (after the second convolutional layer), identical to the first   | `0.9503`             |
| 4  | Remove second maxpooling layer, increase kernal size in second convolutional layer to (4, 4) | `0.9480`             |
| 5  | Double number of filters (to 64) in second convolutional layer                               | `0.9684`             |
| 6  | Double number of nodes in hidden layer to 256                                                | `0.9528`             |
| 7  | Add second hidden layer (both layers with 128 nodes)                                         | `0.9511`             |
| 8  | Remove dropout                                                                               | `0.9486`             |
| 9  | Increase dropout rate to 0.7                                                                 | `0.9022`             |
| 10 | Decrease dropout rate to 0.2                                                                 | `0.9491`             |


## Discussion

The base model performed very poorly, with only `0.0544` testing accuracy. Adding a second convolutional layer dramatically improved accuracy to `0.9708`. None of the other tested models were able to top this accuracy score. However, adding a second max-pooling layer,  doubling the number of filters in the second convolutional layer, and doubling the number of nodes in the hidden layer all yielded promising results, with accurcy scores above `0.95`.

