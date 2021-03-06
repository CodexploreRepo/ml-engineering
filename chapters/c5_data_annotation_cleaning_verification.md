# Chapter 5: Data Annotation, Cleaning and Verification
- Least Enjoyable Part of Data Science is: Cleaning & Organizing Data

# Table of contents
- [Table of contents](#table-of-contents)
- [1. Data Annotation](#1-data-annotation)
  - [1.1. Examples of Label Design](#11-examples-of-label-design) 
  - [1.2. General principles of label design](#12-general-principles-of-label-design)  
  - [1.3. Data Annotation Tool](#13-data-annotation-tool)
  - [1.4. Data Annotation Evaluation](#14-data-annotation-evaluation)
  - [1.5. Quality control over the annotations](#15-quality-control-over-the-annotations)
- [2. Data Cleaning](#2-data-cleaning)
  - [2.1. Missing Values](#21-missing-values) 
  - [2.2. Data Validity vs Data Accuracy](#22-data-validity-vs-data-dccuracy)
  - [2.3. Data Privacy](#23-data-privacy)
- [3. Data Verification](#3-data-verification)

# 1. Data Annotation
## 1.1. Examples of Label Design
- Example 1: if we check images of *chairs* in ImageNet dataset, you may find chair images like these
  - Solution: manually design some sub-classes by asking annotation team, instead of the original "chair" labels. 
    - This helps the machine learning models work better.
<p align="center">
  <img src="https://user-images.githubusercontent.com/64508435/165287611-2b27b5fe-5d4a-4c41-b223-3554b9cfc5b6.png" width="600" />
</p>

- Example 2: Warehouse Fire Detection 
  - Fire in the warehouse is a very rare event & we’d like to design a CV algorithm for fire detection.
<p align="center">
  <img src="https://user-images.githubusercontent.com/64508435/165288394-8351c291-7dd7-4820-9981-7a904d646af8.png" width="600" />
</p>

- Example 3: Text annotation for speech synthesis
  - Without *emotion labels*, the synthesis algorithm may inject emphasis wrongly into the speech synthesis.
  - Solution:
    - Collect more data and let the model learns itself. 
    - Ask annotation team to mark if audio is strongly emotional or not.
## 1.2. General principles of label design
- General principles of label design/review
  - The sample with the **identical** labels are similar to each
  - The **semantic meaning** of the label is easy to understand 
  - The **number of samples for each label** is sufficiently large
    - If there’s a label with very few samples: Give it up!
- The process of label design:
  - Design the label structure
  - Annotate by yourself
  - Review and revise the label structure
  - Pass the instructions to annotation teams to start the real work of annotation on training and test sets.

### 1.2.1. Example of Label Design
- Context: Scooter parking audit
- The task is to recognize if the scooter is parking appropriately
- The business value
  - Educate riders on good parking
  - Reduce operational cost
- Initial version with three labels: 
  - Good parking
  - Bad parking
  - Toppled: if the scooter is toppled, the team will send the operation team to remove that. 
<p align="center">
  <img src="https://user-images.githubusercontent.com/64508435/165290438-2f8cd1c9-d562-4278-b726-33ea9fd5d8e7.png" width="600" />
</p>

- After labelling 500 images, I came up with the second version
  - Invalid photo
  - Good parking
  - Bad parking
  - ~~Toppled~~
- Re-labelling 500 images, we had the third version 
  - Invalid photo
  - Good parking
  - Against the wall
  - Blocking access

## 1.3. Data Annotation Tool
- **Data sets**: objects for data annotation
- **Label sets**: labels/dictionary for annotation
- **Instructions**: connection between dataset and label sets examples on how to do the annotation
<p align="center">
<img width="600" alt="Screenshot 2022-04-26 at 19 44 58" src="https://user-images.githubusercontent.com/64508435/165292909-e88bac03-69ff-4d21-bf6e-2ba3ab00d487.png"></p>

- Step 1: Create a data set
  - Dump the objects for annotation into a bucket
  - Build a CSV file (resp. json file) containing links to the objects on Google Cloud (resp. AWS)
<p align="center">
<img width="300" alt="Screenshot 2022-04-26 at 19 44 58" src="https://user-images.githubusercontent.com/64508435/165293087-d880a2db-aecf-4701-82ab-d3b5173917f2.png"></p>
                                                                                                                               
- Step 2: Config the data set: image, audio
- Step 3: Create a labelling task
- Step 4: Manage the team 
  - Inivte annotator into the team   
  - Annotation team management is a big challenge 
    - `Quality`: The accuracy of the labels decide the accuracy of the model
    - `Efficiency`: The annotation speed decides how much training is available after a period of time                                                                                                            
 ## 1.4. Data Annotation Evaluation
- **Consistency Rate**: Percentage of identical labels from at least two annotators
  - Consistency rate drops when the same annotators run on the same job for a few weeks
- For training data, we will use the data that being labeled and agreed by at least 2 annotators.
<p align="center">
<img width="800" alt="Screenshot 2022-04-26 at 19 44 58" src="https://user-images.githubusercontent.com/64508435/165294384-49fa995a-c364-4aee-93a3-bcb496f35fc6.png"></p>

- The problem of **concept understanding drift**
  - New annotators are not familiar with the rules
  - After a weekend, annotators forget the rules
  - The distribution of the data affects the priori (prior knowledge) of the annotators.
    - For example: the training samples come from batches everyday, and there will be a different between the weekday, weekend and public holidays.
 
## 1.5. Quality control over the annotations
- Write your instructions in a better way
  - Clear descriptions and samples over all possible cases
  - You need to go through them by yourself
  - Don’t expect your annotators help you find the corner/boundary cases
- Methods for **daily quality control**
  - Sample and check the labels every day by yourself (**Consistency Rate**)
  - Run an exam for your annotators every day before they start their daily work

# 2. Data Cleaning
- When do we need data cleaning?
  - Multi-dimensional data is more error-prone
- There are always errors in the data
  - Source problem: data crawler may miss some fields
  - ETL problem: there are bugs in processing some special cases

## 2.1. Missing Values
- Method 1: Remove the rows with missing values
- Method 2: Fill in the value
  - Mean value strategy
    - Pro: simple yet effective in most cases
    - Con: slightly affect the ML performance
  - NULL value strategy
    - Pro: NULL contains additional information in some cases
    - Con: your model is expected to handle NULL value
  - Other strategy based on domain knowledge: A prediction model could be used
    - Pro: If the knowledge/model is correct, it’s highly effective 
    - Con: How to verify the knowledge/model?

## 2.2. Data Validity vs Data Accuracy
<p align="center">
<img width="400" alt="Screenshot 2022-04-26 at 19 44 58" src="https://user-images.githubusercontent.com/64508435/165298323-6ebd849c-261d-4344-93cc-cfdaa5171901.png"></p>

### 2.2.1. Data Validity
- **Data type** constraints 
  - For example:  Age column contains integer only
  - Method: Type checking, Regular expression 
- **Range type** constraints
  - Age column contains numbers no larger than 150
  - Temperate is usually no larger than 50 degree Celsius
  - The speed of a bus is no larger than 300 km/h
- **Unique type** constraints
  - For example: Passport Number, Image ID, Name of a person
- **Foreign key** constraints: If the field refers to another table, make sure the keys are valid
<p align="center">
<img width="600" alt="Screenshot 2022-04-26 at 20 23 22" src="https://user-images.githubusercontent.com/64508435/165299076-c438508d-a768-44a8-8880-de68b0f70f4b.png"></p>

- **Cross-field** validation: Build a formula across fields to validation
  - BMI = Weight / square of Height in meter

## 2.3. Data Privacy
- Find and remove personal identity information (PII)
- Does **General Data Protection Regulation** `GDPR` ban Machine Learning?
  - The short answer is “no”, But you need to prepare a lot of paperwork with the lawyers
<p align="center">
<img width="600" alt="Screenshot 2022-04-26 at 20 23 22" src="https://user-images.githubusercontent.com/64508435/165299524-318274ca-391a-4d17-b4a5-92e0e245627f.png"></p>

# 3. Data Verification
- Why do we need data verification ?
  - The **distribution of the real workload** might be **different** from your training data set
  - When changes happen, need to alert the algorithm team.
- Where does the change come from? 
  - Change of user behavior
  - Change of data collection method
  - Change of the environment or external factors
## 3.1. Consequence of data distribution change
- **Macro-level consequence**
  - Let’s say a model achieves "good parking detection" with 95% recall and 92%
  precision. Assume 20% is good parking
  - The # of complaints from riders per 1,000 trips is 10
    - When the good parking rate grows to 50%
  - The # of complaints from riders per 1,000 trip will be 25
<p align="center">
<img width="600" alt="Screenshot 2022-04-26 at 20 23 22" src="https://user-images.githubusercontent.com/64508435/165303080-ca46a250-d3c3-4eb7-9b34-90a740cb54c2.png"></p>

- Original Boundary: Red Line
- Data change to upper right (green points) &#8594;  put the green points into the training data as well.

## 3.2. Find the distribution change
- `Categorical data`: Keep track of the distribution over the values
<p align="center">
<img width="500" alt="Screenshot 2022-04-26 at 20 50 47" src="https://user-images.githubusercontent.com/64508435/165303698-dd2570c3-1a66-4019-82c2-24d7a8bf288f.png"></p>

- `Numerical values`:
  - Keep track of the mean and variance over the columns
  - Plot Histogram
  - Scatter Plot (to see the joint-distribution in 2 different dimension, which is unable to do in Histogram)
    - On the right scatter plot: negatively correlated to each other
<p align="center">
<img width="500" alt="Screenshot 2022-04-26 at 20 50 47" src="https://user-images.githubusercontent.com/64508435/165303901-8c532a6a-600a-4d7f-866f-e95cd398c693.png"></p>

## 3.3. Data Validation Pipeline
- Enable automatic model update based on data validation
<p align="center">
<img width="536" alt="Screenshot 2022-04-26 at 20 56 16" src="https://user-images.githubusercontent.com/64508435/165304733-d4c9513d-5b19-41f1-b7a7-e5aa28451155.png"></p>


[(Back to top)](#table-of-contents)
