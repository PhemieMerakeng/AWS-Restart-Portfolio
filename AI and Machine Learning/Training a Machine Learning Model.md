## Training a Machine Learning Model
---
### Project Overview 

This project builds a machine learning model that helps doctors detect spinal abnormalities in patients. The model learns from 310 past patient records, each containing six spine measurements and a diagnosis. After training, the model can take new patient measurements and predict whether they have a spinal condition that needs medical attention.

The model uses XGBoost, a powerful machine learning algorithm, and runs on Amazon SageMaker, a cloud platform that provides the computing power and tools needed for training.

#### Amazon SageMaker
A cloud-based platform from Amazon Web Services (AWS) designed specifically for building and training machine learning models. It provides pre-configured computers, built-in algorithms, and managed storage so you don't need to set up your own infrastructure.

#### JupyterLab
An interactive notebook environment that runs inside SageMaker. It allows you to write code, see results immediately, and add explanations in a single document

#### Notebook Instance
A SageMaker notebook instance is a machine learning (ML) compute instance running the Jupyter Notebook App, a web-based interactive computing platform that allows editing and running notebook documents via a web browser.

---
### Objectives

- Load the spinal patient dataset
- Explore the data structure
-	Prepare data for machine learning
-	Split data into training, validation, and test sets
-	Upload data to S3 cloud storage
-	Configure and train an XGBoost model
- Save the trained model
---
### Task 1: Accessing a notebook instance in Amazon SageMaker

- On my AWS console I searched for SageMaker AI and clicked on it
- On the left menu I expanded Applications and IDEs and chose Notebooks

<img width="1366" height="563" alt="Screenshot (347)" src="https://github.com/user-attachments/assets/46da5054-f5e2-4cd2-8e92-8177164f15d8" />

:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

I clicked the Notebook instances tab
I found MyNotebook and clicked Open JupyterLab

<img width="1093" height="240" alt="Screenshot (348)" src="https://github.com/user-attachments/assets/08d3fe49-a7f0-46e9-a29a-eaf3e4c0b641" />

---

### Task 2: Opening a notebook in your notebook instance

-- In JupyterLab I opened the _en_us_ folder
-- I clicked on _3_4-machinelearning.ipynb_

---

### Task 3: Running the Code Cells

#### Step 1 Importing the data

<img width="738" height="118" alt="Screenshot (351)(1)" src="https://github.com/user-attachments/assets/79696540-6c41-491f-8cf1-1277fb45c182" />
This code imports all the tools needed to download the dataset, extract the files, create a data table, read the dataset format, and connect to AWS cloud services. It also hides warning messages to keep the output clean.

:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

![Screenshot (351)~2](https://github.com/user-attachments/assets/64179f3a-df79-42a9-a299-ddecdb0492dd)

This code downloads the spinal patient dataset from the UCI website and extracts the zip file so the data files are ready to use.

:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

![Screenshot (351)~3](https://github.com/user-attachments/assets/b1c19066-1b74-4041-9497-5ee8f393260f)

This code reads the extracted dataset file and converts it into a table with 310 rows (patients) and 7 columns (6 measurements and 1 diagnosis).

:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

![Screenshot (351)~4](https://github.com/user-attachments/assets/78d0ff21-3c1e-4516-a99a-758109961ec5)

This code changes the diagnosis column from words to numbers, converting "Abnormal" to 1 and "Normal" to 0 so the machine learning model can process them.

:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

---

### Step 2: Exploring the data

![Screenshot (353)~2](https://github.com/user-attachments/assets/64336ff5-e6a9-432a-b89f-f31f9852f478)

Shows the size of the dataset, displaying (310, 7) which means 310 patients and 7 columns.

:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

![Screenshot (353)~3](https://github.com/user-attachments/assets/ca6acef5-1370-4348-b9bd-98a8ae7515fa)

This code lists all the column names, showing the six spine measurements and the "class" column containing the diagnosis.

:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

### Step 3: Preparing the data

![Screenshot (354)~2](https://github.com/user-attachments/assets/3024d311-5eff-4310-9bb9-3ae6604b70dd)

This code moves the "class" column to the first position

:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

![Screenshot (354)~3](https://github.com/user-attachments/assets/f6a9e41a-e512-425f-a3e6-1167b8410651)

This code displays the column names after the rearrangement to confirm that "class" is now the first column.

:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

#### Splitting the data

![Screenshot (355)~2](https://github.com/user-attachments/assets/59e84409-b286-413a-be6d-adc9284a9345)

This code splits the dataset into two groups. 80% of patients go to the training set and 20% go to a temporary set for testing and validation. The stratify parameter ensures both groups have the same proportion of normal and abnormal patients.

:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

![Screenshot (355)~3](https://github.com/user-attachments/assets/e76f5949-5fdc-4cab-a525-24a5f779bde1)

This code takes the temporary set (which contains 20% of the original patients, about 62 patients) and splits it into two equal groups. Half become the test set (about 31 patients) and half become the validation set (about 31 patients).

The test_size=0.5 means split the data in half. The random_state=42 ensures the split is the same every time I run the code. The stratify=test_and_validate['class'] makes sure both the test and validation groups have the same percentage of normal and abnormal patients as the original dataset.

:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

![Screenshot (355)~4](https://github.com/user-attachments/assets/5a4e8be6-06aa-49af-ac95-6d431e7a3690)

This code displays the number of patients in each group.

:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

![Screenshot (355)~5](https://github.com/user-attachments/assets/4fbc9bda-3d4e-4fc0-aa08-f4c0e32c2d82)

This code counts how many normal patients (0) and abnormal patients (1) are in each group. This confirms that all three groups have roughly the same proportion of normal and abnormal patients as the original dataset, which had 100 normal and 210 abnormal patients.

:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

#### Uploading the data to Amazon S3

![Screenshot (357)~3](https://github.com/user-attachments/assets/f8c67a6f-f92b-4fe1-bde7-3bfe8bdda2b8)

This code sets up the cloud storage connection. It defines the S3 bucket name, folder name, and file names where the datasets will be saved. Then it creates a function called upload_s3_csv that converts a data table to CSV format and uploads it to the specified location in S3 cloud storage.

:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

![Screenshot (358)~2](https://github.com/user-attachments/assets/f5d76995-8531-4c8d-8404-04ba8b5f9b5b)

This code uploads the training, test, and validation datasets to the S3 cloud storage using the function created earlier. Each dataset is converted to CSV format and saved in its respective folder (train, test, validate) in the S3 bucket. 

:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

### Step 3: Training the model

![Screenshot (358)~3](https://github.com/user-attachments/assets/a5353ec4-1b7f-48cb-9127-8add12eab611)

This code retrieves the pre-built XGBoost software container from Amazon SageMaker. The container contains everything needed to train the model, and the output shows the container's location in AWS.

:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

![Screenshot (358)~4](https://github.com/user-attachments/assets/d425208e-9918-4fb7-b14a-d66abe833410)

This code sets the hyperparameters that control how the XGBoost algorithm learns from the data:
- "num_round":"42" - XGBoost will build 42 decision trees. Each tree learns from the mistakes of the previous tree, and 42 trees provide enough complexity to learn patterns without overfitting.
- "eval_metric": "auc" - The model's performance will be measured using AUC (Area Under the Curve). AUC tells how well the model distinguishes between normal and abnormal patients. A score of 0.5 means random guessing, while 1.0 means perfect predictions.
- "objective": "binary:logistic" - This tells XGBoost this is a binary classification problem with two possible outcomes: normal (0) or abnormal (1).

:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

![Screenshot (360)~2](https://github.com/user-attachments/assets/91438138-4963-43d3-b116-532d5fb0b8a9)

This code configures the training job. It specifies:
- container - Which XGBoost software to use
- instance_count=1 - Use one computer for training
- instance_type='ml.m4.xlarge' - The computer has 4 virtual CPUs and 16GB of memory
- output_path - Where to save the trained model in S3
- hyperparameters - The settings defined earlier (42 trees, AUC evaluation, binary classification)
This sets everything up but does not start training yet.

:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

![Screenshot (364)~2](https://github.com/user-attachments/assets/4d632654-c21a-4b53-94de-30fe26a1dd9e)

This code tells the training job where to find the data in S3. It creates two channels:
- train_channel - Points to the training data location
- validate_channel - Points to the validation data location
Both channels specify the data is in CSV format. These channels are then combined into a dictionary called data_channels that will be passed to the training job.

:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

![Screenshot (364)~3](https://github.com/user-attachments/assets/0c21c17d-52d6-47a2-a352-5a9f037f063d)

This code starts the actual training process. The model learns patterns from the 248 training patients while checking its progress against the 31 validation patients. Training takes 3-5 minutes to complete. Once finished, the trained model is automatically saved to the S3 output location.

:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:
---

### Conclusion

In this project, I successfully built a machine learning model that predicts whether a patient has a spinal abnormality based on six biomechanical measurements. I trained an XGBoost model using Amazon SageMaker with 310 patient records. The model learned patterns from the training data and was saved to S3 for future use. This model can now be used to help doctors identify patients who may need medical attention for spinal conditions.

---

### What I Learned
#### Machine Learning Concepts

- _Data Splitting_ I learned why it is important to split data into training, validation, and test sets. The training set teaches the model,
validation set checks progress during training, and test set provides final evaluation on unseen data.
- _Stratified Splitting_ I learned to use stratify to ensure each group maintains the same proportion of normal and abnormal patients as the original dataset, which prevents biased learning.
-  _XGBoost Algorithm_  I learned how XGBoost builds multiple decision trees that work together to make predictions, and how hyperparameters like num_round and eval_metric control the learning process.
-  _Binary Classification_ I learned to set up a model for binary classification where the outcome is one of two options (normal or abnormal).
