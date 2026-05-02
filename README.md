# Canonigo_Laboratory-Work_3_Custom_Image-Classifier

## Submitted By: JANE VANESSA CANONIGO

# Collab Link : https://colab.research.google.com/drive/1_o6BZH6bK04qqBAV5qy0kzS_dppJ5Xc2?usp=sharing
# Link Drive :https://drive.google.com/drive/folders/1-oFbRb808buWNlD7tqCI-nQXyQtHzukw?usp=drive_link


# Guide Questions (Student Reflection & Explanation

**1. Dataset Preparation**
1.1 My dataset was organized in Google Drive within a main folder called ImagesDataSet. Inside this folder, I created 20 separate subfolders, one for each medicinal plant category, and placed 250 images into each respective plant folder.

1.2 Folder structure is crucial for TensorFlow because it serves as an automatic labeling system. TensorFlow uses the subfolder names to assign labels to images, eliminating the need for separate metadata. This organized setup also facilitates efficient batch loading of images, which speeds up training and prevents memory overload.


**2. Model Training**

2.1 Convolutional layers function as automated feature detectors in image classification. Early layers detect basic elements like edges and textures, while deeper layers combine these to recognize complex features such as eyes or leaves. By scanning images with small filters, they maintain spatial relationships, helping the model identify objects regardless of their position.

2.2 Splitting data into training and validation sets is essential to ensure the model generalizes effectively rather than just memorizing data. The training set is used for learning patterns, while the validation set provides a "new data" test to check how well the model performs on unseen examples. This helps identify and prevent overfitting, where a model .

**3. Performance Analysis**

3.1 My model achieved a validation accuracy of approximately 61.7%, meaning it correctly identified images in the validation set about 62% of the time.

3.2 The quantity of images available significantly impacted the model's ability to learn and generalize effectively.


**4. Critical Thinking**

4.1 A challenge I encountered with my dataset was in the testing phase, where some plants were not accurately identified with a high degree of certainty.

4.2 Data augmentation enhances the model by creating artificial variations of existing images, preventing the model from simply memorizing specific pictures. By applying transformations like rotations, flips, and zooms during training, the model learns to focus on intrinsic plant features such as leaf shape and texture, rather than being influenced by specific angles or lighting.


**5. Application**

5.1 A practical application for this model could be a Mobile Field Guide for Community Health Workers. This tool would allow users in rural areas to quickly identify medicinal plants using their smartphone camera, providing accurate verification for traditional remedies and helping to prevent the dangerous use of incorrect plant species.

5.2 To integrate this system, I would convert the trained model to TensorFlow Lite for mobile or TensorFlow.js for web to optimize performance on consumer devices. For a mobile app, the model would be embedded to enable offline plant identification using the phone's camera. For a web application, I would use a backend framework like Flask or FastAPI to create an API that processes uploaded images and returns identification results and medicinal guidelines to a user-friendly web interface (e.g., built with HTML and JavaScript).


**Guide Questions (Student Explanation & Reflection)**

**Visualization & Overfitting**

Overfitting in my initial model was evident from the significant difference between training and validation accuracy—training accuracy increased towards 100%, while validation accuracy remained much lower. Furthermore, the validation loss began to climb sharply after a few epochs, indicating the model was memorizing specific image details rather than learning general features.
Data augmentation helped to synchronize the validation and training accuracies. While it made the training process more challenging, it stabilized the validation score and prevented it from fluctuating or decreasing, leading to more consistent performance on new data.

**Model Improvement**

Dropout layers serve to randomly disable a percentage of neurons during training. This technique prevents the model from relying too heavily on any single neuron, forcing the network to discover multiple independent pathways for recognition and thereby reducing memorization.
Data augmentation improves a model's ability to generalize by exposing it to various versions of images (e.g., flipped, rotated, altered lighting) that it might encounter in real-world scenarios. By training on these modified images, the model grasps the fundamental characteristics of the medicinal leaf, rather than just one specific photograph.


**Performance Comparison**

Before optimizations, the model showed high training accuracy but poor validation performance due to overfitting. After implementing improvements, both training and validation accuracies converged to approximately 61.7%, representing a more reliable and honest measure of performance.
Data Augmentation contributed the most to improving the model's performance. It effectively addressed the limited diversity in the original 5,000 images by generating countless variations, which was crucial in preventing the validation loss from escalating.

**Deployment & Application**

Saving the model (as an .h5 or .keras file) is important because it stores the learned weights and architectural design from training. This allows the model to be instantly used in other applications without requiring time-consuming retraining.
This model could be deployed by converting it to TensorFlow Lite for mobile use or by running it on a Flask/FastAPI web server. This setup would enable users to upload plant photos from the field and receive immediate identification, along with relevant medicinal preparation instructions, based on the model's predictions.


performs well on training data but poorly on real-world data, and allows for fine-tuning of the model's parameters.
