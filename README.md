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
