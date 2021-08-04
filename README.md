# s3uploader
Welcome to the s3uploader! I hope you're ready for some fun with buckets, functions and gateways! If not, too bad! 

The upload pipeline is made of 4 distinct parts, namely the s3 Bucket, Lambda Function, API Gateway, and Coginto.

S3 Bucket: This is the database that stores our files. Not everyone can upload to this bucket, however. Instead, you must have a specific url in order to upload files.

Lambda Function: Lambda functions are little scripts that run whenever a specific event occurs. In this case, whenever someone successfully accesses our API Gateway, the lambda function will generate and return a specific url that allows users to upload files to the bucket. 

API Gateway: The gateway is a management tool that sits between a client and a collection of backend services. In this case, the gateway autheticates users, and acts as a sort of 'button' that activates our lambda function. Only users that have the correct id_token can 'pass' through this gateway, sort of like the gates in Lord of the Rings or something IDK i don't remember those books.

Cognito: This contais a list of users that have created an account with us, and gives users id tokens to access the API Gateway. 


[Upload Github](https://github.com/aws-samples/amazon-s3-presigned-urls-aws-sam)
