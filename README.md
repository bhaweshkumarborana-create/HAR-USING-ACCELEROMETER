# HAR-USING-ACCELEROMETER
Human Activity Recognition using accelerometer data and SVM, leveraging DSP techniques for signal preprocessing, feature extraction, and accurate classification of daily activities such as walking, sitting, standing, and running.
# Human Activity Recognition Using Accelerometer and SVM

## 📌 Project Overview

This project implements **Human Activity Recognition (HAR)** using tri-axial accelerometer data from the UCI Human Activity Recognition Using Smartphones dataset. Digital Signal Processing (DSP) techniques are applied to preprocess sensor signals and extract meaningful time-domain and frequency-domain features. A multiclass Support Vector Machine (SVM) with an RBF kernel is used to classify six human activities.

The project uses MATLAB for signal processing, feature extraction, model training, prediction, and performance evaluation.

## 🎯 Objectives

- Process accelerometer signals using DSP techniques.
- Apply a Butterworth low-pass filter to reduce high-frequency noise.
- Extract statistical and frequency-domain features using FFT.
- Train a multiclass SVM classifier.
- Evaluate classification performance using accuracy, macro F1-score, and a confusion matrix.
- Understand the application of machine learning in wearable-sensor activity recognition.

## 🛠️ Technologies Used

- MATLAB
- Digital Signal Processing (DSP)
- Fast Fourier Transform (FFT)
- Butterworth Low-Pass Filter
- Support Vector Machine (SVM)
- UCI HAR Dataset

## 📂 Dataset

The project uses the **UCI Human Activity Recognition Using Smartphones Dataset**, which contains smartphone sensor recordings collected from human participants performing different physical activities.

Dataset: [UCI HAR Dataset — UCI Machine Learning Repository](https://archive.ics.uci.edu/dataset/240/human+activity+recognition+using+smartphones)

The implementation uses the following files:

- `body_acc_x_train.txt`
- `body_acc_y_train.txt`
- `body_acc_z_train.txt`
- `total_acc_x_train.txt`
- `total_acc_y_train.txt`
- `total_acc_z_train.txt`
- Corresponding test files
- `X_train.txt`, `y_train.txt`, `X_test.txt`, and `y_test.txt`

The inertial signal files contain pre-segmented windows sampled at **50 Hz**. The supplied dataset's training and test partitions are used separately.

### Activity Classes

| Label | Activity |
|---|---|
| 1 | WALKING |
| 2 | WALKING UPSTAIRS |
| 3 | WALKING DOWNSTAIRS |
| 4 | SITTING |
| 5 | STANDING |
| 6 | LAYING |

## ⚙️ Methodology

### 1. Signal Preprocessing

The inertial signals are loaded from the dataset. A fourth-order Butterworth low-pass filter with a cutoff frequency of 20 Hz is applied using MATLAB's `butter()` and `filtfilt()` functions.

- Sampling frequency: 50 Hz
- Filter type: Butterworth low-pass
- Filter order: 4
- Cutoff frequency: 20 Hz
- Body acceleration: Mean removal followed by filtering
- Total acceleration: Filtering without explicit DC removal to preserve gravity-related information

### 2. Feature Extraction

Time-domain and frequency-domain features are extracted from the acceleration signals.

**Time-domain features**
- Mean
- Standard deviation
- Root Mean Square (RMS)
- Maximum and minimum
- Range
- Median
- Interquartile range (IQR)
- Skewness
- Kurtosis
- Mean absolute value
- Zero-crossing rate

**Frequency-domain features**
- Dominant frequency
- Spectral energy
- Frequency-band energies:
  - 0–3 Hz
  - 3–6 Hz
  - 6–10 Hz
  - 10–20 Hz
- Spectral entropy

FFT is used to analyze the frequency characteristics of the signals.

### 3. Acceleration Magnitude

The resultant acceleration magnitude is calculated from the three axes:

\[
a_{\text{mag}}=\sqrt{a_x^2+a_y^2+a_z^2}
\]

Both body acceleration magnitude and total acceleration magnitude are included in the feature extraction pipeline.

### 4. Feature Normalization

Features are standardized using the training dataset's mean and standard deviation:

\[
X_{\text{norm}}=\frac{X-\mu_{\text{train}}}{\sigma_{\text{train}}}
\]

The same training normalization parameters are applied to the test features to maintain consistency.

### 5. SVM Classification

A multiclass SVM is trained using MATLAB's `fitcecoc()` function with an RBF kernel and a one-vs-one classification strategy.

Model configuration:

- Classifier: Support Vector Machine
- Kernel: Radial Basis Function (RBF)
- Kernel scale: Automatic
- Box constraint: 10
- Multiclass strategy: One-vs-one
- Number of activity classes: 6

The model predicts the activity associated with each test sample.

## 📊 Evaluation Metrics

The trained model is evaluated using:

- **Accuracy:** Percentage of correctly classified samples.
- **Precision:** Proportion of predicted positive samples that are correct, calculated per class.
- **Recall:** Proportion of actual class samples correctly identified.
- **Macro F1-score:** Average of the F1-scores across the six activity classes.
- **Confusion Matrix:** Shows correct classifications and misclassifications for each activity.

The MATLAB implementation generates a confusion matrix visualization and displays the overall classification accuracy and macro F1-score.

Actual performance values should be obtained by running the scripts.

## 🔄 Project Workflow

```text
UCI HAR Dataset
       |
       v
Load Accelerometer Signals
       |
       v
Signal Preprocessing
(DC Removal and Filtering)
       |
       v
Magnitude Calculation
       |
       v
Feature Extraction
(Time Domain + FFT)
       |
       v
Feature Normalization
       |
       v
Multiclass RBF-SVM
       |
       v
Activity Prediction
       |
       v
Accuracy, Macro F1 and
Confusion Matrix
```

## 📁 Repository Structure

```text
Human-Activity-Recognition-SVM/
│
├── UCI HAR Dataset/
│   ├── train/
│   │   ├── Inertial Signals/
│   │   ├── X_train.txt
│   │   └── y_train.txt
│   └── test/
│       ├── Inertial Signals/
│       ├── X_test.txt
│       └── y_test.txt
│
├── extract_training_features.m
├── extract_test_features.m
├── train_svm.m
├── README.md
└── .gitignore
```

*The filenames above are suggested names; adjust them to match the actual files in your repository.*

## ▶️ How to Run

### Prerequisites

- MATLAB
- Signal Processing Toolbox
- Statistics and Machine Learning Toolbox
- UCI HAR Dataset downloaded and extracted

### Steps

1. Clone or download this repository.
2. Download the UCI HAR Dataset from the official source linked above.
3. Extract the dataset into the project directory.
4. Ensure the dataset paths in the MATLAB scripts are correct.
5. Run the training feature extraction script.
6. Run the test feature extraction script.
7. Run the SVM training and evaluation script.
8. View the classification accuracy, macro F1-score, and confusion matrix in MATLAB.

**Important:** The supplied feature-extraction scripts generate custom FFT-based features, while the SVM script shown here trains on the dataset's existing `X_train.txt` and `X_test.txt` feature matrices. These are two separate feature pipelines. To evaluate the custom DSP features with SVM, modify the training script to load `training_features.mat` and `test_features.mat` instead.

## 🚀 Applications

- Fitness and physical activity monitoring
- Smartphone-based activity recognition
- Wearable health-monitoring systems
- Context-aware mobile applications
- Human movement analysis
- Assisted-living and activity-monitoring research

## 🔮 Future Improvements

- Train and evaluate the SVM using the custom FFT-based features.
- Compare linear, polynomial, and RBF kernels.
- Perform systematic hyperparameter tuning.
- Add cross-validation and class-wise performance reports.
- Test generalization across different participants.
- Explore real-time activity recognition using smartphone sensors.
- Compare SVM performance with other machine-learning classifiers.

## 👨‍💻 Project Information

**Project:** Human Activity Recognition Using Accelerometer and SVM  
**Domain:** Digital Signal Processing and Machine Learning  
**Language:** MATLAB  
**Dataset:** UCI Human Activity Recognition Using Smartphones

## 📜 License

Add an appropriate license to the repository if you intend to distribute or reuse the project code.

## 🙏 Acknowledgment

We acknowledge the researchers who developed and published the UCI Human Activity Recognition Using Smartphones dataset for making it available for research and educational purposes.
