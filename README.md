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
