# Implementation-of-CNN

## AIM

To Develop a convolutional deep neural network for digit classification.

## Problem Statement and Dataset

The goal of this project is to develop a Convolutional Neural Network (CNN) to classify handwritten digits using the MNIST dataset. Handwritten digit classification is a fundamental task in image processing and machine learning, with various applications such as postal code recognition, bank check processing, and optical character recognition systems.

The MNIST dataset consists of 28x28 grayscale images of handwritten digits (0-9), totaling 60,000 training images and 10,000 test images. The challenge is to train a deep learning model that accurately classifies the images into the corresponding digits.

## Neural Network Model
![image](https://github.com/user-attachments/assets/0c8482c8-dee8-4c07-aed4-7913fdca2b9e)

## DESIGN STEPS

## STEP 1:
Import the necessary libraries and Load the data set.

## STEP 2:
Reshape and normalize the data.

## STEP 3:
In the EarlyStoppingCallback change define the on_epoch_end funtion and define the necessary condition for accuracy

## STEP 4:
Train the model
## PROGRAM

### Name:Bala murugan p
### Register Number:212222230017

```
import os
import base64
import numpy as np
import tensorflow as tf



data_path = "mnist.npz.zip"


(training_images, training_labels), _ = tf.keras.datasets.mnist.load_data(path=data_path)

print(f"training_images is of type {type(training_images)}.\ntraining_labels is of type {type(training_labels)}\n")

data_shape = training_images.shape

print(f"There are {data_shape[0]} examples with shape ({data_shape[1]}, {data_shape[2]})")
def reshape_and_normalize(images):
    """Reshapes the array of images and normalizes pixel values.

    Args:
        images (numpy.ndarray): The images encoded as numpy arrays

    Returns:
        numpy.ndarray: The reshaped and normalized images.
    """

  
    images = images[..., np.newaxis]

    
    images = images / 255.0

  

    return images

(training_images, _), _ = tf.keras.datasets.mnist.load_data(path=data_path)


training_images = reshape_and_normalize(training_images)
print('Name: Bala murugan           RegisterNumber: 212222230017        \n')
print(f"Maximum pixel value after normalization: {np.max(training_images)}\n")
print(f"Shape of training set after reshaping: {training_images.shape}\n")
print(f"Shape of one image after reshaping: {training_images[0].shape}")
import tensorflow as tf

class EarlyStoppingCallback(tf.keras.callbacks.Callback):

    def on_epoch_end(self, epoch, logs=None):
       
        if logs.get('accuracy') >= 0.995:
           
            self.model.stop_training = True
            print("\nReached 99.5% accuracy so cancelling training!")
import tensorflow as tf

def convolutional_model():
    """Returns the compiled (but untrained) convolutional model.

    Returns:
        tf.keras.Model: The model which should implement convolutions.
    """

    
    model = tf.keras.models.Sequential([
       
        tf.keras.layers.Conv2D(32, (3, 3), activation='relu', input_shape=(28, 28, 1)),

        tf.keras.layers.MaxPooling2D((2, 2)),

        tf.keras.layers.Conv2D(64, (3, 3), activation='relu'),
      
        tf.keras.layers.MaxPooling2D((2, 2)),

        tf.keras.layers.Conv2D(64, (3, 3), activation='relu'),

        tf.keras.layers.Flatten(),
       
        tf.keras.layers.Dense(64, activation='relu'),
       
        tf.keras.layers.Dense(10, activation='softmax')
    ])
   
    model.compile(
        optimizer='adam',
        loss='sparse_categorical_crossentropy',
        metrics=['accuracy']
    )

    return model
model = convolutional_model()
training_history = model.fit(training_images, training_labels, epochs=10, callbacks=[EarlyStoppingCallback()])
```

## OUTPUT

### Reshape and Normalize output

![image](https://github.com/user-attachments/assets/0ed303db-4979-499a-b51d-ff3836703dc4)



### Training the model output

![image](https://github.com/user-attachments/assets/9ec46827-a275-4494-ac3b-6138f607e529)





## RESULT
Thus the program for developing a convolutional deep neural network for digit classification.
