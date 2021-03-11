# Gesture-Recognition

## Problem Statement:
This project aims at preparing a gesture recognition model that can recognise five different gestures performed by the user. Each gesture corresponds to a specific task:
1.	Thumbs up:  Increase the volume
2.	Thumbs down: Decrease the volume
3.	Left swipe: 'Jump' backwards 10 seconds
4.	Right swipe: 'Jump' forward 10 seconds  
5.	Stop: Pause the movie

The training dataset is of 663 video folder and each folder/video has a sequence of 30 frames.

Different dimension of input dataset to be used are 360 x 360 and 140 x 120 and each of these are in RGB coloured format (i.e. 3 channels input).

## Pre-processing:
In order to pre-process the input images we have made sure that these are in same format so that the output from the model is accurate and we have a robust model trained for deployment.
1.	Cropping: We have cropped the 360 x 360 image to size of 340 X 340 by removing 10 units from top, bottom, left and right edges since the images at those ends are redundant and contain no information. We have not made any changes in 140X 120 image since it is of a very small size already and removing any information may lead to information loss.
2.	Resize: Both 340 X 340 and 140 X 120 dimension videos are resized to 120 x 120. This will make sure that a consistent dataset dimension is available to the model for training.
3.	Number of frames: We are choosing a total of 15 frames alternatively out of a total of 30 frames available for each gesture video. This is done in order to reduce the redundant information repeated in every frame and hence reducing the memory size which we will load onto the neural network.
4.	Normalise: This is done to speed up the process and quickly reach to convergence. In case, it is not used then the inputs will be of different scales and hence weights connected to some inputs will be updated much faster than others.
5.	Generator function: we have used a generator function which would help in providing a consistent stream of batched data set length into the model. This helps in an optimum utilisation of memory and we do not need to load the entire dataset at one go which will make the network go out of memory otherwise.
We are creating a batch size of 32 which. In each call to this function, we will traverse through a set of 32 video folders and in each folder, we will pre-process 15 frames (mentioned above). We will crop, resize and normalise the input arrays of video frames prior to returning it to the neural network.

## Architectures:
1.	CNN 3D: This is our final model giving best accuracy.

![alt text](https://github.com/robin991/Gesture-Recognition/blob/main/Image/CNN%203D%20final.png?raw=true)

![alt text](https://github.com/robin991/Gesture-Recognition/blob/main/Image/Conv3D_%20model%20accuracy.png?raw=true)

![alt text](https://github.com/robin991/Gesture-Recognition/blob/main/Image/Conv3D_%20Loss.png?raw=true)

2. CNN 2D – GRU stack: The performance of this architecture was not up to the mark.
We are not choosing this model. Model architecture is not shown for this.

![alt text](https://github.com/robin991/Gesture-Recognition/blob/main/Image/con2D_GRU_Model%20accuracy.png?raw=true)

![alt text](https://github.com/robin991/Gesture-Recognition/blob/main/Image/con2D_GRU_Model%20accuracy.png?raw=true)


## Conclusion:
Based on the below observations the performance of Convolution 3D is better out of the two.
### Conv3D:-
Train_Accuracy: 0.839
Val_Accuracy: 0.82
### Conv2D + GRU:-
Train_Accuracy: 0.95
Val_Accuracy: 0.61

