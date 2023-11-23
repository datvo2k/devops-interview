#### Linux
###### Your EC2 instance is running out of disk space. What actions will you take to mitigate the issue?
- EC2 disk space = EBS volume
- first check if its a root volume or other volume.
_ /root OS
_ /application
- If it root volume I will first try check logs and clear some space if not the instance might shut down also. /var/log or /tmp
- If its application volume, I will use EBS feature to take snapshot and increase disk space. Check application and delete deployment not cleaned.

###### What is bastion host or gateway server? What role do they play?
- A bastion server is used to manage access to an internal or private network from an external network. - sometimes called a gateway server or jump box or jump server.
- Writing log users access bastion host. To check, monitor income host.

###### Multiple EC2 instances in ASG is getting terminated and this is causing downtime on the application. EC2 pricing, quota all look good. How would you start debugging this issue?
When EC2 terminated because is unhealthy:
- disk space full.
- high CPU 100%. Find application take large CPU.
- No memory left

###### Create a linux script that will push certain logs to S3 automatically. Explain only high level design which is enough. Share what all steps you would do to achieve this above script.
- Using IAM role, access key.
- Bash script. Must be know kernel using, save log in /var/log/application-1/*
- linux cronjob

###### Why logging is important? What is centralised logging and what tools helps to achieve logging?
- Recording for application. Log can be json, text
- In AWS, can be dump S3, cloudwatch.

#### Git
###### How do you pass "message" when you commit your git code?
git commit -m "My message"

###### What is branch protection in github?
Make sure working-branch reviewed before merge.

#### Docker
###### how to check logs from my docker container and how to filter only last 200 lines from container logs?
- docker container logs container_name
- docker container logs -tail 200 container_name

###### What will happen to container logs if you restart the container? Will it be lost?
- Container are stateless, will lose log if you delete container.
- if containers are stopped and started or restarted then we wont't be losing any logs. (/var/log)

###### You encounter a docker image with size 2.7GB. Will this be a cause of concern? If yes how would tou tackle this?
- Bigger docker image would result in longer build time -> Smaller image base
- Docker image download error or API rate limit issue -> Multi-Stage Builds
- Application will also become bulkier -> Remove binaries after installing and don't install packages that isn't required.

###### What is difference between docker image and docker layers?
###### Explain CMD and ENTRYPOINT in docker. 
 - Only CMD: CMD["echo", "This is CMD"]
 - Only ENTRYPOINT: ENTRYPOINT["echo", "This is entryPoint"]
 - Both: ENTRYPOINT["echo"] \ CMD["This is EntryPoint"]

 - Both run during docker container runtime. Either one of theme are suggested to be used as best practice. Using both of theme in the same Dockerfile is also possible.
 