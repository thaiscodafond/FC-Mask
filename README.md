# FC-Mask
This project was made for IMT Atlantique's school administration to see and test if first year engineering students could develop a machine learning software without any prior knowledge.

## The algorithm

We used Jupyter Notebook to develop our code. We wanted to make a facial recognition software to know if someone was wearing a mask or not.


## The model
To build our algorithm, we must base ourselves on a model. This model will be based on a “Convolutional Neural Network”. A CNN is a neural network: an algorithm used to recognize patterns in data. Neural networks, in general, are composed of a set of neurons organized into layers, each with its own learnable weights and biases. This object is similar to the Pyrat teaching unit seen in the first year, which used weights in its graphs.
A model is nothing but a stack of layers. We can define our layers ourselves with the ones we decided to import:
from keras.layers import Conv2D, Input, ZeroPadding2D, BatchNormalization, Activation, MaxPooling2D, Flatten, Dense,Dropout
We relied on the Keras documentation to understand how they work.
We choose to train our model on images of 150x150 pixels.

## Training

We needed a dataset to fit the data into a neural network model.
How to create your own set? Create a folder and name it Dataset, then two subfolders in Dataset, name them train (for training) and test. Inside the train and test folders, create two subfolders in each of the image classes we're going to create.
In our case, we have a With_mask class and a Without_mask class. Then upload images of people wearing masks or not. Choose the images containing the people wearing the mask and place half of them in the folder With_mask, which is the subfolder of the train folders and choose the remaining images of people wearing a mask and place them in another folder With_mask, which is the test folders subfolder. Do the same for the images without a mask.

In our own dataset, we used 200 elements in test, and about 1200 elements in train. To retrieve the files, we use the flow_from_directory() method. The flow_from_directory() assumes that the directory contains at least two folders, one for the train and one for the test.
To have even more images to process, we use ImageDataGenerator(), a method that will perform a number of transformations on existing images to increase the size of the dataset. We then perform a replacement of the original batch of images by a new randomly transformed batch, then we can therefore train our model with this one.
We can then test our model using model.fit() with our dataset.

## Testing

To test our model, we decided to set it up on our laptop's camera before testing it on our embedded systems.
We use the cv2 library to display the video in real time. Several operations are performed on the image in real time to be able to analyze it. First, we use haar cascade to detect the faces present in the video, then for each face present, we test the trained model.
For aesthetic reasons, we create a rectangle that is displayed around the face, red if the person has no mask, green otherwise. We also display the confidence interval if a mask is recognized.

## Improvement

The program is not very functional when the person is not well lit, or if the person does not have fair skin. So this problem can easily be solved by adding more different people in the dataset while training the model. Moreover, the model having only been trained with blue mask images, it only works with them. We can also solve this problem by working in depth on the dataset.
Also, we only have two classes: with and without a mask. However, a mask can be put on the wrong way: with the nose or chin sticking out, for example. This can easily be fixed by creating new classes and uploading new photos.
With this first implementation of the software, the modification of the code is then very easy and can easily be adapted to other projects (recognition of moods for example).
