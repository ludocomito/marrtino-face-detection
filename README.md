# MARRtino face mask classifier

## About the repo  🗂

This repository is part of the thesis project involving the robotic platform MARRtino developed by La Sapienza University of Rome. The goal of this project is making the robot navigate inside a mapped environment in order to make him take the package delivered by a postman.

Inside this repository lies the part of the project responsible for creating and training a neural network model capable of making MARRtino recognize faces (with and without masks on).

## Considerations about the dataset  💽

The dataset used for training my model can be found on Kaggle at [this page](https://www.kaggle.com/datasets/vijaykumar1799/face-mask-detection). It contains images belonging to the following classes:

- mask_weared_incorrect
- with_mask
- without_mask

It contains a total of 8982 photos, equally distributes in 2994 elements per folder.

This makes the dataset very balanced with all the classes represented with the same amount of samples. However, the presence of a class representing people with mask weared incorrectly makes the model less “rigid”, while introducing some noise due to possible ambiguous poses.

The following is a sample of 64 images plotted from the dataset:

![Plotted using MatplotlLib](MARRtino%20face%20mask%20classifier%207299dc058b1f423b8c52abe74d447d28/Schermata_2022-07-24_alle_22.53.59.png)

Plotted using MatplotlLib

## Choosing the model to be trained  🧠

The model chosen for this task of image classification is ResNet:

The Residual Network, or ResNet for short, is a model that makes use of the residual module.There are several variants of different sizes, including Resnet18, Resnet34, Resnet50, Resnet101, and Resnet152, all of which are available from torchvision models. **Here Resnet18 model is used.**

When deeper networks are able to start converging, degradation problem occurs. As the network depth increases, the accuracy gets saturated and then degrades rapidly. These degradation is not caused by overfitting, and adding more layers to a suitably deep model leads to higher training error. Degradation indicates **not** all systems are similarly easy to optimize.

Deep residual learning framework address the degradation problem. Instead of hoping each few stacked layers directly fit a desired underlying mapping, these layers are explicitly made to fit a residual mapping.

![resnet.png](MARRtino%20face%20mask%20classifier%207299dc058b1f423b8c52abe74d447d28/resnet.png)

## Training the model with PyTorch 🔥

The framework used to train the model is PyTorch. It takes care of image preprocessing and model training, and my implementation can be found in the [‘****face-mask-detection-marrtino.ipynb’****](https://github.com/ludocomito/marrtino-face-detection/blob/main/face-mask-detection-marrtino.ipynb) notebook that you can find inside the repository.

During my test I experimented training both a ResNet model that came with its weights pre-trained on the ImageNet dataset and a non pre-trained model based only on the ResNet architecture.

Basically I discovered by accident the concept of transfer learning. In fact the usage of a model which has been pre-trained to a similar problem leads to visibly better result, that I will show you in the next paragraph.

## Pre-trained vs plain ResNet18 results  🥊

![Schermata 2022-07-25 alle 00.09.27.png](MARRtino%20face%20mask%20classifier%207299dc058b1f423b8c52abe74d447d28/Schermata_2022-07-25_alle_00.09.27.png)