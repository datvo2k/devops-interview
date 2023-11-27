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

#### Kubernetes
###### Explain replication controller in kubernetes?
A replication controller is responsible for running the specified number of pod copies across the cluster. Create X number pods present.

###### What is pv and pvc in kubernetes? What role do they play?
- PV -> Persistent Volume
- PVC -> Persistent Volume Claim
- POD -> PVC -> PV -> Volume(NFS, EBS)

###### A pod is trying to access a volume but it gives access error. We would like this pod to have access to this volume. What can we do to achieve the same?
- The issue cloud be appear because of AccessMode of volume
- Not all PV allow multiple pod access
- in K8S: ReadWriteOnce, ReadOnlyMany, ReadWriteMany, ReadWriteOncePod
- Example NFS allows ReadWriteMany
- EBS allows only ReadWriteOnce

###### What is side car container?
A sidecar container runs parallel to the main application container. The reason to use a sidecar container can be for different reasons. For example, in Istio the sidecar container is used as a proxy for managing incoming traffic for the main container, it can also be used for logging, monitoring purposes, and more.   
Remove certain complexities when we build application.   

###### How does the K8S scheduler quickly assign worker nodes for the pod? Explain the internal working of K8S's scheduler.
###### You have 10 nodes with 500gb of disk attached to each node. Let us say the node disk space reached 85% usage, then the pod we have deployed should get evicted and re-deployed on a node with better disk health. Explain if this can even be done?

#### AWS
###### What is instance fleet in AWS?
- An EC2 Fleet contains the configuration information to launch a fleet - or group - of instances. in a single API call, a fleet can launch multiple instance type across multiple AZ, using the On-Demand instance, Reserved Instance, and Spot Instance purchasing options together. 
- Define separate On-Demand and Spot capacity targets and the maximum amount you're willing to pay per hour.
- Specify the instance types that work best for your applications.

###### What is vertical scaling and horizontal scaling. Explain with use case you have seen?
- Implement Vertical Scaling if feel that our application requires more CPU and RAM. (multi processing, more features application)
- Horizontal Scaling is more about handling the traffic.

###### Cloud you explain how you would block an IAM user form accessing a specific S3 bucket?
- Using s3 bucket policy. ARN-IAM -> blocked

###### Why do we have 3 different kind of IAM policy types? (Managed, Customer Managed and Inline Policy)
- Managed policy - AWS created and maintained policy.
- Customer Managed - Customer created and managed policy
- Inline policy - Created and attached directly to IAM User, Group and Role

###### What is ingress and egress? Where are these terms mostly associated?
- Ingress -> Incoming traffic
- Egress -> Outgoing traffic

###### Auto Scaling group for a project is having issues with getting/provisioning new nodes. It's using complete spot instances. What could be the issue?
###### How is your K8S setup done on AWS?
- using kops. 
###### What are the load balancers in AWS. Briefly explain which one you have used and uses of others.
- Classic LB: Round robin traffic routing
- ALB: path based routing multiple ASG balancing.
- Network LB: streaming service. Use network layer. (TCP protocol)
- Gateway LB: Target groups support the Generic Networking Virtualization. Runs within one AZ

###### What is a marketplace AMI?
AWS marketplace is a place where I can find external software or OS that I can use without needing to sign a specific contract with organization. 

###### What is a lag in read replica in RDS?

#### Terraform
###### When using terraform to create a RDS, how to save the DB username and password securely?
- We should never commit these information in github repo
- USing vault integration or KMS

###### What is remote-exec in terraform and when will you use it?
###### How to validate the variable during terraform plan time? Example you take a variable called AMI. We need to make sure its of a proper format.
###### What does terraform state lock really mean? Do we have a practical use of it?
- If supported by your backend, terraform will lock your state for all operations that could write state.
- this prevents others form acquiring the lock and potentially corrupting your state.
- State locking happens automatically on all operations that cloud write state.
- You wont see any message that it is happening. If state locking fails, terraform will not continue.
- You can disable state locking for most commands with the -lock flag but it is not recommend.
- If acquiring the lock is taking longer than expected, terraform will output a status message.
- If terraform doesn't output a message, state locking is still occurring if your backend supports it.

#### Prometheus
###### Explain difference way in which prometheus can get metrics?
- Pull based approach -> application metrics endpoint
- Prometheus saved data after scrape on local. 

###### Your development team needs your help to monitor the API endpoint. Which HTTP response would you monitor and when will you trigger the alert?
- Any endpoint get call then you will get different response (check HTTP response code)
- If HTTP response code is 400 or 500 range then we can trigger the alert.

###### What are some ways in which you have setup alerting?
- Prometheus and Alertmanager trigger through messages.

###### Please explain how you create your dashboard for monitoring services in your current project?
- Present the metrics
- K8S -> Grafana
- AWS project -> cloudwatch

#### Helm
###### Do you using helm? Which version do you use currently and do yo usee benefit of using helm?
- Helm is basically packaging all your k8s file into a single chart format which help in:   
[x] Deployment   
[x] Rollback   
[x] upgrade   
[x] Prod, Staging, Dev setup

###### Why use Helm in k8s?
- Helm Chart help you define, install, and upgrade even the most complex K8S application.
- It becomes complex when you have a lot of yaml to handle (deployment, backup, service, serviceaccount etc)
- Charts are easy to create, version, share, and publish

###### Which helm repository do you use today to store/access repository?

#### CI/CD
###### Can we have a jenkins agent which is a docker container and run our test inside this docker container?
###### Have you use Jenkins in multi node setup? if yes, could you explain how to add a new slave/followed to master?
###### What is a blue-green deployment?

#### Python
###### Explain which python module will you use to make a simple API testing code. The code should jest check if a API checkpoint is working or not
```
import requests
status_code = requests.get(website).status_code
```
###### Explain in simple terms what is a package python?
- python package -> module -> function

###### We have a on-premises linux server which needs some monitoring enabled. Being a devops enginner only you have access to this server. How would you setup a basic monitoring script on this on premises server?
```
import psutil

# CPU time
print(psutil.cpu_times())

# RAM
print(psutil.virtual_memory())
```

###### Which build tool are you aware of and what are the build tools used in your project?

#### Devops
###### How do you handle incidents in your team? What DevOps best practices you have implemented for the same?
- Monitoring (cloudwatch, prometheus, ...)
- Alerting(SNS, alertmanager, ...)
- Collecting metric in application, write alerting rules

###### What do you think is the future trajectory towards your journey of being Devops engineer?
###### Tell me about yourself and what are you day to dat task being a DevOps engineer?
###### What is the difference between webserver and application server?