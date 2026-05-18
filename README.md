# 🌿 Laboratory Work 3 — Custom Image Classifier with TensorFlow
**Jane Vanessa Canonigo**
*Custom CNN-based Plant Species Image Classifier*

---

## 📁 Project Overview

This project builds a **Convolutional Neural Network (CNN)** image classifier using TensorFlow/Keras, trained on a custom dataset of **plant species images** stored in Google Drive. The classifier identifies plant categories based on folder-organized images and was iteratively improved using data augmentation and dropout regularization.

---

## 📊 Model Output Summary

### Initial Training (10 Epochs — No Augmentation)

| Epoch | Train Accuracy | Train Loss | Val Accuracy | Val Loss |
|-------|---------------|------------|--------------|----------|
| 1     | 0.2558        | 2.4451     | 0.3053       | 2.3767   |
| 2     | 0.4640        | 1.8181     | 0.5105       | 1.6749   |
| 3     | 0.5890        | 1.3625     | 0.4995       | 1.7223   |
| 4     | 0.7330        | 0.9306     | 0.5976       | 1.4790   |
| 5     | 0.8525        | 0.4927     | 0.5916       | 1.5910   |
| 6     | 0.9047        | 0.3184     | 0.6116       | 1.7697   |
| 7     | 0.9638        | 0.1413     | 0.6136       | 1.8575   |
| 8     | 0.9890        | 0.0529     | 0.6066       | 2.4845   |
| 9     | 0.9945        | 0.0293     | 0.6346       | 2.2123   |
| 10    | 0.9998        | 0.0037     | 0.6456       | 2.4213   |

> **Final Validation Accuracy (Initial Model): 64.56%**

---

### Improved Training (15 Epochs — With Data Augmentation + Dropout)

| Epoch | Train Accuracy | Train Loss | Val Accuracy | Val Loss |
|-------|---------------|------------|--------------|----------|
| 1     | 0.1673        | 2.6424     | 0.2973       | 2.3078   |
| 3     | 0.3770        | 2.0382     | 0.4464       | 1.8157   |
| 5     | 0.4493        | 1.8144     | 0.4775       | 1.7406   |
| 8     | 0.5040        | 1.6138     | 0.5656       | 1.4878   |
| 10    | 0.5562        | 1.4516     | 0.5616       | 1.5193   |
| 12    | 0.5757        | 1.3447     | 0.5806       | 1.3753   |
| 14    | 0.5953        | 1.2887     | 0.6366       | 1.2329   |
| 15    | 0.6300        | 1.2172     | 0.6216       | 1.2831   |

> **Final Validation Accuracy (Improved Model): 62.16%**

---

### 🔍 Prediction Output

The model was tested on a sample image (`MAYANA/249.jpg`):

```
Predicted Class: MAYANA
Confidence: 45.93%
```

---

## 📈 Training & Validation Curves

The charts below show the training and validation accuracy/loss over 15 epochs for the **improved model**. The narrowing gap between training and validation curves indicates that data augmentation and dropout successfully reduced overfitting compared to the initial model.

> *See `training_curves.png` — generated via `matplotlib` after model training.*

**What to observe:**
- **Initial model**: Training accuracy soared to ~99.98% while validation plateaued at ~64.56% → **clear overfitting**
- **Improved model**: Training accuracy grew more gradually (~63%) and validation accuracy tracked more closely → **better generalization**

---

## 🗂️ Dataset Organization

```
MyDrive/
└── ImagesDataSet/
    ├── MAYANA/
    │   ├── 001.jpg
    │   ├── 002.jpg
    │   └── ...
    ├── ClassB/
    │   └── ...
    └── ClassC/
        └── ...
```

- At least **20 plant species** categories
- Minimum **250 images per category**
- Folder names are automatically used as **class labels** by TensorFlow

---

## ❓ Guide Questions — Student Reflection

### Part 1: Dataset Preparation

**Q: How did you organize your dataset in Google Drive?**

The dataset was structured as a directory tree under `MyDrive/ImagesDataSet/`, where each subfolder corresponds to one plant species (e.g., `MAYANA/`). Each folder contains at least 250 `.jpg` images of that species.

**Q: Why is folder structure important for TensorFlow image loading?**

TensorFlow's `image_dataset_from_directory()` function automatically infers class labels from subfolder names. A clean, consistent folder structure eliminates the need for manual labeling and ensures correct mapping between images and their categories.

---

### Part 2: Model Training

**Q: What is the role of convolutional layers in image classification?**

Convolutional layers act as **feature detectors**. Early layers capture low-level features like edges and textures, while deeper layers detect higher-level patterns such as shapes and object parts. This hierarchical feature extraction is what allows CNNs to distinguish between visually similar plant species.

**Q: Why do we split data into training and validation sets?**

Splitting data prevents **data leakage** — the model only trains on the training set and is evaluated on the unseen validation set. This gives an honest estimate of how the model would perform on new, real-world images, and helps detect overfitting early.

---

### Part 3: Performance Analysis

**Q: What accuracy did your model achieve?**

| Model Version | Validation Accuracy |
|---------------|-------------------|
| Initial (10 epochs, no augmentation) | **64.56%** |
| Improved (15 epochs, augmentation + dropout) | **62.16%** |

While the improved model shows slightly lower raw accuracy, it generalizes better — the gap between training and validation accuracy is significantly smaller, indicating less overfitting.

**Q: How did the number of images affect the model's performance?**

With 250+ images per class across 20+ categories, the dataset is moderately sized. More images generally help the model learn a wider variety of visual patterns, reducing overfitting. However, image quality, class diversity, and lighting consistency also play crucial roles.

---

### Part 4: Critical Thinking

**Q: What challenges did you encounter while using your own dataset?**

- **Class imbalance**: Some species may have more images than others, biasing the model toward majority classes.
- **Image quality inconsistency**: Photos taken under different lighting conditions, angles, or backgrounds introduced noise.
- **Overfitting**: The initial model memorized training data (99.98% training accuracy vs. 64.56% validation), showing it failed to generalize.
- **Drive mounting latency**: Loading thousands of images from Google Drive introduced significant I/O overhead during training.

**Q: How can data augmentation improve your model?**

Data augmentation artificially expands the dataset by applying random transformations:

| Augmentation | Effect |
|---|---|
| `RandomFlip("horizontal")` | Teaches the model that a plant looks the same flipped |
| `RandomRotation(0.1)` | Accounts for images taken at different angles |
| `RandomZoom(0.1)` | Simulates images taken at different distances |

These transforms expose the model to more diverse representations of each class, reducing its tendency to memorize training-specific features.

---

### Part 5: Deployment & Application

**Q: Why is saving the model important?**

Saving the trained model (`.keras` format) allows:
- **Reuse** without retraining (which took hours on this dataset)
- **Deployment** to production systems or mobile apps
- **Versioning** — comparing future improved models against the current baseline

```python
model.save("/content/drive/MyDrive/ImagesDataSet/my_image_classifier.keras")
loaded_model = load_model("/content/drive/MyDrive/ImagesDataSet/my_image_classifier.keras")
```

**Q: Suggest a real-world application for your trained model.**

A **plant species identification mobile app** — users photograph a plant in their garden or in the wild, and the app instantly identifies the species and provides care instructions, medicinal uses, or ecological information. This could assist farmers, botanists, and conservation workers in the field.

**Q: How can this model be deployed in a real-world system?**

The saved `.keras` model can be:
1. **Converted to TensorFlow Lite** for on-device inference on Android/iOS
2. **Wrapped in a REST API** using FastAPI or Flask and hosted on a cloud server
3. **Integrated into a web app** using TensorFlow.js for browser-based inference
4. **Deployed via Google Cloud AI Platform** for scalable production use

---

### Part 6: Visualization & Overfitting (Activity 3A)

**Q: What signs indicated overfitting in your first model?**

The most telling sign was the **large divergence** between training and validation metrics:
- Training accuracy reached **99.98%** by epoch 10
- Validation accuracy plateaued at **64.56%**
- Validation loss *increased* from epoch 7 onward while training loss continued to drop

This gap is a textbook sign of overfitting — the model learned the training data's specific patterns rather than generalizable features.

**Q: How did data augmentation affect validation accuracy?**

After adding augmentation and dropout, the validation accuracy remained comparable (~62%) but the **validation loss decreased more steadily** (from ~2.38 to ~1.28), and the training accuracy no longer shot up to near-100%. This indicates the model is learning more robust features rather than memorizing data.

---

### Part 7: Model Improvement

**Q: What is the purpose of dropout layers?**

Dropout randomly deactivates a fraction of neurons (30% in this case) during each training step. This prevents individual neurons from becoming overly specialized, forcing the network to learn redundant representations and improving generalization.

**Q: Why does data augmentation improve generalization?**

Each epoch, the model sees slightly different versions of the same images. This is functionally equivalent to having a larger dataset, and it prevents the model from associating a specific background, angle, or lighting condition with a class label.

---

### Part 8: Performance Comparison

| Metric | Initial Model | Improved Model |
|--------|--------------|----------------|
| Epochs | 10 | 15 |
| Final Train Accuracy | 99.98% | 63.00% |
| Final Val Accuracy | **64.56%** | **62.16%** |
| Final Train Loss | 0.0037 | 1.2172 |
| Final Val Loss | 2.4213 | 1.2831 |
| Overfitting | **Severe** | **Reduced** |
| Train–Val Accuracy Gap | ~35% | ~1% |

> **Key Insight:** The improved model's validation loss (1.28) is nearly **half** that of the initial model (2.42), showing that augmentation and dropout substantially improved generalization even with similar raw accuracy.

The technique that contributed most to improvement was **data augmentation** — it addressed the root cause of overfitting by increasing effective dataset variability.

---

Google Colab Link: https://colab.research.google.com/drive/1LSiaExbQ3SKB0UEVdjAJEYavydWr3-kW?usp=sharing

Google Dataset & Model Link: https://drive.google.com/drive/folders/1-LNikanTVxL_Rz3jN7jUkffZtsTjYU0J?usp=sharing
