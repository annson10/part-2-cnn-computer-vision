# Part 2: Computer Vision Problem Formulation and CNN Prototype

## Objective
The objective of this project is to build a Convolutional Neural Network (CNN) to classify manufacturing product images into four categories: normal, scratch, dent, and stain.

## Dataset Source
The dataset was provided as part of the assignment materials and can be downloaded from:

https://drive.google.com/drive/folders/1akV6po4Nrgkc3yQrJkzA6cJlV-wBvUYs?usp=sharing

The dataset is provided as a ZIP file containing an `images/` folder and `labels.csv`.

### Classes
- `normal` – Product surface without major defect
- `scratch` – Product surface with scratch-like marks
- `dent` – Product surface with circular dent-like marks
- `stain` – Product surface with colored stain-like marks

## Problem Type
This is an image classification problem because each image belongs to exactly one class.


## Methodology

### 1. Problem Identification
The dataset was identified as an image classification task because each image has a single label representing the overall condition of the product surface.

### 2. Dataset Exploration
- Counted the number of classes
- Calculated the number of images per class
- Displayed sample images from each class
- Checked image dimensions
- Examined class balance

### 3. Image Preprocessing
- Resized all images to 128 × 128 pixels
- Normalized pixel values to the range [0, 1]
- Split data into training and validation sets
- Applied data augmentation:
  - Rotation
  - Zoom
  - Horizontal flipping
  - Width and height shifts

### 4. CNN Model Creation
CNN Architecture:
- Conv2D (32 filters, 3×3, ReLU)
- MaxPooling2D (2×2)
- Conv2D (64 filters, 3×3, ReLU)
- MaxPooling2D (2×2)
- Conv2D (128 filters, 3×3, ReLU)
- MaxPooling2D (2×2)
- Flatten
- Dense (128 neurons, ReLU)
- Dropout (0.5)
- Output Dense (4 neurons, Softmax)

Loss Function:
- Categorical Crossentropy

Optimizer:
- Adam

### 5. Model Training
- Trained for up to 20 epochs
- Used early stopping to prevent overfitting
- Monitored validation loss

### 6. Evaluation
- Training accuracy and loss
- Validation accuracy and loss
- Classification report
- Confusion matrix
- Sample predictions on validation images   

## Results
The model successfully learned to distinguish between normal surfaces and defective surfaces.

Performance was evaluated using:
- Accuracy
- Precision
- Recall
- F1-score
- Confusion matrix

The generated outputs include:
- `results/accuracy_loss_curves.png`
- `results/confusion_matrix.png`
- `sample_predictions/prediction_outputs.png`



## CNN Concept Explanation

### What is convolution?
Convolution is the process of applying a small filter ( kernel) to an image to detect important patterns such as edges, corners, textures, and shapes.

The filter slides across the image and performs element-wise multiplication with the pixel values. The result is a feature map that highlights specific visual patterns.

For example:
- Early layers may detect edges and lines.
- Middle layers may detect textures or defect shapes.
- Deeper layers may detect complex objects such as scratches or dents.

### Why is pooling used?
Pooling is used to reduce the size of feature maps while preserving the most important information.

The most common type is **Max Pooling**, which selects the maximum value from a small region (for example, 2×2).

Benefits of pooling:
- Reduces computational cost
- Reduces the number of parameters
- Helps prevent overfitting
- Makes the model more robust to small shifts in the image

### Why is ReLU commonly used?
ReLU (Rectified Linear Unit) is an activation function defined as:

f(x) = max(0, x)

It replaces negative values with zero and keeps positive values unchanged.

Advantages of ReLU:
- Introduces non-linearity
- Computationally efficient
- Helps reduce the vanishing gradient problem
- Speeds up model training

### Why are CNNs better than feed-forward networks for images?
CNNs preserve spatial relationships and require far fewer parameters by sharing weights.

CNNs are specifically designed to process images.

#### 1. Preserve Spatial Relationships
CNNs analyze local regions of an image, allowing them to capture spatial patterns such as edges and shapes.

#### 2. Weight Sharing
The same filter is applied across the entire image, greatly reducing the number of parameters.

#### 3. Translation Invariance
CNNs can recognize features even if they appear in different positions.

#### 4. Automatic Feature Extraction
CNNs learn useful features directly from raw pixel values, eliminating the need for manual feature engineering.

In contrast, regular feed-forward networks flatten the image into a long vector, which loses spatial structure and requires a much larger number of parameters.



## Business Use Case Mapping

### Manufacturing Quality Inspection

This CNN can be used in manufacturing to automatically detect product defects such as scratches, dents, and stains.

Traditionally, quality inspection is performed manually by human inspectors, which can be time-consuming, expensive, and prone to inconsistency. A CNN-based image classification model can analyze images captured by cameras on the production line and classify each product as either normal or defective.

If a defect is detected, the system can automatically remove the product from the production line or alert operators for further inspection.

Benefits include:
- Ensures consistent quality standards
- Improves inspection speed and efficiency
- Reduced human error
- Lower labor costs
- Improved product quality
- Real-time defect detection on production lines

### Real-World Impact

Manufacturers in industries such as automotive, electronics, and consumer goods can use this technology to maintain high product quality while increasing productivity and reducing operational costs.



## Key Findings
- CNNs effectively learned defect patterns from images.
- Data augmentation improved model generalization.
- Early stopping reduced overfitting.
- Manufacturing quality inspection is a practical real-world application.



## How to Run
1. Install dependencies:
   ```bash
   pip install -r requirements.txt