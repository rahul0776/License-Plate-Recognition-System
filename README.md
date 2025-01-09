# License-Plate-Recognition-System
License Plate Recognition Systems use the concept of optical character recognition to read the characters on a vehicle license plate. In other words, LPR takes the image of a vehicle as the input and outputs the characters written on its license plate.<br>
<h2>LPR sometimes called ALPR (Automatic License Plate Recognition) has 3 major stages.</h2>


License Plate Detection: This is the first and probably the most important stage of the system. It is at this stage that the position of the license plate is determined. The input at this stage is an image of the vehicle and the output is the license plate.<br>
Character Segmentation: It’s at this stage the characters on the license plate are mapped out and segmented into individual images.<br>
Character Recognition: This is where we wrap things up. The characters earlier segmented are identified here. We’ll be using machine learning for this.

<h3>License Plate Detection (Plate localization)</h3><br>

This is the first stage and at the end of this stage, we should be able to identify the license plate’s position on the car.<br> In order to do this, we need to read the image and convert it to grayscale. In a grayscale image, each pixel is between 0 & 255. <br>We now need to convert it to a binary image in which a pixel is either complete black or white.<br>
We need to identify all the connected regions in the image, using the concept of connected component analysis (CCA).<br> Other approaches like edge detection and morphological processing can also be explored.<br> CCA basically helps us group and label connected regions on the foreground. A pixel is deemed to be connected to another if they both have the same value and are adjacent to each other.<br>
<h3>Character Segmentation</h3>

This part of the process focuses on identifying and extracting individual characters from the detected license plate using Connected Component Analysis (CCA). The license plate is inverted (black pixels to white and vice versa) to standardize the segmentation process.<br> After labeling connected regions in the binary image, the script identifies regions that satisfy specific height and width criteria based on assumptions about the dimensions of characters relative to the license plate.<br>

Key steps include:<br>

Filtering regions: Ensures only regions with dimensions resembling license plate characters are selected.<br>
Drawing boundaries: Red rectangles are drawn around identified characters for visualization.<br>
Resizing: Each detected character is resized to 20x20 pixels for uniformity and preparation for recognition.<br>
Tracking order: The column_list records the x-coordinates of the detected regions to maintain the correct sequence of characters.<br>
This process prepares the segmented characters for the next stage: recognition.<br>

<h3>Character Recognition</h3><br>

This is going to be the last stage, it’s at this stage we introduce the concept of machine learning. Machine learning can simply be defined as the branch of AI that deals with data and processes it to discover pattern that can be used for future predictions. The major categories of machine learning are supervised learning, unsupervised learning and reinforcement learning. Supervised learning makes use of a known dataset (called the training dataset) to make predictions. We’ll be taking the path of supervised learning because we already have an idea of how As, Bs and all the letters look like. Supervised learning can be divided into two categories; classification and regression. Character recognition belongs to the classification category.
<br>
All we need now is to get a training data set, choose a supervised learning classifier, train a model, test the model and see how accurate it is, then use the model for prediction.
<br>
Let’s start with training our model. I have two different datasets, one is 10px by 20px and the other is 20px by 20px. We’ll make use of the 20px by 20px because we’ve already resized each character to that size. 
<br>
There are several classifiers we can use with each of them having its advantages and disadvantages. We’ll use SVC (support vector classifiers) for this task. I chose to use SVC because it gave me the best performance. However, this does not necessarily mean that SVC is the best classifier.<br>
A 4-fold cross validation was also done to determine how accurate the model is and then the model was persisted to a file so that predictions can be done without training a model anymore.<br>
Now that we have a trained model, we can attempt to predict the characters that we earlier segmented.
