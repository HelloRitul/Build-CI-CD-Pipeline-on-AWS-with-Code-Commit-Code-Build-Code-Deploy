# Implementing CI/CD Pipeline in AWS
# Overview
In this article, we will learn about how to create a CI/CD Pipeline using AWS Services: AWS CodeCommit, AWS CodeBuild, AWS CodeDeploy, AWS Pipeline.
# Introduction
Once we have developed and deployed the application/product, It needs to be continuously updated based on user feedback or the addition of new features. This process should be automated, as without automation we have to run the same development and deployment steps/commands again and again for every change to the application.

With Continuous Integration and Continuous Delivery Pipeline, we can automate the complete workflow from building, testing, packaging, and deploying, which will be triggered when there are any changes to an existing application or we can say if there is any new commit to an existing code repository.

![Screenshot (57)](https://user-images.githubusercontent.com/69754757/225552491-bf553cdf-d753-4ddf-81b7-b24606bcd674.png)

# Advantages of a CI/CD Pipeline
1. Frequent releases: With CI/CD we can release the changes based on customer feedback or monitoring input

2. Low risk: As the process will be automated, there won’t be any manual intervention and configuration setup

3. Increased Productivity: With a structured process, a product will be released independently of other components, as in the case of multiple microservices we can release changes independently thus increasing developer productivity

Now, let’s start building the pipeline.

# AWS CodeCommit
It is a version control service similar to Github, hosted by AWS. For Demo, we will use a CodeCommit repository and push our application code to it (If you want you can use Github also).
1. In AWS console search CodeCommit, create a repository, and give a name to it.


![codecommit1](https://user-images.githubusercontent.com/69754757/225554238-3a9e3085-9d04-4568-949d-5e187bbbc93f.png)
2. Once the repository is created we need to add specific permission and create Git credentials to access the CodeCommit repository.

3. Go to the IAM console, choose Users and select which User you want to configure for CodeCommit, and attach AWSCodeCommitPowerUser policy from the policies list and Review and then click Add Permission.



![Screenshot (58)](https://user-images.githubusercontent.com/69754757/225555738-df89a179-f954-4270-bc51-a8ade7f8fd82.png)

4. Now, to generate Git credentials select the User for which you have added CodeCommit Permission and search for HTTPS Git credentials for AWS CodeCommit section and then click Generate credentials and download it.


![Screenshot (59)](https://user-images.githubusercontent.com/69754757/225556368-d1863c84-4349-4519-b9fa-896270f295cb.png)

5. Now copy the repository URL and clone it on the local system using git clone




![coderepo](https://user-images.githubusercontent.com/69754757/225558080-82d0456e-e718-4bb5-b189-19dca4836412.png)

git clone URL

a. For username and password, use from credentials file downloaded earlier.

b. Now we can push our application to this repository, I am using Visual Studio Code to write the source code, you can download source code from my Github or use your own application.

![visualstudiocode ](https://user-images.githubusercontent.com/69754757/225558708-ea1a7948-7058-4185-9bdb-74f0b423c611.png)

git add .

git commit -m 'app:v1.0'

git push

Once you have pushed the code, your CodeCommit repository will look as follows


![codecommit4](https://user-images.githubusercontent.com/69754757/225559196-c8fda407-afe9-4417-a096-c051a2f6bfb4.png)


# Create a CodeBuild Project
The next step is to set up Continuous Integration functionality on the CodeCommit repository.


AWS CodeBuild is managed CI Service which compiles source code, runs tests, and packages the source code which can be used for deployment.

Project Configuration:- 
 Write Project Name

Source:-
 Choose a Source AWSCodeCommit

Environment:- 
 Choose a managed environment and Amazon Linux OS. Create a new service role, and name it something like {{ProjectName}}-ServiceRole. In keeping with our theme, make sure you record it!

Artifact:- 
 Under type, choose S3 and put in your bucket name, and create a build artifact name. 
Once you have that ready to go, click the orange “Create Build Project.”

To use CodeBuild, we need a buildspec.yml file that contains commands used to compile, test, and package our code.


![Screenshot (60)](https://user-images.githubusercontent.com/69754757/225561100-76d1b055-169e-43d8-bf29-3c44342f79ef.png)

# Create a CodeDeploy Configuration
This one is easier! Under “Deploy” -> “Create Application” and choose EC2 as your “Compute Platform.”


Once you Create Application will look as follows

![application](https://user-images.githubusercontent.com/69754757/225561513-fbe34315-1e97-4429-b85c-586d848100b8.png)

Inside Applications Create Deployment Group


![depl1](https://user-images.githubusercontent.com/69754757/225561889-790e6cc8-ae3f-4581-80a9-2b3726dc7e89.png)


![depl2](https://user-images.githubusercontent.com/69754757/225561988-be35fc35-9ab4-44b3-b912-6e726cca0e88.png)

![depl3](https://user-images.githubusercontent.com/69754757/225562061-349d4142-b5f2-4e35-a39e-94f8a88c2bd6.png)

![depl4](https://user-images.githubusercontent.com/69754757/225562119-fec4428f-0141-4910-9741-c573216dfbfd.png)

After Creating Deployment Group ,Let’s we have to create Deployment

![depl5](https://user-images.githubusercontent.com/69754757/225562277-47f2f470-c00b-4dad-a119-1bc350f6408b.png)

![depl8](https://user-images.githubusercontent.com/69754757/225564740-a75b46b2-0ce7-4bed-80f6-4255a65a85bd.png)

# AWS CodePipeline

CodePipeline will automatically build and deploy our application when there are any changes in the code repository.

1. Go to CodePipeline console, click Get started and configure the pipeline

2. Next, select CodeCommit for source provider (or Github if you are using it, for this, you have to log in to Github) and select the repository and branch to configure for CI/CD

![pipe1](https://user-images.githubusercontent.com/69754757/225565264-4824ed54-ef2f-4d76-b250-ac35fab48d4a.png)

![pipe2](https://user-images.githubusercontent.com/69754757/225565412-5aa01d5a-61b9-4f7a-8ec6-c3b67134a7a1.png)

3. Next, for the build provider select CodeBuild and create a new build project, give it a name and configure it as follows

![pipebuild](https://user-images.githubusercontent.com/69754757/225565601-9fd7568d-ca76-4cc8-835a-0a6bde79e6a9.png)

4. For Deploy provider, select CodeDeploy and create a new deploy stage, give it a name and configure it as follows

![pipedeploy](https://user-images.githubusercontent.com/69754757/225565830-9be7c181-9431-4a06-8825-d0d14a482c30.png)

Click Next, Review it and click Create pipeline

5. Once Pipeline is created successfully.

6. Now, let’s test the complete Pipeline by changing the source code and pushing the changes to the Code commit repository.

Make some changes(highlighted text in below image) in the ‘index.html’ file in the templates folder


![vs1](https://user-images.githubusercontent.com/69754757/225566542-4f756816-f7cc-4332-ac9e-e9de1084a0c0.png)

Now push the changes to the repository

![vs2](https://user-images.githubusercontent.com/69754757/225566691-5a39f44d-ff88-49fb-82ef-7effcdb8289b.png)

![vs3](https://user-images.githubusercontent.com/69754757/225566755-992f7dad-3421-4ce2-a22f-7f7f8f52625f.png)

Once the changes are pushed, CodePipeline will trigger the CI/CD process and release change.

![rel1](https://user-images.githubusercontent.com/69754757/225566926-b034d671-4f06-4519-9e3a-306c3c1d6b2d.png)

![rel2](https://user-images.githubusercontent.com/69754757/225566992-cbacc9ed-78cf-455d-9e3b-5c909ddbb0ea.png)

Now, to verify our changes are made and deployed successfully, visit the EC2  and Copy the Public-Ip and Paste in the browser 

![Screenshot (55)](https://user-images.githubusercontent.com/69754757/225567172-2468fa59-a05a-4622-94a4-3cea6c180650.png)

![output1](https://user-images.githubusercontent.com/69754757/225567298-b8f5f663-86a6-468d-bbb1-f72cd85aa31d.png)

# Hooray! We have successfully created a CI/CD Pipeline in AWS services.
