# Packet-level Micro-behavior Classification with Convolutional Neural Networks (CNNs)

## Task
The objective of this project is to **classify individual network packets** into one of three traffic categories: **Tor, VPN, or regular traffic**. This is achieved by treating packet metadata and payload as structured, image-like inputs suitable for processing with a **Convolutional Neural Network (CNN)**.

---

## Implementation Ideas

### • Data Representation
- Each packet is represented as a **2D array**, where:
  - **Rows** correspond to features such as byte values, header fields, and payload sizes.
  - **Columns** denote segmented parts of the packet.
- This structure mimics the layout of an image, making it ideal for CNN input.

### • Model Architecture
- Use a well-established CNN architecture (e.g., **ResNet**, **VGG**) to process these packet "images".
- **Convolutional layers** extract local patterns and dependencies inherent in packet structures, improving the model’s ability to generalize.

### • Preprocessing
- Normalize byte values and scale other features to a fixed range (e.g., [0,1]).
- Reshape all packet representations into a consistent format (e.g., fixed-length arrays) to ensure uniform CNN input dimensions.

### • Training
- Train the CNN on a large, labeled dataset of packet instances.
- Employ **categorical cross-entropy** as the loss function for multi-class classification tasks.
- Use techniques like data shuffling, batch normalization, and dropout for better generalization.

### • Evaluation
- Evaluate model performance using:
  - **Accuracy**
  - **Precision-Recall**
  - **Confusion matrix**
- Separate evaluation per class (Tor, VPN, regular) to monitor model fairness and performance consistency.

---

## Problem Formulation
Given a time series of network traffic features, the goal is to:
1. **Predict the next step** in the feature sequence.
2. **Detect anomalies** based on significant prediction errors, which may suggest the presence of Tor or VPN traffic.

---

## Mathematical Formulation

- **Input**:
  - A sequence of traffic features:  
    $$ X = \{x_1, x_2, ..., x_T\}, \quad \text{where } x_t \in \mathbb{R}^d $$  
    Each \( x_t \) is a d-dimensional feature vector at time step t.

- **Model**:
  - A **Temporal Convolutional Network (TCN)** with parameters \( \theta \).

- **Output**:
  - Predicted next step:  
    $$ \hat{x}_{T+1} = T(X; \theta) $$

- **Anomaly Detection**:
  - An anomaly is flagged if the prediction error exceeds a threshold \( \delta \):  
    $$ \|\hat{x}_{T+1} - x_{T+1}\|_2 > \delta $$

- **Loss Function**:
  - Mean Squared Error (MSE):  
    $$ L(\hat{x}, x) = \frac{1}{T} \sum_{t=1}^{T} \|\hat{x}_t - x_t\|_2^2 $$

---

## Summary
This project combines the strengths of CNNs in local pattern recognition with structured traffic feature representation, offering a modern, effective approach to encrypted traffic classification and anomaly detection. It lays the groundwork for intelligent cybersecurity solutions capable of detecting anonymized communication in real-time environments.
