# Neural Network for Number Addition (TensorFlow/TFLearn)

## Project Overview
This project implements a neural network to perform arithmetic addition of two concatenated 2-digit numbers, trained using TensorFlow 1.7.0 and TFLearn. The model is designed for deployment on Android devices, demonstrating the process of training a regression model and exporting it for mobile inference.

## Problem Statement
Given two 2-digit numbers (e.g., 12 and 34), predict their sum (46) using a neural network that processes the individual digits through one-hot encoding.

## Dataset Generation
- **Synthetic Data Creation**: Generated 500 training samples
- **Input Representation**: Each digit is one-hot encoded (10-dimensional vector)
- **Input Features**: 20-dimensional vector (10 for first number + 10 for second number)
- **Target**: Sum of the two numbers (regression target)
- **Data Range**: Numbers from 00-99, sums from 0-198

## Methodology

### Data Preprocessing
- **One-Hot Encoding**: Converted each digit (0-9) to a 10-element binary vector
- **Concatenation**: Combined encodings of both numbers into a single input vector
- **Label Generation**: Computed actual sum for supervision

### Model Architecture
- **Input Layer**: 20 neurons (one-hot encoded digits)
- **Hidden Layer**: 10 neurons with linear activation
- **Output Layer**: 1 neuron with linear activation (regression output)
- **Loss Function**: Mean Squared Error (MSE)
- **Optimizer**: Adam with learning rate 0.001

### Training Process
- **Epochs**: 1000 iterations
- **Batch Processing**: Full batch training
- **Monitoring**: TensorBoard integration for visualization
- **Model Saving**: Checkpointing and final model export

### Model Export for Android
- **Graph Freezing**: Removed training operations for inference-only model
- **Format Conversion**: Saved as TensorFlow protocol buffer (.pb) for Android compatibility
- **Graph Definition**: Exported graph structure for mobile deployment

## Technical Skills Demonstrated
- **TensorFlow 1.x Expertise**: Working with legacy TensorFlow API
- **TFLearn Integration**: High-level neural network construction
- **Regression Modeling**: Continuous output prediction
- **Model Serialization**: Preparing models for production deployment
- **Synthetic Data Generation**: Creating training data programmatically
- **One-Hot Encoding**: Efficient categorical data representation

## Challenges and Solutions
- **Version Compatibility**: Managed TensorFlow 1.7.0 installation and dependencies
- **Memory Management**: Handled graph operations and session management
- **Model Optimization**: Ensured model size and complexity suitable for mobile devices
- **Data Representation**: Designed appropriate input encoding for numerical operations

## Results
- **Training Convergence**: Model learned to approximate addition function
- **Prediction Accuracy**: Demonstrated ability to predict sums within reasonable error bounds
- **Model Size**: Optimized for mobile deployment
- **Export Success**: Successfully generated Android-compatible model files

## Code Structure
- Data generation and preprocessing functions
- Neural network model definition using TFLearn
- Training loop with monitoring
- Model export and freezing utilities
- TensorBoard integration for visualization

## Libraries Used
- **TensorFlow 1.7.0**: Core deep learning framework
- **TFLearn**: High-level API for TensorFlow
- **NumPy**: Numerical computations and array operations
- **Random**: Synthetic data generation

## Applications
- **Educational Tool**: Demonstrating neural networks for arithmetic
- **Mobile AI**: Foundation for on-device computation
- **Sequence Learning**: Basis for more complex numerical operations
- **Embedded Systems**: Lightweight models for resource-constrained devices

This project showcases the ability to design, train, and deploy neural networks for practical applications, including the critical skill of preparing models for production environments like mobile platforms.