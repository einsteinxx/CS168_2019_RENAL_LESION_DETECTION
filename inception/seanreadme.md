#
information about the pre-trained model:
1 March 2016
This checkpoint contains the weights of an Inception v3 model that has been
trained to a 78.7% accuracy. On the ILSVRC 2012 validation data set, the
model correctly predicts 39371 images out of 50000 examples.


Our model is based on the pre-trained model and been train in 1000 steps
I used 500 images for training and 250 images for testing
The way I splite the raw data for every patient is that 2/3 for training and 1/3 for testing.
As you can see, the some of the images have lots of noises. 
I think the model could be better with more training data and training steps.
Will push the accuracy vs number of testing images later.

//This file does have the pre-train model and after-train model
//Since the pre-train is 480MB and after-train model 1.3GB
