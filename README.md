# Gesture Recognition Case study

### Problem Statement
Imagine you are working as a data scientist at a home electronics company which manufactures state of the art smart televisions. You want to develop a cool feature in the smart-TV that can recognise five different gestures performed by the user which will help users control the TV without using a remote.

The gestures are continuously monitored by the webcam mounted on the TV. Each gesture corresponds to a specific command:
 
| Gesture | Corresponding Action |
| --- | --- | 
| Thumbs Up | Increase the volume. |
| Thumbs Down | Decrease the volume. |
| Left Swipe | 'Jump' backwards 10 seconds. |
| Right Swipe | 'Jump' forward 10 seconds. |
| Stop | Pause the movie. |

Each video is a sequence of 30 frames (or images).

### Objectives:
1. **Generator**:  The generator should be able to take a batch of videos as input without any error. Steps like cropping, resizing and normalization should be performed successfully.

2. **Model**: Develop a model that is able to train without any errors which will be judged on the total number of parameters (as the inference(prediction) time should be less) and the accuracy achieved. As suggested by Snehansu, start training on a small amount of data and then proceed further.

3. **Write up**: This should contain the detailed procedure followed in choosing the final model. The write up should start with the reason for choosing the base model, then highlight the reasons and metrics taken into consideration to modify and experiment to arrive at the final model.

### Dataset:
You can download the dataset from [here.](https://drive.google.com/uc?id=1ehyrYBQ5rbQQe6yL4XbLWe3FMvuVUGiL)
The training data consists of a few hundred videos categorised into one of the five classes. Each video (typically 2-3 seconds long) is divided into a sequence of 30 frames(images). These videos have been recorded by various people performing one of the five gestures in front of a webcam - similar to what the smart TV will use. 
The data is in a zip file. The zip file contains a 'train' and a 'val' folder with two CSV files for the two folders. These folders are in turn divided into subfolders where each subfolder represents a video of a particular gesture. Each subfolder, i.e. a video, contains 30 frames (or images). Note that all images in a particular video subfolder have the same dimensions but different videos may have different dimensions. Specifically, videos have two types of dimensions - either 360x360 or 120x160 (depending on the webcam used to record the videos). 


### Project Objective and Model Architecture:
Train a model that can correctly identify the 5 hand gestures based on the Test Data. 
For the same, there are two Architectures suggested.
- 3D Convs and 
- CNN-RNN Stack

3D convolutions- Its a natural extension to the 2D convolutions. Just like in 2D conv, you move the filter in two directions (x and y), in 3D conv, you move the filter in three directions (x, y and z). In this case, the input to a 3D conv is a video (which is a sequence of 30 RGB images).

CNN-RNN stack- The conv2D network will extract a feature vector for each image, and a sequence of these feature vectors is then fed to an RNN-based network. The output of the RNN is a regular SoftMax (for a classification problem such as this one).

### Model Architecture and Training:
-	Experimented with different configurations of the model, hyperparameters, number of iterations and combinations of batch sizes with image sizes, choice of kernels(size, padding, stride) for best accuracy. 
-	Also, tried different Learning Rates and used ReduceLRonPlateau to reduce Learning Rate if the metric(val_loss) remains unchanged in between epochs. 
-	For Optimizers, tried SGD() and Adam() but went ahead with Adam() optimizer as it led to improvement in accuracy by rectifying high variance in the model’s parameters. 
-	Also, we achieved little Regularization by using BatchNormalization, pooling and Dropouts when we saw that our model was overfitting (giving poor validation accuracy and good train accuracy) 



### OBSERVATIONS:

-	Training time is directly proportional to number of parameters 
-	Batch Size should be chosen as per the GPU selected. A large Batch size throws Out of Memory error. So, we need to find the optimal Batch size which our GPU can support. 
-	Increase in Batch size improves on computational cost however it affects accuracy implying a trade-off between both. So, we need to find the best Batch size which gives best computational time and highest accuracy. 
-	We achieved better accuracies when the image size selected was 128*128 in comparison to 64*64. 
-	We obtained a better performing model using Conv3D than CNN+LSTM and CNN+GRU based models. 


### FINAL MODEL:

We selected Conv3D model#1 as the best performing model over CNN+LSTM and CNN+GRU for following reasons: 
-	Training Accuracy : 81% 
-	Validation Accuracy: 85% 
-	Number of parameters are low 357,541 which makes the model computationally less expensive.
-	Model is Statistically simpler. 


## Technologies Used
- Pandas
- Numpy
- Tensorflow
- keras
- matplotlib
- seaborn
- OpenCV

## Acknowledgements
- This project was inspired by Course in ML and AI from IIITB and Upgrad.


## Contributors
- <a href="https://github.com/sawan121989/">Sawan Sabbu</a>
- <a href="https://github.com/pramod-prasad01/">Pramod Prasad</a>


