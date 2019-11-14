---
layout: single
title:  "Using GPU in venv"
date:   2019-11-14 09:35:00 +0100
categories: python jupyter-notebook tensorboard
---

# Virtualenv

## Create venv
```powershell
virtualenv .\venv_directory
```

## Activate venv
```powershell
.\virtualenv\Scripts\activate
```

## Install tensorflow
As we want to use the GPU we have to install
```powershell
pip install tensorflow-gpu
```

# Install VisualStudio 2017 Community
We need 2017 as we have to use CUDAv10.0 as TensorFlow is not yet compatible with CUDAv10.1, the installer is sadly only available with a free Microsoft Dev account and under the link for [MyVisualStudio - Downloads](https://my.visualstudio.com/Downloads?q=Visual%20Studio%202017).

Install VS2017 Community and the C++ Workload
![VS Installer with correct workloads](/images/VS2017-installation.png)

# Install CUDA and cuDNN

Get the CUDAv10.0 Installer from the [CUDA Toolkit Archive](https://developer.nvidia.com/cuda-toolkit-archive) and the cuDNN zip file from the [cuDNN Archive](https://developer.nvidia.com/rdp/cudnn-archive).

Install CUDAv10.0 and copy the files in the cuDNN zip file to the install directory.

Check if the installer has correctly added a system environment variable called 'CUDA_PATH' pointing to the install directory, otherwise add it yourself.
![CUDA System Environment Variable](/images/CUDA-system-environment-variables.png)

# Check if installation was successful
Check for GPU
```python
import tensorflow as tf
print("Num GPUs Available: ", 
len(tf.config.experimental.list_physical_devices('GPU')))
```

Check if CUDA Toolkit is used correctly
```python
from tensorflow.keras.datasets import mnist
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Dense
from tensorflow.keras import utils
(X_train, y_train), (X_test, y_test) = mnist.load_data()
X_train = X_train.reshape(60000,784)
X_test = X_test.reshape(10000,784)
X_train = X_train.astype('float32')
X_test = X_test.astype('float32')
X_train /= 255.0
X_test /= 255.0
n_classes = 10
Y_train = utils.to_categorical(y_train)
Y_test = utils.to_categorical(y_test)
number_of_epochs = 10
batch_size = 128
dimension_input = X_train.shape[1]
model = Sequential()
model.add(Dense(n_classes, input_shape=(784,), activation='softmax'))
model.summary()
model.compile(optimizer='adam', loss='categorical_crossentropy', metrics=['accuracy'])
log = model.fit(X_train, Y_train, batch_size=batch_size, epochs=number_of_epochs, verbose=True, validation_data=(X_test, Y_test))
```

Enjoy!

Source: [m4l4 on StackOverflow](https://stackoverflow.com/a/58247816)