---
title: "Ways to create models in TensorFlow with keras."
date: 2021-04-25
comments: True
mathjax: True
tags: [machine learning]
---

There are three ways of creating models in `TensorFlow` using `keras`.

### Sequential API

Sequential is the easiest way to create models but allows less flexibility. We cannot share layers, have brances, multiple inputs or outputs
with sequential api. We define the sequential TF model like this
```python
def create_model(input_shape)
    model = keras.models.Sequential([
        keras.layers.Conv1D(..., input_shape),
        keras.layers.Dense(...)
    ])
    return model
```

### Functional API

Functional api allows us to create complex models with support for multiple inpts and outputs. We can have brances, share layers, and have graphs.
Any sequential model can be implemented using Functional api. Example of a Functional model is 
```python
def create_model(input_shape):
    inputs = keras.layers.Input(input_shape)
    x = keras.layers.Conv1D(...)(inputs)
    x = keras.layres.Dense(...)(x)
    
    model = keras.Model(inputs, x)
    return model
```

### Model Subclassing

The final way to create TF models is by inherating the `keras.Model` class. Model subclassing is fully-customizable and enables us to implement custom forward pass. 
```python
class CreateModel(keras.models.Model):
    def __init__(self, input_shape):
        super(CreateModel, self).__init__()
        self.in_shape = input_shape

        # create the layers
        self.conv = keras.layers.Conv1D(...)
        self.dense = keras.layers.Dense(...)

    def call(self, inputs):
        x = self.conv(inputs)
        x = self.dense(x)

        return x
```

Lastly, we can create the model using any of the above appraoch and train the model with proper `Optimizer` and `Loss` function like this.
```python
# Dataset
X, Y = get_data(...) 

# Model
model = create_model(input_shape) or CreateModel(input_shape)

# Optimizer and Loss settings
model.compile(loss = keras.loss.BinaryCrossEntropy(), 
            optimizer = keras.optimizer.Adam(learning_rate),
            metrics = ['accuracy'])

# traing the model
model.fit(Y, Y, batch_size, n_epochs, validation_split=0.25, verbose = 1)

# evaluate the model
model.evaluate(x, y)
```

Cheers! :grin: