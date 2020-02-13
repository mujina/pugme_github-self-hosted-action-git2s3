## Instructions 
The runner.json file in this directory contains the CloudFormation required 
to build an EC2 instance in your AWS account with an IAM Role & 
associated instance profile that allows the GitHub self-hosted runners to upload 
artifacts to S3.

After you have built your EC2 instance with the CF/runner.json log into your 
EC2 instance using ssh to install Docker (if not done via user data of other means
)
* <code>ssh -i ~ssh/my_aws_private_key.pem ec2-user@$instance-name</code>
* <code>yum install -y docker</code>
* <code>sudo service docker start</code>

Add user to Group (Your Power User may be different)

* <code>usermod -a -G docker ec2-user</code> 

Logout (Ctrl-D) and login again. List running containers (there should not be any!)

* <code>docker ps -a</code>

Now follow instructions in Docker/README.md to build the Github runner image and 
run per-project Github runners. 
