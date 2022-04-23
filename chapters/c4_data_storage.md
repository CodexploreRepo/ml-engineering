# Data Storage
- 90% of the time spends on Data. If the company spends 50% of the time on machine learning model, the company will fail.

# Table of contents
- [Table of contents](#table-of-contents)
- [1. Storage for Complex ML Data](#1-storage-for-complex-ml-data)
  - [1.1. Why Storage matters to ML](#11-why-storage-matters-to-ml)
- [2. Object Store: Amazon S3](#2-amazon-s3)
  - [2.1. Access S3 with Python](#21-access-s3-with-python) 
- [3. Document Store: Mongo DB](#3-mongodb)
  - [3.1. Access MongoDB with Python](#31-access-mongodb-with-python)
  - [3.2. Comparison between RDBMS vs MongoDB](#32-comparison-between-rdbms-vs-mongodb) 
  - [3.3. Complex Object Storage in MongoDB](#33-complex-object-storage-in-mongodb)
  - [3.4. Command Lines](#34-command-lines)
- [Resources](#resources)


# 1. Storage for Complex ML Data
## 1.1. Why Storage matters to ML
- *Data Type* complex and high diversified
  - Different data types (images, video, audio, text)
  - Label complexity: not only 1, 2, 3 but like bounding boxes
- *High Performance* requirement:
  - Need to pack data in a efficient way 
  - Select & de-select data, based on the training results
- *Different Nature of Data*: :rocket:
  - Semi-structured objects
  - Key-value objects (Redis)
  - Object store (Amazon S3). 
  - Document Store 
    - Mongo DB: Plain text, without fuzzy search
      - For ex: medical report
    - Elastic Search: Plain text, search index needed
      - For ex: text logs from the systems

# 2. Amazon S3 
- It’s originally proposed by AWS, but not almost every cloud provides a copycat
- Simple Idea: every **object** (binary string) is indexed with 2 strings
  - A bucket name
  - A key name 
<p align="center">
  <img src="https://user-images.githubusercontent.com/64508435/163996879-b3013dad-2833-411e-b7d0-6e794ce0c2a6.png" width="550" />
</p>

- This `.JPG` image is stored in S3.
  - Hireachy: Amazon S3 &#8594; Buckets &#8594; neuron-server (bucket_name)

## 2.1. Access S3 with Python
<p align="center">
  <img src="https://user-images.githubusercontent.com/64508435/163997320-1d40da2f-be81-48a4-822e-cbb64a43bc4b.png" width="550" />
</p>

- Access to S3 is very easy
  - `boto3`: is the python library for S3 access
  - `s3.object(bucket_name, object_name)`
- *Problem*: very hard to filter the object as the data is not organized. Only good for massive data storage
- *Solution*: MongDB - managing a collection of documents

# 3. MongoDB
- `JSON format`: to organize data in the plain text, so that any machine can understand the data format
- **MongoDB**: to manage the collection of these `json` documents and you can query the data. 
  - In practice: MongoDB is used as the data warehouse.   
  - **No Schema**: it can accept any json format, **need to be very careful**.
  - GUI: Robo3T
<p align="center">
<img width="500" alt="Screenshot 2022-04-19 at 19 54 32" src="https://user-images.githubusercontent.com/64508435/163997774-d13ca302-257e-46b9-b253-f2ca1f7926fd.png">
</p>

## 3.1. Access MongoDB with Python
<p align="center">
<img width="700" alt="Screenshot 2022-04-19 at 19 54 32" src="https://user-images.githubusercontent.com/64508435/164891126-ddf5b0d0-52a3-407b-a3de-4bfd662e9e81.png">
</p>

  - Query, Aggregrateion pipeline (similar to SQL - Group By), Sort 
<p align="center">
<img width="700" alt="Screenshot 2022-04-19 at 19 54 32" src="https://user-images.githubusercontent.com/64508435/164891197-5e515492-9507-450d-8be7-4f24b7a3aeba.png"><br>
<img width="700" alt="Screenshot 2022-04-19 at 19 54 32" src="https://user-images.githubusercontent.com/64508435/164891245-11850898-6d09-4fdb-ac77-5a962e3ac04f.png">
</p>

## 3.2. Comparison between RDBMS vs MongoDB
<p align="center">
<img width="600" alt="Screenshot 2022-04-19 at 19 54 32" src="https://user-images.githubusercontent.com/64508435/163998225-e37a6367-aad8-428b-8d4c-3a2978b23624.png">
</p>

## 3.3. Complex Object Storage in MongoDB

## 3.4. Command Lines:
- EmployeeDB: name of the database
- Employee: name of the colletion
- WriteResult: one document inserted in a collection
<p align="center">
<img width="474" alt="Screenshot 2022-04-19 at 19 58 59" src="https://user-images.githubusercontent.com/64508435/163998441-211f445c-0cfa-4436-a154-125141ce0045.png">
</p>
  
[(Back to top)](#table-of-contents)

### 2.3.1. Storing Complex Objects
- Convert binary file into a Base64 string
  - Split the binary string into a sequence of 8-bit number
  - Convert every 8-bit number to a character according to the Base64 Encoding Table
- Reverse conversion
  - Convert a character to 8 binary bits
  - Concatenate the bits into a long binary string


<img width="413" alt="Screenshot 2022-04-19 at 20 16 20" src="https://user-images.githubusercontent.com/64508435/164001482-5bac836f-9103-4626-9fca-8f95afc056c2.png">


<p align="center">
  <img src="https://user-images.githubusercontent.com/64508435/164001532-a25ac14b-d5f3-4a46-82d1-5b0b8a59495b.png" width="550" />
  <br>Base64 encoding in Python for storing an image in MongoDB
</p>

<p align="center">
  <img src="https://user-images.githubusercontent.com/64508435/164001761-c531c951-65b9-4f64-9e49-1a2b450604d9.png" width="550" />
  <br>Base64 decoding in Python 
</p>

## 2.4. ElasticSearch
- ElasticSearch behaves like a search engine
  - The adoption of RESTful interface
  - Its very unique score function over **text search queries**
  - Powerful query language over text data
  - Strong consistency guarantee
- The demand of text search is more complicated
<img width="1126" alt="Screenshot 2022-04-19 at 20 43 11" src="https://user-images.githubusercontent.com/64508435/164006572-c6ac4bfd-8c35-4dd9-9cc3-5fbe13fcc82c.png">

- ElasticSearch organizes documents in a **hierarchy** and provide search functions

<img width="618" alt="Screenshot 2022-04-19 at 20 43 49" src="https://user-images.githubusercontent.com/64508435/164006882-59da250c-fd2e-4ef9-8bfc-503a2cf2d486.png">

- No need the command-line, but via Browser, you can connect to ElasticSearch database
- For example: create `hardwarezone` database on ElasticSearch
  <img width="986" alt="Screenshot 2022-04-19 at 20 44 42" src="https://user-images.githubusercontent.com/64508435/164007027-77a70c7b-9e6b-4157-9645-be57b85aad5c.png">
  
- Use RESTFUL API to insert data into the database via POST method.
  - `201`: operation is successsfully applied. 
  - Insert a document without an ID 
<img width="1052" alt="Screenshot 2022-04-19 at 20 45 36" src="https://user-images.githubusercontent.com/64508435/164007166-4e681580-b860-49e6-912c-d1e7e0489bc0.png">

  - Insert a document with an ID
<img width="787" alt="Screenshot 2022-04-19 at 20 48 02" src="https://user-images.githubusercontent.com/64508435/164007533-2f332ad8-a0a8-4edb-9f5e-89dbd252f344.png">
  
  - Retrieve a document based on ID
<img width="787" alt="Screenshot 2022-04-19 at 20 51 29" src="https://user-images.githubusercontent.com/64508435/164008122-9b311e61-e45d-4be7-a544-39fbaf4eaff9.png">

- Simple search operations: Simple Lucene-style search
- <img width="679" alt="Screenshot 2022-04-19 at 20 52 35" src="https://user-images.githubusercontent.com/64508435/164008338-81a8550b-b0c7-4e92-99a2-22ad1f364844.png">
<img width="476" alt="Screenshot 2022-04-19 at 20 55 10" src="https://user-images.githubusercontent.com/64508435/164008775-95009fdd-79f7-4895-bdb8-58d6729f023b.png">
#### Domain-Specific Language (DSL)
-  Query in a tree structure
-  The first part query context is involved in the score function
- The second part filter context includes filtering conditions
- "must" condition: must have 
- "filter" condition: add some scores, if a good match, the score will be high.
- Boolean query combines 
  - Must query
  - Filter query
  - Should query
  - Must_not query

<img width="385" alt="Screenshot 2022-04-19 at 20 57 35" src="https://user-images.githubusercontent.com/64508435/164009180-26a5bf97-e383-4481-9491-7fa3ea8e63a1.png">

- Boosting query combines 
  - Positive query
  - Negative query
#### what makes ElasticSearch different

<img width="734" alt="Screenshot 2022-04-19 at 21 00 14" src="https://user-images.githubusercontent.com/64508435/164009708-a6f6ec9a-5b16-4b97-a5dd-0a8bb0c75744.png">
- Chracter Filter in Analyzer: Elastic Search can ignore the 

<img width="548" alt="Screenshot 2022-04-19 at 21 01 18" src="https://user-images.githubusercontent.com/64508435/164009906-aae86f34-701e-4808-bb43-ff4e7a705a86.png">

- Tokenizer in Analyzer
  - Break sentence into tokens
  - Every analyzer has exactly one tokenizer
  - Stem

  - Transformation over the tokens 
    - Convert to lower-case
    - Stemming
    - Synonyms

- html_strip: a character filter to remove any HTML character texts.
<img width="977" alt="Screenshot 2022-04-19 at 21 02 51" src="https://user-images.githubusercontent.com/64508435/164010157-99bfed91-d77b-4c41-aaf1-e5bded61ae90.png">


- When Elastic Search? And When MongoDB?
- Use Elastic Search: search over the documents, log analysis from IoT system.
  - An internal search engine over massive documents
  - Advanced text search involving complex text pre-processing
- Use MongoDB: dump all the data
  - A general-purpose database for all sorts of data
  - An engine with data retrieval based data id or batches 
  - **High performance** as *object* store in compare with Elastic Search. 

# Resources




[(Back to top)](#table-of-contents)