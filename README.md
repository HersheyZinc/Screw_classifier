# Screw_classifier

## Introduction
Screws are essential tools for many professions in home, industrial and research settings. However there exists a large variety of screws, each with their unique features and use. While some types are hardly distinguishable with the naked eye, using the wrong screw type can result in damage to important equipment, or even fatal errors.

Our team aims to create a cheap, efficient and accessible application to sort screws by utilizing artificial intelligence. In this project, we adopted a deep learning approach, using Convolutional Neural Network (CNN) to automate the identification and classification task of 4 unique types of screws. As proof of concept, our primary objective is for our application to distinguish between M4x10, M4x16, M6x10 and M6x12 screws, and a control class “None”.

## Data Collection
The methodology of creating the dataset was as such: We first placed the screw onto a plate. The plate is then placed on a rotating dish. A camera is then attached to a tripod a certain distance away and aimed at the screw. The dish is then rotated uniformly and the video is recorded. We repeated this process for different camera angles, different background colours and different screw types. This process allowed us to collect a robust dataset.

To create a dataset of large enough samples, it would be extremely time and energy consuming to manually take photos of the screws. As such, we automated the process of converting video data into an image dataset through the openCV library in Python. By reading video files frame by frame, and extracting an image between a set amount of frames, we can reliably obtain images of the screws at unique positions and angles.

## Tried Models
We first explored the possibility of our own CNN models with a few layers. However, results showed high training accuracy but low test accuracy, signifying that our models were overfitting. After trail and error with multiple parameters, we concluded that the model we had on hand was not complex enough for the task.

We then moved on to try transfer learning. We collected pre-trained models such as InceptionV3, VGG16, and EfficientNet, and froze their bottom layers. We then set the top layers to fit our classification task and trained it on our dataset.

## Results
After evaluating all the different models, we compared their train,validation and test results. From this, we observed that while all models fared well on the train data, the transfer learning models did significantly better on validation data than the models we created ourselves. A possible explanation for this would be that our own models were not complex enough and were overfitting on the train data, or that they were emphasising on the wrong features of the images.

Our second observation was that aside from the InceptionV3 model, all other models had suboptimal accuracy results on the test data. This signifies that these models were still memorizing features that were present in the train and validation data, but not in the test. On the other hand, InceptionV3 managed to keep its high accuracy score, indicating that it was successful in generalizing the features of each class of screw, and could effectively apply it on images it had not seen before. As such, our team decided that this model is the most suitable to reach our objective and should be implemented into our final product.

## Telegram Implementation
By utilizing Python to access the telegram API, we set up a script to follow the flow as follows. Firstly, an image is uploaded to the telegram API via Telegram bot. It then sends the image to our CNN model using google colabotary and generates a prediction. This prediction is then displayed back to the user via text message.
