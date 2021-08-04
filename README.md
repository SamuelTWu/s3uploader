# s3uploader
Welcome to the s3uploader! I hope you're ready for some fun with buckets, functions and gateways! If not, too bad! 

The upload pipeline is made of 4 distinct parts, namely the s3 Bucket, Lambda Function, API Gateway, and Coginto.

S3 Bucket: This is the database that stores our files. Not everyone can upload to this bucket, however. Instead, you must have a specific url in order to upload files.

Lambda Function: Lambda functions are little scripts that run whenever a specific event occurs. In this case, whenever someone successfully accesses our API Gateway, the lambda function will generate and return a specific url that allows users to upload files to the bucket. 

API Gateway: The gateway is a management tool that sits between a client and a collection of backend services. In this case, the gateway autheticates users, and acts as a sort of 'button' that activates our lambda function. Only users that have the correct id_token can 'pass' through this gateway, sort of like the gates in Lord of the Rings or something IDK i don't remember those books.

Cognito: This contais a list of users that have created an account with us, and gives users id tokens to access the API Gateway. 


Steps to Create s3Uploader w/Folders
1) Create *lambda test function*, *s3 bucket*, and *temp-gateway*
        1) Follow github instructions at the [S3 presigned URLs with SAM Github](https://github.com/aws-samples/amazon-s3-presigned-urls-aws-sam), auto-create *s3 bucket*, *lambda function*, and *temp_gateway*  
        2) Copy lambda code from my very own [S3Uploader Github](https://github.com/SamuelTWu/s3uploader). In depth analysis of code is at bottom of tutorial  
        3) Keep note of the *lambda test function*, yours will be named differently, for the purpose of this tutorial we will refer to it as *lambda test function*  
        4) *temp_gateway* will be replaced with a *Rest_API* later, hence “temp”  
2) Create *Cognito*
        1) Create a cognito user pool, following this [cognito-upload integration demo](https://www.youtube.com/watch?v=o7OHogUcRmI)
        2) For callback url, we will be replacing with *temp_url* later
3) Create *temp_url*
        a) Copy index.html from [S3Uploader Github](https://github.com/SamuelTWu/s3uploader)
        b) Host on temp url using [Github pages](https://www.youtube.com/watch?v=8hrJ4oN1u_8)
4) Create *Rest_API*
        a) Go to API Gateway service
        b) Click ‘Create API’, then choose ‘Build’ under Rest API
        c) Name Rest API, other options can be ‘default’
        d) Under ‘Actions’ choose ‘create resource’, name resource
        e) Under ‘Actions’, choose ‘create method’, choose ‘GET’
        f) You will be prompted with ‘Integration Type’ select Lambda Function
        g) Underneath you will see ‘Use Lambda Proxy integration’, select checkbox
        h) Under lambda function, begin to type ‘lambda test function’ and you will see it pop up
5) Link *Cognito* to *Rest API*
          a) his loosely follows [this video](https://www.youtube.com/watch?v=oFSU6rhFETk)
          b) Under GET select ‘method request’
          c) Under authorization select ‘Cognito’
          d) You will need to allow CORS access. To do so, select ‘Actions’ and choose ‘Enable CORS’. Click ‘Enable CORS and replace existing CORS headers’
          Extra note) Because we are using lambda proxy integration, we must also send the ‘Access-Control-Allow-Origin’ header in the lambda function. I have done this for you, you’re welcome.
6) Link *temp_url* to *Rest API*
        a) In the *index.html*, find the ‘URL_ENDPOINT’ variable
        b) In *Rest API*, select ‘stages’ and choose your stage. 
        c) The ‘URL_ENDPOINT’ is = to the ‘Invoke url’ followed by /’resource_name’
           Example: https://example.region-2.amazonaws.com/test/exampleresource


Commonly Asked Questions:
Bro what the lambda function do?
Why tf we using Lambda Proxy Integration?
How does the index.html work?

ill answer these later chill

