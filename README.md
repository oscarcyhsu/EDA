# EDA for insurance industry Part4

## Customer Use Cases

A. Calculate insurance quotes for health insurance


Both structured data and unstructured data are collected and stored in a S
bucket, then read into Amazon Redshift / DynamoDB in preparation phase of
EDA system to do parsing and cleaning and store back to S3. That is to say,
when the procedure of calculating insurance quotes are called, all data are
already available in S3.

Amazon Sagemaker then read the data from S3 and train machine learning
models / make prediction with machine learning models. The result of
estimated quotes will be stored back to database for future use. Amazon
Sagemaker also allows users to retrain the model easily without have to
implement the pipeline by ourselves. I configure a routine to retrain the model
every 7 days to keep the model up to date.

B. Insurance Coverage Analysis for Business Development

Insurance coverage dataset are stored in to Amazon Redshift and can be visualized using
build-in tool. This can be used by data analysts to determine the business strategies for each
city. Intuitively, we want to invest business effort in cities with a high average expense and
are expanding their medical facilities.

## EDA Design and End-to-End workflow-based applications

The following figure is the reference architecture that I used. As I mentioned in Part3, some
components are simplified in my implementation because AWS provide more high-level
services now. Also, streaming component are ignored.

For the end-to-end solution, an imaginary end user application (not implemented) will try to
retrieve the estimated quote from the database. If the entry is not there, Sagemaker will be
triggered to make prediction based on the data we collected for the user, and store the result
to database.

For database optimization, although in current implementation several datasets are used for
predictions, they are independent. Therefore, no redundancy in database is needed to allow
fast query. All we need is a foreign key to relate personal data to a person.



## Database Logical Design and Optimization

The relational database is in fifth normal form so no consistency check has to be done when
inserting, updating, deleting entries.


