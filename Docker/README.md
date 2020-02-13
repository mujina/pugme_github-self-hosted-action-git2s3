## Instructions 
Log into your EC2 instance built with CF/runner.json using ssh 
* <code>ssh -i ~ssh/my_aws_private_key.pem ec2-user@$instance-name</code>

Build the GitHub Runner Docker Image (Assumes Dockerfile in local directory)
* <code>docker build -t github-runner .</code>

Run the Docker container after obtaining your Runner Token from your GitHub project 
* <code>docker run -d --restart always --name "${my-project}"-runner \
  -e REPO_URL="https://github.com/tr/${my_project}" \
  -e RUNNER_NAME="demoapp-runner" -e RUNNER_TOKEN="{$MY_TOKEN}" \
  -e RUNNER_WORKDIR="/tmp/github-runner" -v /var/run/docker.sock:/var/run/docker.sock \
  -v /tmp/github-runner:/tmp/github-runner github-runner:latest</code>