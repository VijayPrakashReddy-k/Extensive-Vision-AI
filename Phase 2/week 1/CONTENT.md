<section id="serverless-computing">
<h2>Serverless Computing</h2>
</section>

*`Serverless computing is a cloud computing execution model in which the cloud provider runs the server, and dynamically manages the allocation of machine resources. Pricing is based on the actual amount of resources consumed by an application, rather than on pre-purchased units of capacity.`*

- *`Serverless allows you to build and run applications and services without thinking about servers.`* 
- *`Cloud-based computing model.`*
- *`It eliminates (hides) infrastructure management tasks such as:`*

      server or cluster provisioning,
      
      operating system maintenance,
      
      capacity provisioning,
      
      downtime 
          
- *The unit of execution is often a function:* **FaaS - Function as a Service**
- *Pricing is based on the actual amount of resources consumed* <br>

`You can build them for nearly any type of application or backend service, and everything required to run and scale your application with high availability is handled for you!`

<section id="serverless-framework">
<h2>Serverless Framework</h2>
</section>

*`The Serverless Framework is a free and open-source web framework written using`* **Node.js**. *`Serverless is the first framework developed for building applications on AWS Lambda, a serverless computing platform provided by Amazon as a part of Amazon Web Services but now can work with others as well.`*

- A Serverless app can simply be a couple of lambda functions to accomplish some tasks or an entire back-end composed of hundreds of lambda functions. 
- It is used for building serverless applications via command line and config files
- It uses Amazon CloudFormation under the hood, which allows you to describe and provision all the infrastructural resources you need using a single JSON file. Once we define this file, all resources will be created in the cloud for us. 

![serverless-steps](https://user-images.githubusercontent.com/42317258/87466908-b7a71180-c634-11ea-9a63-bc07b7581efc.png)

<section id="aws-lambda">
<h2>AWS Lambda</h2>
</section>

- `AWS Lambda lets you run code without provisioning or managing servers.` <br>
- `You pay only for the compute time you consume - there is no charge when your code is not running` <br>
- `It automatically scales your application by running code in response to each trigger. Your code runs in parallel and process each trigger individually, scaling precisely with the size of the workload` <br>
- `You are charged for every 100ms your code executes and Can be triggered by different events (e.g. HTTP request)`

- ***`Your function code and it's dependencies shouldn't be greater than 250MB (deployment package .zip file)`***

![Lambda_usecases](https://user-images.githubusercontent.com/42317258/87825851-7fead480-c895-11ea-9fed-1ab8ef0a35e3.png)

**Features :**
            
            Runs on Amazon Linux OS, inside a runtime container
            The more RAM memory you allocate, the faster CPU you get:
            from 128MB to 3008 MB, in 64 increments
            Max. 500MB of storage inside /tmp directory (where your code/files can expand)
            
 *Free Tier:*
            
            1 million requests per month ($0.0000002 per requests thereafter)
            400,000 GB-seconds of compute time per month ($0.000000208 for every 100ms used thereafter, 128 MB of RAM)

<section id="dnn-model-deploy">
<h2>Deploying a DNN model</h2>
</section>

**Steps :**
<ol>
<li> Download a pre-trained model (downloading mobilenet v2 as assignment)
<li> create a Python Lambda function (AWS - python3)
<li> Python requirements plugin (for bundling all the libraries required)
<li> Adding requirements (adding pyhton library wheel links for size < 250 MB)
<li> handler.py (2 files will get created once completing the creation of service {lambda function})
<li> create an S3 bucket and move your model into the bucket
<li> configuring the serverless.yml
<li> deploying
      
            serverless deploy
            
<li> multipart/form-data (we are sending image interms of bytes, so make changes in AWS cloudwatch settings)
<li> testing our deployment (with help of INSOMNIA by passing image as input)

![Deploy DNN model](https://user-images.githubusercontent.com/42317258/87827211-0bfdfb80-c898-11ea-8002-3a43a2d5e9da.png)

<section id="assignment">
<h2>Assignment</h2>
</section>

`The result from the Mobilenet V2 model can be shown in the below INSOMNIA screen shot :`

![Model-prediction](./Images/Yellow-Labrador-Retriever.jpg)

