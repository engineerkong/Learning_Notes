# Intro to Deep Learning

- A Single Neuron

![mfOlDR6](https://github.com/engineerkong/Learning_Notes/assets/89781823/486e044a-c90d-4f7d-84b1-a542074c3a3d)

Deep learning is an approach to machine learning characterized by deep stacks of computations.


Keras:

```
from tensorflow import keras
from tensorflow.keras import layers
# Create a network with 1 linear unit
model = keras.Sequential([
    layers.Dense(units=1, input_shape=[3])
])
w, b = model.weights
```

- Deep Neural Networks

modularity - building up a complex network from simpler functional units.

dense layers - collect together linear units having a common set of inputs. `layers.Dense(units=4,activation='relu),input_shape=[2]`

convolutional layers / recurrent layers

activation function: `layers.Activation('relu')` # ReLU: max(0,x) make nonlinear, except the output layer other: elu, selu, swish

```
from tensorflow import keras
from tensorflow.keras import layers
model = keras.Sequential([
    # the hidden ReLU layers
    layers.Dense(units=4, activation='relu', input_shape=[2]),
    layers.Dense(units=3, activation='relu'),
    # the linear output layer 
    layers.Dense(units=1),
])
```

- Stochastic Gradient Descent

**Loss function** 

loss function: mean absolute error (MAE) - abs(y_true-y_pred)

learning rate: optimizer - stochastic gradient descent / adam

size of batch: each iteration (epoch) 's sample of training data

```
model.compile(
    optimizer="adam",
    loss="mae",
)
```

```
history = model.fit(
    X_train, y_train,
    validation_data=(X_valid, y_valid),
    batch_size=256,
    epochs=10,
)
```

- Overfitting and Underfitting

1. signal and noise
training loss goes down: learn signal or noise

validation loss goes down: learn signal

2. capacity (how many neurons it has and how they are connected together)

underfitting: not enough signal, increase capacity (wider or deeper)

overfitting: too much noise

3. early stopping

![eP0gppr](https://github.com/engineerkong/Learning_Notes/assets/89781823/23973fe6-423a-41b9-9df0-617ec10c39a7)

callback: a function you want run every so often while the network trains.

```
early_stopping = EarlyStopping(
    min_delta=0.001, # minimium amount of change to count as an improvement
    patience=20, # how many epochs to wait before stopping
    restore_best_weights=True,
)
```
- Dropout and Batch Normalization

dropout layer: randomly drop out some fraction of a layer's input units every step of training - correct overfitting

```
keras.Sequential([
    # ...
    layers.Dropout(rate=0.3), # apply 30% dropout to the next layer
    layers.Dense(16),
    # ...
])
```

batch normalization layer: normalize the data before it goes into the network - speed up optimization

```
keras.Sequential([
    # ...
    layers.Dense(16),
    layers.BatchNormalization(),
    layers.Activation('relu'),
    # ...
])
```

```
    layers.Dense(1024, activation='relu'),
    layers.Dropout(0.3),
    layers.BatchNormalization(),
    layers.Dense(1),
```

- Binary Classification

accuracy = number_correct / total, threshold

cross-entropy: H(P,Q) = −∑P(x)logQ(x)

```
model.compile(
    optimizer='adam',
    loss='binary_crossentropy',
    metrics=['binary_accuracy'],
)
```

sigmoid activation: sigmoid(x) = 1/(1+e^(-x)) # for binary classification

`layers.Dense(1, activation='sigmoid')` # output layer use sigmoid activation 
