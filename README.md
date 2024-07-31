Firs load code in google colab.

(If you are unfamiliar with using Colab, you can use the following guide:
https://www.aparat.com/v/u751kb9)

code link in google drive:
https://drive.google.com/file/d/1Otz9wfk-c8uSJGY6XKGL_UL0eRInH9Db/view?usp=drive_link

Dataset link in google drive:
https://drive.google.com/drive/folders/1rlP31T042SLtQNhlomgoHJrpDu8cXCsY?usp=drive_link

After loading the data into the Colab environment, we proceed with data augmentation. For this purpose, we define the data_augment function. This function initially takes the directory of the original data and the output directory for storing the augmented data. First, it checks if the output directory exists; if not, it creates it. Then, it stores all image data with extensions “.jpg”, “.jpeg”, and “.png” and performs the augmentation operations in sequence, saving each new file with an appropriate name after each operation.

For the flip operation, a random number generator is used to decide the type of flip before applying it. The rotations are performed sequentially by 90, 180, and 270 degrees, with each result saved.
Data augmentation is an approach that can significantly increase the number of data samples in a dataset for training a model. For image datasets, this approach uses processing operations such as reflection, rotation, cropping, or filling to augment the data. In this study, two image processing operations, namely flipping and rotating, were used for data augmentation. The following approach was considered:
	1: In the first stage of augmentation, 90 X-ray images were flipped to obtain 90 new images.
	2: In the second stage, the original 90 images were rotated by 90 degrees to obtain 90 additional images.
	3: In the third stage, the original images were rotated by 180 degrees to obtain another 90 images.
	4: Finally, the original 90 images were rotated by 270 degrees to obtain 90 more images.
These operations resulted in the creation of a dataset consisting of 450 COVID-19 X-ray images. Subsequently, to augment the data, we proceed to increase the given data.
We then rescale the training and test data. For the validation data, we create a subset of the training data with a size of 0.25 of the training data, which is also rescaled. We then take a batch of augmented training data and print the first four data samples in that batch. (Each batch has a structure of (32, 150, 150, 3), meaning there are 32 data samples in each batch.) Another batch of this data is taken, and four more images are printed.

A Convolutional Neural Network (CNN) architecture is used for binary classification tasks. The CNN model consists of 38 layers, including convolutional layers (Conv2D), max pooling, dropout, activation functions, batch normalization, flatten, and fully connected layers. The input image dimensions are set to (150, 150, 3) for RGB images. Convolutional layers use a 3×3 kernel. After each Conv2D layer, various techniques are applied, including max pooling (with a 2×2 size), batch normalization (along axis 1), ReLU activation function, and a dropout layer (with a 20% rate). The final output, obtained from 256 neurons in the last Conv2D layer, passes through max pooling, batch normalization, activation, and dropout layers.

For binary classification, the model uses the binary cross-entropy (BCE) loss function and the sigmoid activation function, as only one output node is needed to classify data into one of the two existing classes. The Adam optimizer is used to dynamically adjust the weight features and learning rate to minimize model loss.

Based on the described architecture and utilizing the TensorFlow library, we proceed to implement the proposed model. We then train the model using the validation data generated in previous steps. The number of epochs is set to 50, similar to the article. The learning rate is set to 0.006, determined experimentally through testing.

After training the model, we plot the loss and accuracy graphs for the training and validation data. Next, we evaluate the implemented network. To further evaluate this network structure, we define models with 1, 2, 3, 4, and 5 convolutional layers. These models are trained with augmented data similar to the original model with 6 convolutional layers and then evaluated using test and validation data.
