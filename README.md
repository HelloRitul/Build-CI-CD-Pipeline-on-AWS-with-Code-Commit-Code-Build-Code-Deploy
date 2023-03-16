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

> Process For Code build, we will:

Create a Code Build Poject

Create buidspec.yml File

Create S3 bucket

Add Artifact

# →Let’s Create a CodeCommit:
