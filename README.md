# Pugme Self Hosted Runner Git2S3 Sample Repo

## Introduction 

The purpose of this repository is first and foremost to provide a demonstration of 
how to use GitHub Actions to package source code as a zip artifact and upload to an 
S3 bucket. 

It also provides a natural replacement if using CodeBuild projects in share AWS accounts, 
where account wide authentication with Github can be prone to 
authentication errors if the CodeBuild service is accidentally disconnected or seeded 
with a token that does not have sufficient scope. 

## Ok, explain a little more ...
It is a project containing examples on how to add the Worfklow GitHub Action to your 
project that will, on a push event, run a GitHub action on a self-hosted runner that 
will zip your source code and publish it to an S3 bucket.  

The self hosted runner runs on an EC2 instance in your AWS account. This allows 
you to use a IAM instance profile to provide the necessary policy that allows the 
GitHub runner to upload to the S3 bucket. (See CF/runner.json)

The primary reason you would want to run a self-hosted runner is that it does not 
eat into your Github Action free minutes and you also do not need to provide IAM API Keys 
(via an IAM service account) to provide the permission to upload the artifact to S3. 

If however you do want to use native GitHub Action runners, use the 
github/workflows/trigger-github-runner-generic.yaml file as a template for your action. 
Be sure save the API Keys as secrets in your Github project and rotate them at least 
every 90 days. 

## And how do I use it?
* Create a project in GitHub
* Build an EC2 instance to host your GitHub runners and install the Docker daemon. 
  (see CF/runner.json)
* Build your Docker image (see Docker/README.md)
* Add github/workflows/trigger.yaml to your project branches (rename github to .github)
* Under Actions, Settings in your GitHub project, click "Add Runner". Copy the runner token 
  displayed in the instructions. 
* Go back to your EC2 instance and run a Docker container with the token you obtain in  
  the step above (see Docker/README.md). You will note that in your GitHub project your 
  runner is now in the idle state. 
* Make a change to your project and push. This will trigger the Github action to package 
  your source code and upload it to your S3 bucket. 



