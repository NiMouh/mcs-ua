# Spam

## Numerical stability
Numerical instability is a concept that refers to the propensity of an algorithm or computational procedure to produce inaccurate results due to round-off errors, truncation errors, or other computational issues.

## NLTK
NLTK is a leading platform for building Python programs to work with human language data.

**Tokenization** is the process of tokenizing or splitting a string, text into a list of tokens.

**Lemmatization** is the process of grouping together the different inflected forms of a word so they can be analyzed as a single item.

**Stemming** is the process of reducing inflected (or sometimes derived) words to their word stem, base or root form.

## Text-mining
Text mining is the process of deriving high-quality information from text.

### Term Frequency
Term frequency is the measurement of how frequently a term occurs within a document.

### Data visualization
There are two traditional visualizations for textual data:
- Bar plots (for frequency and ranking)
- WordClouds: are graphical representations of word frequency that give greater prominence to words that appear more frequently in a source text. The larger the word in the visual the more common the word was in the document(s).

### TF-IDF
TF-IDF (term frequency-inverse document frequency) is a statistical measure that evaluates how relevant a word is to a document in a collection of documents.

This is done by multiplying two metrics: how many times a word appears in a document, and the inverse document frequency of the word across a set of documents.

### Blind Optimization
Blind optimization is the process of finding the best solution to a problem without having any idea of how good that solution is.

Examples of blind optimization algorithms are:
- Genetic Evolution
- Differential Evolution
- Particle Swarm Optimization: is best used to find the maximum or minimum of a function defined on a multidimensional vector space.

### Gradient Descent
A very simple and powerfull algorithm that is used to find a local minimum of a function.

### Logistic Regression
Logistic regression estimates the probability of an event occurring, such as voted or didn't vote, based on a given dataset of independent variables. It's good for binary classification.

### Classification
There are perhaps three main types of classification tasks that you may encounter; they are:
- **Binary Classification**: those classification tasks that have two class labels (i.e. spam or not spam).
- **Multi-Class Classification**: those classification tasks that have more than two class labels (i.e. what type of spam?)
- **Multi-Label Classification**: those classification tasks that have two or more class labels, where one or more class labels may be predicted for each example (i.e. spam and urgent).

# Anomaly Detection
Anomaly detection is the identification of abdnormal data points within a dataset.

Anomaalies can be broadly categorized as:

- Point anomalies: A single instance of data is anomalous if it's too far off from the rest. Business use case: Detecting credit card fraud based on "amount spent."
- Contextual anomalies: The abnormality is context specific. This type of anomaly is common in time-series data. Business use case: Spending $100 on food every day during the holiday season is normal, but may be odd otherwise.
- Collective anomalies: A set of data instances collectively helps in detecting anomalies. Business use case: Someone is trying to copy data form a remote machine to a local host unexpectedly, an anomaly that would be flagged as a potential cyber attack.

## Unsupervised Learning
Unsupervised learning is where you only have input data (X) and no corresponding output variables (no labeled data).

## Clustering
The task of dividing the population or data points into a number of groups such that data points in the same groups are more similar to other data points in the same group than those in other groups.

Clustering algorithms:
- K-Means
- Gaussian Mixture Models
- DBSCAN
- Hierarchical Clustering

## Density-Based Anomaly Detection
Density-Based Anomaly Detection is based on the k-nearest neighbors algorithm. It is a non-parametric method for detecting the presence of outliers in a given dataset.

## SVM (Support Vector Machine)
A support vector machine is another effective technique for detecting anomalies. A SVM is typically associated with supervised learning, but there are extensions (OneClassCVM, for instance) that can be used to identify anomalies as an unsupervised problems.

## Isolation Forest Algorithm
The algorithm is based on the fact that anomalies are data points that are few and different. As a result of these properties, anomalies are susceptible to a mechanism called isolation.

## Autoencoders
An autoencoder is a type of artificial neural network used to learn efficient data codings in an unsupervised manner.

It's composed of two parts:
- Encoder: The encoder part of an autoencoder transforms the input data into a compressed representation.
- Bottleneck: The compressed representation of the input data.
- Decoder: The decoder part of an autoencoder transforms the compressed representation into the reconstructed data.

## Confusion Matrix
A confusion matrix is a table that is often used to describe the performance of a classification model (or "classifier") on a set of test data for which the true values are known.

It's a 2x2 matrix:
- True Positive: The number of correct predictions that the occurrence is positive.
- True Negative: The number of correct predictions that the occurrence is negative.
- False Positive: The number of incorrect predictions that the occurrence is positive.
- False Negative: The number of incorrect predictions that the occurrence is negative.

From the confusion matrix, we can calculate:
- the accuracy (TP+TN/TP+TN+FP+FN)
- precision (TP/TP+FP)
- recall (TP/TP+FN)
- F1 score (2*precision*recall/precision+recall).

## Recall vs Precision
- Recall: Out of all the positive classes, how much we predicted correctly. It should be high as possible.
- Precision: Out of all the positive classes we have predicted correctly, how many are actually positive. It should be high as possible.

# Malware

**Malware**, or malicious software, is any program or file that is **intentionally harmful** to a computer, network or server. Usually it´s analyzed **binary files** rather than **executable files** (.exe) since malware can be hidden in any type of file, being them a vehicle for malware delivery or **healthy carriers**.

## History of malware
- **Creeper** (1971): Creeper did no harm to the systems it infected - Thomas developed it as a proof of concept, and its only effect was that it caused connected teletype machines to print a message that said “I’M THE CREEPER: CATCH ME IF YOU CAN.”
- **ILOVEYOU** (2000): a **worm** that would steal other people’s passwords so he could piggyback off of their accounts.
- **CryptoLocker** (2013): a ransomware trojan that targeted computers running Windows.
- **Mirai** (2016): a **botnet** that targeted Internet of Things (IoT) devices such as routers, security cameras and DVRs.
- **Clop** (2019): a **ransomware** that encrypts files on a victim’s computer and demands a ransom to decrypt them.

## Types of malware

### Ransomware
**Ransomware** is a type of malware that **encrypts** a victim's files. The attacker then demands a ransom from the victim to restore access to the data upon payment.

### Botnet
A **botnet** is a number of Internet-connected devices, each of which is running one or more bots. Botnets can be used to perform distributed denial-of-service attack (DDoS attack), steal data, send spam, and allows the attacker to access the device and its connection.

### Worm
**Worm** is a type of malware that **replicates** itself and spreads to other computers through network connections.

### Trojan
**Trojan** is a type of malware that is often disguised as legitimate software. Trojans can be employed by cyber-thieves and hackers trying to gain access to users' systems.

### Zero-day
**Zero-day** is a type of malware that exploits a **software vulnerability** that is unknown to the software developer or vendor. The term "zero-day" refers to the unknown nature of the hole to those outside of the hackers, specifically, the developers.

### APT (Advanced Persistent Threat)
**APT** is a type of malware that is designed to gain **unauthorized access** to a computer system, and remain undetected for a long period of time.

### Downloader
**Downloader** is a type of malware that is designed to download and install other malware, typically through a backdoor.

## Magic Numbers
**Magic numbers** are the **first few bytes** of a file that **identify** the **type of file**. They are also called **file signatures**.

## Malware in Windows OS

### PE Files

PE files are **Windows executable files**. Consists in a **header** and **section table** followed by **sections**.

### PE Header

The **PE file header** is encapsulated in the **Windows NT header structure** (defined in the winnt.h header file, along with other C structures) and is composed of the following:

- **MS DOS header**
- **The PE signature**
- **The image file header**
- **An optional header**

### PE Sections
PE sections are **parts of a PE file**. Each section can be thought as a folder, hosting various binary objects.

## Tools to detect malware

These tools can be categorized as follows:
- **Disassemblers**;
- **Debuggers**;
- **System monitors** (such as Process Monitor and Process Explorer);
- **Network monitors** (such as Wireshark and tcpdump)
- **Unpacking tools and Packer Identifiers**;
- **Binary and code analysis tools** (such as PE Explorer);

## How to recognize malware

1. **Signature-based detection:** Identifies malware based on known digital indicators, but they are reactive because they rely on known malware signatures. This means that they can only detect malware that has already been identified and analyzed.

2. **Static file analysis:** Examines a file's code without execution, looking for signs of malicious intent in file names, hashes, and other data.

3. **Dynamic malware analysis:** Executes suspected malicious code in a secure environment (sandbox) to observe and study malware behavior without risking infection.

4. **Dynamic monitoring of mass file operations:** Observes mass file operations for signs of tampering or corruption, utilizing file integrity monitoring tools.

5. **File extensions blocklist:** Prevents the download or use of dangerous files by listing known malicious file extensions.

6. **Application allowlist:** Authorizes approved applications, reducing the risk of nefarious applications but potentially impacting operational speed and flexibility.

7. **Malware honeypot:** Simulates a safe environment to draw out and analyze malware attacks, aiding in the development of antimalware solutions.

8. **Cyclic redundancy check (CRC):** Checks data integrity through calculations, though it is not foolproof against tampering.

9.  **File entropy:** Identifies potential malware by measuring data changes in files, particularly those with high entropy levels.

10. **Machine learning analysis:** Uses machine learning algorithms to analyze file behavior, identify patterns, and improve detection of novel and unidentified malware.

## Malware Detection
The collected data used to malware recognition is collected at different phases:
- **Pre-execution phase data**: Information about a file obtained without executing it. This includes details such as executable file format, code descriptions, binary data statistics, text strings, and information extracted through code emulation. Essentially, it encompasses everything known about a file before it is run.

- **Post-execution phase data**: Information that reveals the behavior or events resulting from a file's activity within a system. This data is collected after the file has been executed and provides insights into the consequences of the file's actions on the system.

## Machine learning approaches

- **Unsupervised learning**: Large unlabeled datasets are available to cybersecurity vendors and the cost of their manual labeling by experts is high.

- **Supervised learning**: The goal is to fit the model that will produce the right answers for new objects. This approach consists of two stages, training the model and fitting the model and applying the trained model to new samples.

For training: The **X** could be some **features or behaviours of the file**, and **y** could be the **label of the file** (i.e. malware or benign in binary classification or malware family in multi-class classification).

## Requirements

- **Deep Learning** is a special machine learning approach that facilitates the extraction of features of a high level of abstraction from low-level data. It can learn complex feature hierarchies and incorporate diverse steps of malware detection pipeline into one solid model that can be trained end-to-end;
- **Large representative datasets**;
- **The trained model has to be interpretable** (XAI): most model families used are called **black box models**. They are given the input X, and they will produce Y through a complex sequence of operations that can hardly be interpreted by a human.
- **False positive rates must be low**.
- **Model must be able to adapt to new malware families and new benign software**.

## Multi-class classification

Multi-class classification is the problem of classifying instances into one of **three or more classes**.

### One-vs-Rest (One-vs-All)

**Splits** the **multi-class dataset** into **multiple binary classification problems** and uses them to train the binary classifier and predict the results.

Example: 
- Binary Classification Problem 1: red vs [blue, green]
- Binary Classification Problem 2: blue vs [red, green]
- Binary Classification Problem 3: green vs [red, blue]

### One-vs-one
It involves fitting **one binary classifier** **per class pair**. If there are N classes in the dataset, then there are `N * (N - 1) / 2` binary classifiers that are trained.

Example:
- Binary Classification Problem 1: red vs. blue
- Binary Classification Problem 2: red vs. green
- Binary Classification Problem 3: red vs. yellow
- Binary Classification Problem 4: blue vs. green
- Binary Classification Problem 5: blue vs. yellow
- Binary Classification Problem 6: green vs. yellow

## Libraries

### Pandas library
Pandas is a library for **data manipulation** and **analysis**, it's used to read and write data in csv files.

The **iloc function** is part of pandas and is used as an indexing tool for csv datasets, first argument is the row and second argument is the column `df.iloc[row, column].values`.

### Scikit-learn library
Scikit-learn is a library used for **machine learning algorithms**.

*Imputer* is a transformer for completing missing values, it replaces missing values with the mean value of the column.

## Classes Distribution
The classes distribution is the number of **samples** **for each class**.

## Features visualization
The features visualization is the number of **features** **for each class**.

## Feature Scaling

Feature scaling is a method used to **normalize the range of independent variable**s or **features** of data. In data processing, it is also known as data normalization and is generally performed during the data preprocessing step.

An example of scaling is to normalize by:
```
scaled_value = (value - mean) / standard_deviation
```
which falls in the range of -4 to 4.

Another example is Min-Max scaling:
```
scaled_value = (value - min) / (max - min)
```
which falls in the range of 0 to 1.

## Label Encoding

Label encoding is a popular encoding technique for handling **categorical variables**. In this technique, each label is assigned a unique integer based on alphabetical ordering.

Example:
```
blue: 0
green: 1
red: 2
```

## One-hot Encoding

One-hot encoding is a technique used to convert **categorical variables** into **binary vectors**. It is called one-hot because only one feature is 1 while the others are 0.

Example:
```
0: 0 0 1
1: 0 1 0
2: 1 0 0
```

## Keras Classifier
Keras works by creating a neural network model, compiling it with an optimizer and loss function, training it on labeled data, and then using the trained model to make predictions on new data.

## Evaluation Metrics

### Confusion Matrix
It´s composed of 4 different values:
- True Positive (TP): the model correctly predicts the positive class.
- True Negative (TN): the model correctly predicts the negative class.
- False Positive (FP): the model incorrectly predicts the positive class.
- False Negative (FN): the model incorrectly predicts the negative class.

### Accuracy
Accuracy is the ratio of correctly predicted observation to the total observations `TP + TN / TP + TN + FP + FN`

### Precision
Precision is the ratio of correctly predicted positive observations to the total predicted positive observations `TP / TP + FP`

### Recall
Recall is the ratio of correctly predicted positive observations to the all observations in actual class `TP / TP + FN`

### F1-score
F1-score is the weighted average of Precision and Recall `2 * Precision * Recall / Precision + Recall`

### Squared Error
Squared error is the **difference** between the **predicted value** and the **actual value**, squared.

### MCC
MCC is the **correlation coefficient** between the observed and **predicted binary classifications**. It returns a value between -1 and 1. A coefficient of +1 represents a perfect prediction, 0 represents a random prediction and -1 represents an inverse prediction.

### ROC curve
ROC curve is a plot of the **true positive rate** (TPR) against the **false positive rate** (FPR), as the false positive rate increases, how much the true positive rate increases.

The area under the curve (AUC) is a measure of how well a parameter can **distinguish between two diagnostic groups**, if the AUC is 0.5, the parameter is totally random, if the AUC is 1, the parameter is perfect.

### Loss curves (Training and Validation)
The loss function is a measure of how well a machine learning model is able to **predict** the expected outcome. **The lower** the loss, **the better** the model is at predicting the outcome.

### Mcnemar's Statistical Test
McNemar test should be used for obtaining a probability of difference between the cases of false negative and false positives, to **compare two classifiers**.

Can be represented by a **contingency table**:

    A. both models predict correctly
    B. model 1 predicts correctly, model 2 predicts incorrectly
    C. model 1 predicts incorrectly, model 2 predicts correctly
    D. both models predict incorrectly

P-value is the probability of obtaining a test statistic at least as extreme as the one that was actually observed, assuming that the null hypothesis is true. if the p-value is **less than the significance level**, there is a **significant difference** between the two classifiers.

### Feature Importance
Feature importance assigns a **score to input features** based on how **useful they are at predicting** a target variable.

In each model:
- Logistic Regression: the coefficients of the model;
- Decision Tree: importance scores based on the reduction in the criterion used to select split points, like Gini or entropy;
- CART (Classification and Regression Trees): after being fit, the model provides a feature importances property;

