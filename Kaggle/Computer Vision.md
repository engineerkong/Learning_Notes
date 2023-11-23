# Computer Vision

- Convolution (filter) + Activation (detect) + Maximum Pooling (condense)

pretrained base + untrained head

Problem: Translation Invariance - pooling destroyed some of their positional information

```
model = keras.Sequential([
    layers.Conv2D(filters=64, kernel_size=3), # activation is None
    layers.MaxPool2D(pool_size=2), / layers.GlobalAvgPool2D(), # reduces each of features to a single value
    # More layers follow
])
```

```
image_condense = tf.nn.pool(
    input=image_detect, # image in the Detect step above
    window_shape=(2, 2),
    pooling_type='MAX',
    # we'll see what these do in the next lesson!
    strides=(2, 2),
    padding='SAME',
)
```

- The sliding window:

The **strides** parameter says how far the window should move at each step, like (1,1)
 
and the **padding** parameter describes how we handle the pixels at the edges of the input. like 'valid' or 'same'

The receptive field just tells you which parts of the input image a neuron receives information from.

```
image = circle_64
kernel = bottom_sobel
visiontools.show_extraction(
    image, kernel,
    conv_stride=1,
    conv_padding='valid',
    pool_size=2,
    pool_stride=2,
    pool_padding='same',
    
    subplot_shape=(1, 4),
    figsize=(14, 6),
)
```

one-dimensional convolution

- Custom Convnets

Convolutional Blocks: convolution - activation - pooling

- Data Argumentation

train on more data: add in some extra fake data that looks reasonably like the real data and your classifier will improve, like flipped

```
model = keras.Sequential([
    # Preprocessing
    preprocessing.RandomFlip('horizontal'), # flip left-to-right
    preprocessing.RandomContrast(0.5), # contrast change by up to 50%
    # Base
    pretrained_base,
    # Head
    layers.Flatten(),
    layers.Dense(6, activation='relu'),
    layers.Dense(1, activation='sigmoid'),
])
```

```
augment = keras.Sequential([
    # preprocessing.RandomContrast(factor=0.5),
    preprocessing.RandomFlip(mode='horizontal'), # meaning, left-to-right
    # preprocessing.RandomFlip(mode='vertical'), # meaning, top-to-bottom
    # preprocessing.RandomWidth(factor=0.15), # horizontal stretch
    # preprocessing.RandomRotation(factor=0.20),
    # preprocessing.RandomTranslation(height_factor=0.1, width_factor=0.1),
])
```
