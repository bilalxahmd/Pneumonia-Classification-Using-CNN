# 🫁 Pneumonia Classification using CNN

This project implements a Convolutional Neural Network (CNN) using TensorFlow and Keras to detect pneumonia from chest X-ray images. The model is trained on the **Chest X-Ray Pneumonia** dataset from Kaggle and includes data augmentation, learning rate reduction, and evaluation using a validation dataset.

---

## 📂 Dataset
The dataset used for training and evaluation is the **Chest X-Ray Pneumonia** dataset, available on Kaggle:

- **Train Path:** `/content/chest_xray/train`
- **Test Path:** `/content/chest_xray/test`
- **Validation Path:** `/content/chest_xray/val`

### Dataset Classes:
- `PNEUMONIA` – Labeled as `0`
- `NORMAL` – Labeled as `1`

---

## 🚀 Model Architecture
The CNN model consists of the following layers:
1. **Convolutional Layers** – Extracts features using 2D convolutions with `ReLU` activation.
2. **Batch Normalization** – Improves training stability and convergence.
3. **MaxPooling Layers** – Reduces spatial dimensions.
4. **Dropout Layers** – Reduces overfitting.
5. **Dense Layers** – Fully connected layers for classification.

### 🔹 Model Summary:
```python
Model: "sequential"
_________________________________________________________________
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━┓
┃ Layer (type)                         ┃ Output Shape                ┃         Param # ┃
┡━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━━━━━┩
│ conv2d_3 (Conv2D)                    │ (None, 150, 150, 32)        │             320 │
├──────────────────────────────────────┼─────────────────────────────┼─────────────────┤
│ batch_normalization                  │ (None, 150, 150, 32)        │             128 │
│ (BatchNormalization)                 │                             │                 │
├──────────────────────────────────────┼─────────────────────────────┼─────────────────┤
│ max_pooling2d_3 (MaxPooling2D)       │ (None, 75, 75, 32)          │               0 │
├──────────────────────────────────────┼─────────────────────────────┼─────────────────┤
│ conv2d_4 (Conv2D)                    │ (None, 75, 75, 64)          │          18,496 │
├──────────────────────────────────────┼─────────────────────────────┼─────────────────┤
│ dropout_1 (Dropout)                  │ (None, 75, 75, 64)          │               0 │
├──────────────────────────────────────┼─────────────────────────────┼─────────────────┤
│ batch_normalization_1                │ (None, 75, 75, 64)          │             256 │
│ (BatchNormalization)                 │                             │                 │
├──────────────────────────────────────┼─────────────────────────────┼─────────────────┤
│ max_pooling2d_4 (MaxPooling2D)       │ (None, 38, 38, 64)          │               0 │
├──────────────────────────────────────┼─────────────────────────────┼─────────────────┤
│ conv2d_5 (Conv2D)                    │ (None, 38, 38, 64)          │          36,928 │
├──────────────────────────────────────┼─────────────────────────────┼─────────────────┤
│ batch_normalization_2                │ (None, 38, 38, 64)          │             256 │
│ (BatchNormalization)                 │                             │                 │
├──────────────────────────────────────┼─────────────────────────────┼─────────────────┤
│ max_pooling2d_5 (MaxPooling2D)       │ (None, 19, 19, 64)          │               0 │
├──────────────────────────────────────┼─────────────────────────────┼─────────────────┤
│ conv2d_6 (Conv2D)                    │ (None, 19, 19, 128)         │          73,856 │
├──────────────────────────────────────┼─────────────────────────────┼─────────────────┤
│ dropout_2 (Dropout)                  │ (None, 19, 19, 128)         │               0 │
├──────────────────────────────────────┼─────────────────────────────┼─────────────────┤
│ batch_normalization_3                │ (None, 19, 19, 128)         │             512 │
│ (BatchNormalization)                 │                             │                 │
├──────────────────────────────────────┼─────────────────────────────┼─────────────────┤
│ max_pooling2d_6 (MaxPooling2D)       │ (None, 10, 10, 128)         │               0 │
├──────────────────────────────────────┼─────────────────────────────┼─────────────────┤
│ conv2d_7 (Conv2D)                    │ (None, 10, 10, 256)         │         295,168 │
├──────────────────────────────────────┼─────────────────────────────┼─────────────────┤
│ dropout_3 (Dropout)                  │ (None, 10, 10, 256)         │               0 │
├──────────────────────────────────────┼─────────────────────────────┼─────────────────┤
│ batch_normalization_4                │ (None, 10, 10, 256)         │           1,024 │
│ (BatchNormalization)                 │                             │                 │
├──────────────────────────────────────┼─────────────────────────────┼─────────────────┤
│ max_pooling2d_7 (MaxPooling2D)       │ (None, 5, 5, 256)           │               0 │
├──────────────────────────────────────┼─────────────────────────────┼─────────────────┤
│ flatten_1 (Flatten)                  │ (None, 6400)                │               0 │
├──────────────────────────────────────┼─────────────────────────────┼─────────────────┤
│ dense_2 (Dense)                      │ (None, 128)                 │         819,328 │
├──────────────────────────────────────┼─────────────────────────────┼─────────────────┤
│ dropout_4 (Dropout)                  │ (None, 128)                 │               0 │
├──────────────────────────────────────┼─────────────────────────────┼─────────────────┤
│ dense_3 (Dense)                      │ (None, 1)                   │             129 │
└──────────────────────────────────────┴─────────────────────────────┴─────────────────┘
 Total params: 1,246,401 (4.75 MB)
 Trainable params: 1,245,313 (4.75 MB)
 Non-trainable params: 1,088 (4.25 KB)   
=================================================================
```
## 📈 Data Augmentation
To improve generalization and reduce overfitting, **data augmentation** was applied using the `ImageDataGenerator` from Keras. The following augmentations were applied:

✅ **Rotation:** Up to 30 degrees  
✅ **Zoom:** Up to 20%  
✅ **Width and Height Shift:** Up to 10%  
✅ **Horizontal Flip**  

```python
datagen = ImageDataGenerator(
    rotation_range=30,
    zoom_range=0.2,
    width_shift_range=0.1,
    height_shift_range=0.1,
    horizontal_flip=True
)
```
## 🏋️‍♂️ Training
The model was compiled using the following settings:

- **Optimizer:** `RMSprop`  
- **Loss Function:** `Binary Crossentropy`  
- **Metrics:** `Accuracy`  

### 🔹 Learning Rate Reduction:
A `ReduceLROnPlateau` callback was implemented to reduce the learning rate if the validation accuracy stopped improving:

```python
learning_rate_reduction = ReduceLROnPlateau(
    monitor='val_accuracy', 
    patience=2, 
    verbose=1, 
    factor=0.3, 
    min_lr=0.000001
)
```

### 🔹 Learning Command:
```python
history = model.fit(
    datagen.flow(X_train, y_train, batch_size=32),
    epochs=12,
    validation_data=datagen.flow(X_val, y_val),
    callbacks=[learning_rate_reduction]
)
```
## 🎯 Results
### ✅ Test Accuracy:
Achieved test accuracy of exactly **91.35%**.

### 📊 Confusion Matrix:
![image](https://github.com/user-attachments/assets/2d4a99a6-76d3-47b9-8a48-bf71c44b9c49)

### 📉 Training and Validation Accuracy:
Training and validation accuracy plots show consistent learning behavior without overfitting.

### 🏆 Performance Metrics
**Train Accuracy:** 97.65%
**Validation Accuracy:** 81.25%
**Test Accuracy:** 91.35%
**FI-Score:** Macro Avg = 0.90, Weighted Avg = 0.91

### 📄 Classification Report:
```python
              precision    recall  f1-score   support

           0       0.89      0.98      0.93       390
           1       0.95      0.81      0.88       234

    accuracy                           0.91       624
   macro avg       0.92      0.89      0.90       624
weighted avg       0.92      0.91      0.91       624

```

## 📌 To-Do
- ✅ Improve data augmentation strategies
- ✅ Test on a larger dataset
- ✅ Try different optimizers (Adam, SGD)
- ✅ Using Regularization techniques to enhance accuracy
- ✅ Adding Dropout Layers and making use of early stopping
