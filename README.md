My approach to solve this problem is as following.
1. Read data from csv and construct the features X and labels y.\\
2. Normalize the training features by dividing 255 of each pixel value, to keep the result in the high derivative area of activation function(sigmoid).\\
3. Use one hot encoding to transform lables y to vectors.\\
4. Use sklearn train\_test\_split to split data into 2 parts, i.e. training and testing.\\
5. Use the predefined ann to fit the training data. I use L2 loss and mini-batch SGD to train the ann. I also implemented cross entropy loss, however, not used in this mnist task.\\
6. The strcuture of my ann is 5 layers ann, including input layer, 3 hidden layers and output layer. The size of the hidden layers is [256, 128, 64].\\
7. I did some hyperparameter tuning during the training. The final hyperparameter I used is learning rate is 0.1, number of epoches is 20, batch size is 32.\\
8. After 20 epoches of training, the accuracy on validation data is 97.24\%.\\
9. Plot the training cost and validation cost as a function of number of epoches, as shown below.\\
\[
\includegraphics[scale=0.75]{1.png}
\]
10. Plot the training accuracy and validation accuracy as a function of number of epoches, as shown below.\\
\[
\includegraphics[scale=0.75]{2.png}
\]
11. Plot the confusion matrix, as shown below.\\
\[
\includegraphics[scale=0.75]{3.png}
\]










