# Build CI/CD Pipeline on AWS with Code Commit | Code Build | Code Deploy 
This Article will demonstrate how to Create Git repository on AWS CodeCommit. Also , Compiles source code of repository with Success using CodeBuild.
# What is CodeCommit?
AWS CodeCommit is a version control service hosted by Amazon Web Services (AWS) that you can use to privately store and manage assets such as documents, source code, and binary files. It is an in-house repository or infrastructure that lets you host or hold repositories. AWS CodeCommit basically gives you an environment where you can actually go ahead commit your code, code push it, or pull it. CodeCommit can be found in your AWS management console under Developer Tools.
# What is CodeBuild ?
AWS CodeBuild is a fully managed build service in the cloud. CodeBuild compiles your source code, runs unit tests, and produces artifacts that are ready to deploy. CodeBuild eliminates the need to provision, manage, and scale your own build servers.
# Flow of Execution
-> Process For Code Commit, we will:

Create Repository

Create Crendentials

IAM Attach policy

Add index.html file in repository

-> Process For Code build, we will:

Create a Code Build Poject

Create buidspec.yml File

Create S3 bucket

Add Artifact

# →Let’s Create a CodeCommit:
Step by Step implementation:

1.Go to AWS console home and search a service “Code Commit” . Click on “Create repository”.



![p1](https://user-images.githubusercontent.com/69754757/225605056-cc39d2fc-9bfd-4cfa-9ca4-6dcb39bab95a.png)

2. Enter a Repository name and optionally description, “Click on Create”.

![p2](https://user-images.githubusercontent.com/69754757/225605170-72b64d22-ed22-4fdc-8c2a-883c354a37ea.png)

3. After created your repository, You need a GitCredentials for your AWS IAM User, Create IAM User navigate to “Security Crendentials” , Select for “HTTPS GIT crendentials for AWS code commit”

![p3](https://user-images.githubusercontent.com/69754757/225605546-7bc1c289-a9a1-45f9-8b58-d3145724177e.png)

3. Click on Generate Crendentials and download it.

![p4](https://user-images.githubusercontent.com/69754757/225605816-05b88f7b-4ad8-4505-a233-d7fa8547f492.png)


4. Go to your VS Code. Make a folder ,open terminal and Clone your repository from CodeCommit using command “git clone <repository_url>”.

![p5](https://user-images.githubusercontent.com/69754757/225606172-c3f40637-96f0-48d8-bf1b-3846c3e45f6c.png)


# Enter your credentials: 
Username and password in given prompt which you generated and downloaded.

![p6](https://user-images.githubusercontent.com/69754757/225606572-f0fcad09-d240-409e-ae36-7c8606e0b4a0.png)


5. you will get an error , for this error , you have to give permission to IAM User for code commit, Back to IAM dashboard ,Click on “Add permissions” dropdown and click on “Add permissions”.


![p7](https://user-images.githubusercontent.com/69754757/225607005-722f0410-8106-4815-b720-0ff1cac2c3fd.png)
Pick “AWSCodePowerUser” from given options.

![p8](https://user-images.githubusercontent.com/69754757/225607194-42526200-1678-4fb4-af3a-459d762ac5e6.png)

Here you will get access of code commit.

![p9](https://user-images.githubusercontent.com/69754757/225607458-fe9bacdc-8bbd-497a-873b-64e4ca47b27c.png)


6. Come back to visual studio ,After that, again Run the command “git clone <repository_url>” . Now the repository will be cloned.

7. Make a new file “index.html” and write desired code in it as given below in the screenshot.

![p10](https://user-images.githubusercontent.com/69754757/225607729-84436dc9-5d0e-4f66-a98f-948a28ca32e6.png)

8. Push the local changes to CodeCommit repository Using the command “git add .” , git commit -m “added sample” , “git push origin master”.

9. Open CodeCommit. Go to your repository and click on it, You will be able to see “index.html” file in your repository

![p11](https://user-images.githubusercontent.com/69754757/225608025-c1eb4cde-2d55-4a92-8d82-d9ed85a0ed09.png)

# →Now Let’s create a CodeBuild:

1 . Go to AWS CodeBuild page and click “Create Project”

![p13](https://user-images.githubusercontent.com/69754757/225608332-523690bb-7868-4864-8abd-8b60f994ba05.png)


2. Enter the project name.

![p12](https://user-images.githubusercontent.com/69754757/225608579-1c41cce1-2d78-480b-9d5c-201c6d03e998.png)

3. Next, choose the source location of the code AWS CodeBuild will clone on its server. In this case, the source is my website’s AWS CodeCommit repo’s master branch.

![p14](https://user-images.githubusercontent.com/69754757/225608691-1d878b2d-524a-4ed3-b955-a05c51f634dd.png)

4. Next I will choose the operating system image that I want to be running on the server building my project. I chose Ubuntu in this case.

![p15](https://user-images.githubusercontent.com/69754757/225609638-eca12f6a-9e13-43f4-bf81-489ac2215526.png)

5. buildspec File → This is a yaml file called buildspec.yml that should be placed in the root of my repository project, and AWS CodeBuild looks for it after cloning the repo to follow the instructions declared in it.

Add buildspec.yaml file to CodeCommit Repository and complete the build process.

![p16](https://user-images.githubusercontent.com/69754757/225610265-919bb6c8-254e-430e-97b7-4f1c676e83e3.png)

Go to vs code ,create buildspec.yml file.Add configurations to install nginx as given below in the screenshot and save the file.

![p17](https://user-images.githubusercontent.com/69754757/225610659-f1ee0f8a-9715-4074-ae79-655f112325c7.png)

AWS CodeBuild to execute certain commands at different phases of the build process. These phases are named “install”, “build”, and “post_build”. I will only be using the install and build phases to install dependencies and build my webapp.The artifacts section specifies the files that should be included in the output artifact produced by the build process. In this case, the files section specifies that all files and directories in the build output should be included in the artifact. The **/* pattern matches any file or directory recursively in the build output directory


The buildspec.yml file will be visible in CodeCommit.
![p18](https://user-images.githubusercontent.com/69754757/225611270-fc0bd281-531d-43e3-9d94-fd5f6d902c29.png)

6. Go back to CodeBuild where you left the Task 1. Scroll down and click on “Create build project”.

![p19](https://user-images.githubusercontent.com/69754757/225611551-36888f88-66f9-4a84-8c28-27771aeca45f.png)


7. Your project will be created successfully. Click on “Start build”.
![p20](https://user-images.githubusercontent.com/69754757/225612087-9e0bc8e5-14d4-4280-ae7b-c99b4942d124.png)

Project will start building and build successfully.


![p21](https://user-images.githubusercontent.com/69754757/225612617-47370cc0-b02f-4b92-b0a1-c744fafc9965.png)

If you want your project to be build at a specific place, then you can specify the artifact upload location.

8. First create ‘S3 bucket’

![p22](https://user-images.githubusercontent.com/69754757/225613417-534ce35c-3954-4100-8e71-264b9b5d3987.png)

9. In build projects, Edit and choose ‘Artifacts’.

![p23](https://user-images.githubusercontent.com/69754757/225613747-5795d9d1-a2ca-4868-aed1-28cad1b15eb4.png)

10. Before create artifact , Create folder which will be use in artifact setup

![p24](https://user-images.githubusercontent.com/69754757/225614077-ab11a2fc-a410-41ad-9350-434e1714957c.png)

11. In Artifacts, select artifact type as Amazon S3 and choose bucket name also create a folder, click on “update artifacts”

![p25 0](https://user-images.githubusercontent.com/69754757/225617046-01d3f43d-585b-4f33-b164-e8df12282829.png)


![p26 0](https://user-images.githubusercontent.com/69754757/225617086-80d24ee3-e9b1-4291-a376-07db0c7b5d3d.png)

12. Artifact upload location successfully added. Click on ‘Start build’

![p27](https://user-images.githubusercontent.com/69754757/225615578-03ff5c64-96d5-4758-8804-f4e295fedfae.png)

Build is Succeeded.
![p28](https://user-images.githubusercontent.com/69754757/225615906-fe315a04-0e05-4679-9110-bfcc3a9a1a9f.png)


# What is CodeDeploy?
AWS CodeDeploy is a deployment service that automates application deployments to Amazon EC2 instances, on-premises instances, serverless Lambda functions, or Amazon ECS services.

AWS CodeDeploy allows developers and administrators to centrally control and track their application deployments across their different development, testing, and production environments. The service scales with your infrastructure so you can easily deploy to one EC2 instance.

# Flow of execution
Process For Code Deploy, we will:

Create application

Create Deployment Group

Create Deployment

Create 2 IAM roles we will use in this blog:

IAM role for CodeDeploy to talk to EC2 instances.

IAM role for EC2 to access S3.


