
**      ///////       ---------------------------------- Terraform Assignments  -----------------------------------------       ////////**
=============
**Terraform Assingment-5**
=============

## Category
- AWS Resources
- Terraform modules
- Terraform State management and state locking

## Details

In this assignment, we will create an end-to-end infrastructure using Terraform modules.

## Must Do
- Create the following resources using terraform resource block :
    - Create 1 VPC 
        - eg : `ninja-vpc-01`
    - Create 4 Subnet
        - 2 public subnet
            - eg : `ninja-pub-sub-01/02`
        - 2 private subnet
            - eg : `ninja-priv-sub-01/02`
    - Create instances in it ( bastion and private instance)
    - Create 1 IGW
        - eg : `ninja-igw-01`
    - Create 1 NAT 
        - eg : `ninja-nat-01`
    - Create 2 Route Table
        - 1 for public subnet
            - eg : `ninja-route-pub-01/02`
        - 1 for private subnet
            - eg : `ninja-route-priv-01/02`

- call the root modules using wrapper code for reusability
- Achieve terrafom state managemnet using S3 and terrafom state locking using dynamodb.

NOTE: Please make maximum use of variables and output file 

## Good to Do
- Convert your code in two modules named Network and Security
- Use data source while calling modules.

## References
- https://www.terraform.io/docs
- https://registry.terraform.io/providers/hashicorp/aws/latest/docs
developer.hashicorp.comdeveloper.hashicorp.com
Documentation | Terraform | HashiCorp Developer
Documentation for Terraform, including Terraform CLI, Terraform Cloud, and Terraform Enterprise. (124 kB)
https://www.terraform.io/docs



Deepak
@channel
=============
**Terraform Assingment-4**
=============
## Infrastructure as a Code
### Task Description 

- Create the following resources using terraform resource block :
    - Create 1 VPC 
        - eg : `ninja-vpc-01`
    - Create 4 Subnet
        - 2 public subnet
            - eg : `ninja-pub-sub-01/02`
        - 2 private subnet
            - eg : `ninja-priv-sub-01/02`
    - Create instances in it ( bastion and private instance)
    - Create 1 IGW
        - eg : `ninja-igw-01`
    - Create 1 NAT 
        - eg : `ninja-nat-01`
    - Create 2 Route Table
        - 1 for public subnet
            - eg : `ninja-route-pub-01/02`
        - 1 for private subnet
            - eg : `ninja-route-priv-01/02`

**Note: Make maximum use of variables and output files**

**      ///////       ---------------------------------- AWS -----------------------------------------       ////////**
 
Ishaan Ambashta
**aws Assignment-03**
Hi @channel  here is your 3rd assignment :slightly_smiling_face:
:alert:  :alert:  :alert:
# You need to work on your tool cloud infrastructure design w.r.t 
1. Highly Availability
2. Disaster Recovery
3. Cost optimization
Kindly validate your design by your buddy and then start the implementation.

# After that create your infrastructure with one click , either from Jenkins or your script which uses your AWScli cmd mainly.

# suppose you need to upgrade your tool v1.0 --> v2.0 in between without downtime when your tool application is in running mode. Kindly come up with a deployment strategy that you should use in your tool implementation and show it in your design.

# Try to learn about the 6 deployment strategies.
(edited)



 
Ishaan Ambashta
**aws Assignment-02**
@channel here is your 2nd Assignment :slightly_smiling_face: Good Luck :ninja:
:alert: :alert: :alert:
"""Suppose client has a new requirement of setup service in one network and setup its management in another network. Client needs a setup of nginx as a web page hosting, but he has an issue as he needs a basic cache system + who can handle the requests smoothly + manages the requests according + need a middleware layer which helps them easily debug the service issue. So he called DevOps."""

"""You understood the problem statement and told them you would create 2 networks for management and service. For the middleware problem statement we need nginx again but as a reverse proxy."""

Kindly do the following day wise setup:

Day1: 
Create 2 vpc networks with min requirements
1 public subnet (management vpc and service vpc)
1 private subnet (management vpc)
2 private subnet (service vpc)
1 database private subnet (service vpc)
1 middleware private subnet (service vpc)

Create in such a way that both vpc networks can communicate with each other. Then setup nginx in service vpc under private subnet and use another nginx as a reverse proxy which can forward traffic from load balancer to nginx web hosting.

"""Client has another concern about security of the network, as not all resources should be allowed to each resource, so kindly restrict the rest of the traffic in route tables and Nacl".

Day2:
You need to manage 
route tables of both the networks in such a way that only your teammates ip addresses should be allowed to igw rest should be deny.
Also manage Nacl group in such a way that it should allow traffic on specific port ranges to subnetworks.

"""While you are doing work on instance, some how your key 🗝️ is lost somewhere or currupted, client raising this issue as p0 and ask us for recover the key or kindly setup new key so that they can login the server atleast."""

Day3:
Kindly find the possible ways through which we can login to the server , you can do this 
Either by volume mounting
Either by doing configuration changes through user data.
Or by creating your own server key as temporary key to login there.

Kindly perform all three one by one and analyse the result.

NOTE: 
All traffic should be blocked only specific ports and IP addresses should be allowed.
No secret and access keys, only roles and policy
No root login. 

GOOD TO DO: 
If above part is done then only perform this scenario. CloudFront can cache objects and serve them directly to users (viewers), reducing the load on your Application Load Balancer. CloudFront can also help to reduce latency and even absorb some distributed denial of service (DDoS) attacks. So if you need these benefits with less load on LB and basic ddos protection kindly attach cloudfront network in front of load balancer on http traffic forwarding.
(edited)



 
Ishaan Ambashta
**AWS Assignment -2**
@channel here is your 1st Assignment :slightly_smiling_face: Good Luck :ninja:
:alert: :alert: :alert:
"""Suppose your client has infrastructure running over the AWS cloud, but for the past few days, the client application has not been able to handle enough traffic and load, so he is thinking of setting up any reverse proxy for handling the load as middleware. He called you from the DevOps team and explained the problem statement. You have explained very well about the plan and design that you are going to perform.""" 

You were told that nginx needs to be set up in between your client and application service, which can handle the request, but we need to setup one more thing, which is the basic HA (high availability) and DR (disaster recovery) of that middleware setup. Tasks would be done day-wise.

Day 1: 
- Create instance and install nginx on that, after that create an AMI-1
- Create instance from the above AMI-1 and make V1
- Do some changes in same instance and  again create AMI-2 
- Create instance from the above AMI-2 and make V2
- Make both V1 and V2 AMI's 
- Now you have 2 AMI's total 

You have to continue the strategy with autoscaling group, attach asg on LB and follow the same strategy and make this highly available by testing load test on the nginx server so that it would autoscale at the time of load.
 
Attach the policy to asg and increase the stress according to policy mentioned then analyse the result. ( Try every policy )
    - Avg CPU utilization
    - Network bytes in/out
    - ALB requests count per target.
Somehow client needs version upgrade in Nginx so please upgrade V1 to V2 that you have made

"""But the client has complained to us that our new version V2 is not compatible with the service, so please revert back. You need to revert back to the previous version. """

Day 2: """Client has told you about the change in it's Nginx as he needs this tool as hosting webpage too, so you need to plan accordingly. Also, he has specially mentioned that all tasks should be performed from their AWS environment, which means all O/P would be done through EC2 only. """

- You need to pull image content which would be display at the time of webpage hosting from VCS git and push your images on S3 bucket using aws-cli. (Do not use secrete and access keys)

- You need to create a frontend including images in nginx page which will be fetched directly from S3 bucket.

Day3:
"""Now client has again told us to test it continuously to see if ASG is working or not if my server got unhealthy.""" 

Enter in the server and make some changes in server in order to make server unhealthy. Now analyze the result to see how ASG can help you to maintain your instance desire state.

==========================================
(Remember the special points from client)
NOTE 1: You need to create the utility in such a way that it will make AMI of specific version and attach to the asg and perform the rolling deployment strategie. In case of revert back you should also have the function of revert back feature. 

NOTE 2: But always remember first do it all the tasks manually.
==========================================

GOOD TO DO:
Do the whole automation with Blue Green Deployment and add CloudFront in front of Load Balancer to access the website in order to overcome latency.
Continue to the previous assignment 1 and use your both nginx AMI's for displaying webpage and use your images from S3 bucket.

Day4:
"""Client called devOps and asked if it was possible to get the two different details with single LB DNS, as he has two webpages and wants to pass the traffic through a single ALB but with a different path, like app.opstree.com/path1 or app.opstree.com/path2. """ 

You have told him yes, it is possible with path-based routing in the ALB. Now do the following:

## Use existing Nginx and there should be 1 ec2 in each private subnet .
    - 1 bastion host in public subnet .
    - port 22 of bastion host should only accessible from your public ip.
    - nginx welcome page with path '/ninja1' on first ec2 should display `Image-1`.
    - nginx welcome page with path '/ninja2' on second ec2 should display `Image-2`.
    - port 22 of  both the nginx servers should only be accessible from  bastion host.

## Create target group for each nginx server. (2 servers)
## Create Application load balancer.
    - port 80 open of nginx server should only be accessible from your ALB.
    - port 80 open of ALB should only be accessible from your public IP.
    - ALB should only be accessible though your public IP none else.
    - create listener rule so that {YOUR-ALB-DNS-NAME}/ninja1 should display welcome page of first ec2.
    - create listener rule so that {YOUR-ALB-DNS-NAME}/ninja2 should display welcome page of second ec2.

## Push all the updated images of the webpage to S3 bucket defined folders through any EC2 instance and maintain repo on that server only.

Day5: 
"""Client asked for S3 service and bucket to be deployed in the US-East-1 region and segregate the folders with env names with proper restrictions."""

## You need to create a IAM user and a S3 Bucket on any of the region, Kindly follow as mentioned below :
 - Create 2 folders prod and nonprod inside that bucket.
 - Upload any different image files inside both folders.
 - Create a role for the above specific task and it should only be access S3 full access
 - A bucket should only be accessible from your both root, IAM user and nginx application.
 - Restrict the access of IAM user to access prod folder but able to access the nonprod folder.
 - Set IAM and bucket policies in such a way that it accomplished the above points.

Day6:
"""Client facing issue with some policy in IAM. Earlier,  he assigned one policy to S3, but if he assigned the same to CDN, then it showed an error. He called the devOps for this anonymous issue.""" 

DevOps told him that it needs to be validated through a trust relationship in the IAM service

## suppose organization wants to get the page access quick, so you need to implement CDN and fetch the images through CDN instead S3, use same role in the CDN which you are using in EC2 without any modification of policy.

## Make your own IAM user and assign minimal permissions to yourself for this task.


 
Himanshi Parnami
**AWS Task -5 ** 
Create a S3 bucket and host a static website through S3 feature after that integrate cloudFront service with your S3 bucket to overcome the latency and then access your static website through cloudFront url. Now change the content and hit again remember cache will not be taken at that time
Nov 5th at 2:00 PM




**AWS Task -4 **
@channel  Task :
You need to create a bucket and try to versioning the objects inside the bucket and analyse the result. Once you made the bucket it'll only be accessible from your IAM user and after uploading the object just remove the write access, then try to dowload and upload the object and analyse the result.

Avoid giving * permission in policy.



** 
AWS-CLI task- 3**
Create a Instance inside VPC network if already exist if not then make whole infrastructure with the help of aws-cli tool

Perform operations below through aws-cli:
 - Start instance 
 - Stop instance
 - Restart instance
 - Terminate instance
 - Attach IAM role to that instance
 - Make ALB internet facing 

Good to do , If above implemented then implement this by aws-acli with single click, first do manually on console




** AWS Task -2**

@channel this is your ASG task :slightly_smiling_face:
Create an infrastructure with the following resources or use existing resources: 
  - VPC 
  - 2 public subnets 
  - 2 private subnets 
  - 1 instance on one of the private subnets 
  - create internet facing application load balancer 
  - create Autoscaling group and atteach your above load balancer 
  - attach CPU intensive dynamic tracking policy to your asg 
So in the above mentioned infrastructure, generate a CPU stress load on the server and analyse the result.
Try to complete your ASG and LB task by today.



 
**AWS Task -1 @channel**
You have to setup vpc network in your cloud and configure the following:
 - 1 VPC 
 - 1 public subnet 
 - 1 private subnet
 - 1 LB with 1 listner rule 80 
 - 1 Target group with 2 servers setup with nginx

perform the task with required configs and analyse the LB behaviour


 **      ///////       ---------------------------------- Jenkins Assignments  -----------------------------------------       ////////**

**Jenkins Assignment 6:**
"Create a Ansible shared library in Jenkins for your tool with following steps:
- clone
- User Approval
- Playbook Execution
- Notification
Required inputs for the shared library should be passed via configuration file
eg:
SLACK_CHANNEL_NAME  = build-status
ENVIRONMENT         = prod
CODE_BASE_PATH      = env/prod
ACTION_MESSAGE      = <channel message>
KEEP_APPROVAL_STAGE = "true"
:+1:
3

Oct 27th at 9:55 AM


 

**"Jenkin Assignment 5:**
Topics Covered:  (User Authentication, User Authorization)
     Assignment on Authentication and Authorization
        Their is an organization which has 3 teams
            - Developer
            - Devops
            - Testing
        First you need to create 9 dummy jenkins jobs.Each job will print their jobname, build number.
            For Developer create 3 dummy jobs.In developer view
                job1:- dev-1
                job2:- dev-2
                job3:- dev-3
            For Testing create 3 dummy jobs. In testing view
                job1:- test-1
                job2:- test-2
                job3:- test-3
            For Devops create 3 dummy jobs. In devops view
                job1:- devops-1
                job2:- devops-2
                job3:- devops-3
        Users in each team: 
            developer: [ They can see only dev jobs, can build it, see workspace and configure it ]
                - developer-1 
                - developer-2 
            testing: [ They can see all test jobs ,can build it, see workspace and can configure it, | They can also view dev jobs ]
                - testing-1 
                - testing-2 
            devops:  [ They can see all devops jobs ,can build it, see workspace and can configure it, | They can also view dev and test jobs  ]
                - devops-1 
                - devops-2
            admin
                -  admin-1 [ It will have full access ]
        See what Authorization strategy suits it and implement it.
        Also go through all authorization strategy
        Legacy mode
        Project Based
        Matrix Based
        Role-Based
        Point 2:-
        Enable SSO with Goggle"



 

 ** Jenkins Assignment 4:**
Create a Declarative CI pipeline for java based project that contains various stages like
Code checkout
Run below stages in parallel
- Code stability.
- Code quality analysis.
- Code coverage analysis.
Generate a report for code quality & analysis.
Publish artifacts.
Send Slack and Email notifications.
The user should have the option to skip various scans in the build execution. And before publish there should be an approval stage to be set in place to approve or deny the publish and if approved the step should execute and the user should be notified post successful/failed
Repeat the same using Scripted Pipeline.



 

 
Jenkin Tasks
What you will do:

In this lab we will create a Jenkins Declarative Pipeline exploring basic elements of pipeline :

Create a Jenkins pipeline that will print Hello World 
Add a parameter in Jenkins Pipeline that will take a name and print Hello <name>
Add a stage to print the code of the name provided if the code is present in secret file available in credential
Add an option to take user input while running the pipeline if we want to fail the pipeline
Add a stage to print success/failure message
Update pipeline to execute every 5 minutes
Ensure that if pipeline is running for more than a minute it should fail.
Oct 22nd at 12:30 PM


 

**Jenkins Assignment 3:**
Topics Covered:  (Configuring Agents, Various Methods, Distributing Loads, Executors, Assigning Nodes)
     Assignment on configuring Nodes
        Configure a Ubuntu node using execution of command on the master method. 
        - Make sure at any point of time maximum 5 jobs can be executed on this node.
        - Assign this node to Assignment 2: Part 1 
        Configure a RHEL node using  Launch slave agents via SSH method. 
        - Make sure at any point of time maximum 2 jobs can be executed on this node.
        - Assign this node to Assignment 2: Part 2
        Configure a CentOS node using Launch slave agents via SSH method. 
        - Make sure at any point of time maximum 3 jobs can be executed on this node.
        - Assign this node to Assignment 3
        Configure a Windows node using method of your choice
        - Download one sample application of .NET and build it on Windows Node.
Oct 20th at 9:50 AM


 

**Jenkins Assignment 2:**
Topics Covered: (Shell Scripting, Git, Freestyle Job, Paramteters, Upstream/Downstream, Slack + Email Notification)
    Part 1:-
      Create a Jenkins job via which you will be able to perform below operations & if        any of the step fails a Slack and Email notification should be sent:
      - Create a branch
      - List all branches
      - Merge one branch with other branch
      - Rebase one branch with other branch
      - Delete a branch

    Part 2:-
      Create 2 Jenkins Jobs that will:
      - Create a file
      - Add few content in the file "<Ninja Name> from Devops Ninja"
      - Publish the content using a web server
      The second job must get triggered automatically only after successful completion of the first job.
      If any of the step fails a Slack and Email notification should be sent.
      if all jobs run successfully Slack and Email notification should be sent.




Jenkins Assignment 1: CICD

Topics Covered: (Ansible, Jenkins, Plugins)
Step 1: Create an ansible role for Jenkins.
Step 2: Deploy Jenkins Master in remote server Using Ansible Role



 

**Jenkins Task**
What you will do:

In this lab we will explore how we can add & configure agent:

Add a node to your controller Jenkins master via SSH agent.
Ensure that at any point of time only 1 job can be executed on this slave.
Create a Jenkins Job that should read print the name of Agent on which that job is executing.
Ensure that if Jenkins job would be run between 9am-6pm then only it should be executed on the newly added node, else on the master node.
Add another EC2 agent which should create a server when a Jenkins job needs to be executed.
Oct 15th at 4:50 PM

**      ///////       ---------------------------------- Ansible Assignments  -----------------------------------------       ////////**
 

**Ansible Assignment-5**
Role on the assigned tool with following features: - Should be able to install version specific - Should be OS independent - COnfiguration should be variablelized - Try using jinja template - It should include Templates for the configuration files with all the dynamic value that needs to be updated. - It should include handlers ,but not along with the task. - User should have the options to execute the role on centos or ubuntu or together on both.




** Ansible Assignment-4**
Create a System manager ansible role with below feature

I should be able to manage softwares that needs to be installed
I should be able to manage user's on the system
I should be able to manage various git repository
Various folder structures that should exist on a VM
Think of other system specific settings that you should manage



 

**Ansile Assignment-3**

Setup an entire infra using ansible playbook on aws
Setup Spring3HibernateApp (https://github.com/opstree/spring3hibernate) on created infra using ansible playbook by following the below steps:
Install MySQL
Create the war file for Spring3HibernateApp using maven
Install JDK 11
Install Tomcat
Send the war file created earlier to path "/opt/tomcat/apache-tomcat-7.0.108/webapps/"
Restart tomcat service
(edited)
opstree/spring3hibernate
A java loaded application for various testing purpose
Website



 

**Ansible Assignment-2**

Install nginx in your servers(more then 2) and make sure the log files of nginx should not be granted more than 1 GB space on the nodes
Create equal number of websites as per your team  members and every members website should be hosted for only 2 hours and after every 2 hours another website should start displaying.
    - First 2 hours <team>.opstree.com should display content of tanya website
    - Next 2 hours <team>.opstree.com should display content of Heena website

Install Apache
Also Configure nginx to run as reverse proxy to apache after completing first point individually.


- Run the ansible commands in such a way that workers nodes are updated one by one and not altogether and also make sure using all type of strategies.



 

**ANSIBLE ASSIGNMENT-1**

Complete the following steps with the help of ansible modules:

UserManager:
Add NinjaTeam (Simulate Group) ex: team1
Add a User (Simulate) under a team ex: Nitish added to team1 Ensure below constraints are met:
A user should have read,write, execute access to home directory
All the users of same team should have read and excute access to home directory of fellow team members.
In home directory of every user there should be 2 shared directories
Team: Same team members will have full access
Ninja: All ninja's will have full access
Additional Features:

Change user Shell
Change user password
Delete user
Delete Group
List user or Team



**      ///////       ---------------------------------- Linux / Maven / git Assignments  -----------------------------------------       ////////**

# Assignment 8
Create a utility to manage build operations of a maven based java project such as:
- Mandatory
   - Genreate the artifact of project
   - Upload the artifact of project to local repo
   - Perform static code analysis of project using any of the tool, which will be provided as an argument in commandline
       - checkstyle
       - findbugs
       - pmd
       - Perform unit test case analysis of the project and let user give an option to either generate report in csv/xml/html for
            - Unit tests status
            - code coverage status
   - deploy the artifact to websever(tomcat)         
- Optional
   - Generate documentation of an  application
   - Update build definition to fail build if various thresholds are not met in 
      - checkstyle
      - findbugs
      - pmd
      - code coverage
Repo link : https://github.com/opstree/spring3hibernate.git
i.e 
./buildMaven.sh -a 
./buildMaven.sh -i 
./buildMaven.sh -s checkstyle
./buildMaven.sh -s findbugs
./buildMaven.sh -s pmd
./buildMaven.sh -t <unit_test_plugin_name>
./buildMaven.sh -d 

flag help
a : to generate a artifact
i : to install the artifact to local repo 
s : to do  any static code analysis 
t : to do any unit testing
d : to deploy the artifact
(edited)
Sep 26th at 8:22 PM


 

@here Assignment 7
## Git Assignment 7 - Part A
- Create a folder ninja at the root level of your cloned code
- Add a file README.md with content "Trying fast forward merge" in  ninja folder
- Create a branch ninja and move to it
- Run git status command
- Commit your changes to ninja branch
- Merge ninja branch to master branch make sure that a new commit get's created
- Assuming you are in the master branch, modify README.md with content "Changes in master branch", commit the changes in master branch.
- Switch to ninja branch, modify README.md with content "Changes in ninja branch", commit the changes in ninja branch.
- Merge the ninja branch to the master branch in such a fashion that a merge conflict is generated and resolve it using the ours and theirs concept so that the changes of the ninja branch overrides changes in master branch.

## Good To Do
- Simulate the above scenarios using rebase


## Part B
- Write a script to manage branches
    - Must
        - List branches
        - Create branch
        - Delete branch
        - Merge 2 branches
        - Rebase 2 branches
e.g:
```
./gitBranches.sh  -l 
output: 
master 
ninja
./gitBranch.sh -b <branch_name>
./gitBranch.sh -d <branch_name>
./gitBranch.sh -m -1 <branch_name1> -2 <branch_name2> ----> which means branch_name1 branch is going to merge into branch_name2 branch 
./gitBranch.sh -r -1 <branch_name1> -2 <branch_name2>---- which means branch_name1 branch is going to rebase on branch_name2 branch
```
- Write a script to manage tags
    - Must
        - Create tag
        - List tags
        - Delete tag
e.g:        
```
./gitTags.sh  -t <tag_name>
./gitTags.sh  -t ninja_1.0
./gitTags.sh  -t ninja_1.1
./gitTags.sh  -l 
output :
ninja_1.0
ninja_1.1
./gitTags.sh  -d <tag_name>
./gitTags.sh  -d ninja_1.0
````
- Write a script to generate commit report of a repo
    - Input
        - Repo url
        - days for which report to be generated
    - Output
        - Commit Id
        - Author name
        - Autoher EMail
        - Commit Message
        - Changed Files lists
    - Must Do
        - Report in html or csv format
    - Optional
        - An additional column showing if commit is valid or not
            - A commit is valide if it starts with pattern JIRA-XXXX: 
        
e.g :
```     
./gitCommitReport.sh -u <url> -d <days>
./gitCommitReport.sh -u https://github.com/opstree/spring3hibernate.git -d 40 
```
output:
```
Fri Dec 9 15:49:41 2022 +0530 | Sandeep | sandeep@opstree.com | Updated path to correct value
Sat Dec 3 10:28:04 2022 +0530 | Sandeep Rawat | sandeep@opstree.com | Merge pull request #40 from opstree/msk-tf-files
Fri Dec 2 18:16:18 2022 +0530 | priyanshichauhan0707 | priyanshichauhan0707@gmail.com | renamed data_network.tf
Fri Dec 2 17:52:09 2022 +0530 | priyanshichauhan0707 | priyanshichauhan0707@gmail.com | added _override.tf, backend.tf and data.tf
Fri Dec 2 11:59:55 2022 +0530 | Sandeep | sandeep@opstree.com | Added capability to fetch & store state in S3

```
GitHubGitHub
GitHub - opstree/spring3hibernate: A java loaded application for various testing purpose
A java loaded application for various testing purpose - GitHub - opstree/spring3hibernate: A java loaded application for various testing purpose (64 kB)
https://github.com/opstree/spring3hibernate.git





ASSIGNMENT 6

Part A
Please find your assignment for today

Create a process management utility, to find


Top n process by memory
Top n process by cpu
Kill process having least priority
running duration of a process by name or pid
List orphan process if any
List zoombie process if any
Kill process by name or pid
List process that are waiting for the resources

i.e.
./ otProcessManager topProcess 5 memory
./ otProcessManager topProcess 10 cpu
./ otProcessManager killLeastPriorityProcess 
./ otProcessManager RunningDurationProcess <processName>/<processID>
./ otProcessManager listOrphanProcess
./ otProcessManager listZoombieProcess
./ otProcessManager killProcess <processName>/<processID>
./ otProcessManager ListWaitingProcess

Part B

Process Manager utility

Create a  ProcessManager utility that will perform below operation:


register a service which it will start as a daemon service( it will register script path and one alias to this service)
start a particular service
show the  status of particular service(shows whether a service  is running or not)
stop a particular service
change the priority of any service
list the   details  of particular  service started by this utility


 i.e.
./ProcessManager.sh -o register -s <path> -a <alias> -> Register Process
./ProcessManager.sh -o start -a <alias> -> Start Process
./ProcessManager.sh -o status  -a <alias> -> status of  processes
./ProcessManager.sh -o kill -a <alias> -> Kill process
./ProcessManager.sh -o priority -p <low/med/high> -a <alias> -> change priority
./ProcessManager.sh -o list  
output:
service2
service1
service3
./ProcessManager.sh -o top [-a <alias>] -> List process details
output:
 alias, PID, State, Priority, Script

Part C

Let's play around with process:


clear a log file of running process
delete a log file of running process and see what happens to process
elevate the priority of a process



 

ASSIGNMENT 5

Part A
Create a template engine, that can generate values file and replace the variables provided as arguments

./templateEngine.sh template.file key1=value1 key2=value2....


trainer.template
{{fname}} is trainer of {{topic}} 



i.e 
./templateEngine.sh trainer.template fname=sandeep topic=linux

sandeep is trainer of linux 



Part B
Create a text editor utility, using which you can

Add a line at top
Add a line at bottom
Add a line at specific line number
Replace word
Delete word
Insert word
Delete a line
Delete a line containing a word


./otTextEditor addLineTop <file> <line>
./otTextEditor addLineBottom <file> <line>
./otTextEditor addLineAt <file> <linenumber> <line>
./otTextEditor updateFirstWord <file> <word1> <word2>
./otTextEditor updateAllWords <file> <word1> <word2>
./otTextEditor insertWord <file> <word1> <word2> <word to be inserted>
./otTextEditor deleteLine <file> <line no>
./otTextEditor deleteLine <file> <line no> <word>


Also come with your own features of text editor






 

# ASSIGNMENT 4
Create a utility otssh, this utility will have below features
- add ssh connect
- list ssh connection
- update ssh connection
- delete ssh connection
- Connect




## Add ssh connection

```
$ otssh -a -n server1 -h 192.168.21.30 -u kirti (add user kirti to connect 192.168.21.30 with name server1 with default ssh setting)
$ otssh -a -n server2 -h 192.168.42.34 -u kirti -p 2022 (add user kirti to connect 192.168.42.34 with name server2 with port 2022 and default ssh setting)
$ otssh -a -n server3 -h 192.168.46.34 -u ubuntu -p 2022 -i ~/.ssh/server3.pem (add user ubuntu to connect 192.168.46.34 with name server3 with port 2022 and ssh key file ~/.ssh/server3.pem and default ssh setting)

```


## List ssh connection
```
i.e 
$ otssh -l (This should list the name of all connection added using utility)
server1
server2
server3
$ otssh -l  -d (This should list the name of all connection with details added using utility)
server1: ssh kirti@192.168.21.30
server2: ssh -p 2022 kirti@192.168.42.34
server3: ssh -i ~/.ssh/server3.pem -p 2022 ubuntu@192.168.46.34

```

## Update/modify ssh connection (This should update the settings for connection mentioned after name)
```
$ otssh -m -n server1 -h 192.168.21.30 -u user1
$ otssh -m -n server2 -h 192.168.42.34 -u user2 -p 2022
$ otssh -l -d
server1: ssh user1@192.168.21.30
server2: ssh -p 2022 user2@192.168.42.34
server3: ssh -i ~/.ssh/server3.pem -p 2022 ubuntu@192.168.46.34
```


## Delete ssh connection (This should Delete the mentioned connection)

```
$ otssh -r server1
$ otssh -r server2
$ otssh -l -d
server3: ssh -i ~/.ssh/server3.pem -p 2022 ubuntu@192.168.46.34

```






# ASSIGNMENT 3
## Part A
Please find your assignment for today 

Create a shell script to generate a star, it will take 2 arguments size & type
```
./drawStar.sh 5 t1
    *
   **
  ***
 ****
*****
```

```
./drawStar.sh 5 t2
*
**
***
****
*****
```

```
./drawStar.sh 5 t3
    *
   ***
  *****
 *******
*********
```

```
./drawStar.sh 5 t4
*****
****
***
**
*
```

```
./drawStar.sh 5 t5
*****
 ****
  ***
   **
    *
```

```
./drawStar.sh 5 t6
*********
 *******
  *****
   ***
    *
```

```
./drawStar.sh 5 t7
    *
   ***
  *****
 *******
*********
 *******
  *****
   ***
    *
```

## Part B
Create a shell script that will take take a number and print below output depending on the conditions
- tom -> If number is divisible by 3
- cat -> If number is divisible by 5
- tomcat -> If number is divisible by 15
```
i.e
./printTomcat.sh 7

./printTomcat.sh 6
tom

./printTomcat.sh 10
cat

./printTomcat.sh 30
tomcat
```
:+1::+1::skin-tone-2::+1::skin-tone-4:
11
:white_check_mark:
1

Sep 14th at 8:05 PM



ASSIGNMENT 2

Please find your assignment for today (Day2)

UserManager utility

Add NinjaTeam (Simulate Group) ex: team1
Add a User (Simulate) under a team ex: Nitish added to team1


Ensure below constraints are met:

A user should have read,write, execute access to home directory
All the users of same team should have read and excute access to home directory of fellow team members.
others should have only execute permission to user's home directory
In home directory of every user there should be 2 shared directories

team: Same team members will have full access
ninja: All ninja's will have full access

i.e
./UserManager.sh addTeam amigo
./UserManager.sh addTeam unixkings
./UserManager.sh addUser Rakesh amigo
./UserManager.sh addUser Sandeep unixkings

Resultant Structure
/home
  - Rakesh
    - team
    - ninja
  - Sandeep
    - team
    - ninja

Additional Features
change user Shell
change user password
Delete user
Delete Group
list user or Team
i.e 
./UserManager.sh delTeam amigo

./UserManager.sh delUser Rakesh

./UserManager.sh changePasswd Rakesh

./UserManager.sh changeShell Rakesh /bin/bash

./UserManager.sh ls User

./UserManager.sh ls Team
:+1:
5

Sep 12th at 9:08 PM


 

## ASSIGNMENT 1.1: Basic Linux Commands

Create a utility(FileManager.sh) that will be able to
- Create a Directory
- Delete a Directory
- List Content of a Directory
- Only listfiles in a Directory
- Only listDirs in a Directory
- listAll(files and directory)


For example
```
./FileManager.sh addDir /tmp dir1
./FileManager.sh addDir /tmp dir2
./FileManager.sh addDir /tmp dir3
./FileManager.sh listFiles /tmp
./FileManager.sh listDirs /tmp
./FileManager.sh listAll /tmp
./FileManager.sh deleteDir /tmp dir3

```



Update FileManager to process Files as well
- Create a file
- Add content to file
- Add conent at the begining of the file
- Show top n lines of a file
- Show last n lines of a file
- Show contents of a specific line number
- Show conteint of a specfific line number range
- Move/Copy file from one location to another
- Delete file

For example
```
./FileManager.sh addFile /tmp/dir1 file1.txt
./FileManager.sh addFile /tmp/dir1 file1.txt "Initial Content"
./FileManager.sh addContentToFile /tmp/dir1 file1.txt "Additional Content"
./FileManager.sh addContentToFileBegining /tmp/dir1 file1.txt "Additional Content"
./FileManager.sh showFileBeginingContent /tmp/dir1 file1.txt 5
./FileManager.sh showFileEndContent /tmp/dir1 file1.txt 5
./FileManager.sh showFileContentAtLine /tmp/dir1 file1.txt 10
./FileManager.sh showFileContentForLineRange /tmp/dir1 file1.txt 5 10
./FileManager.sh moveFile /tmp/dir1/file1.txt /tmp/dir1/file2.txt
./FileManager.sh moveFile /tmp/dir1/file2.txt /tmp/dir2/
./FileManager.sh copyFile /tmp/dir2/file2.txt /tmp/dir1/
./FileManager.sh copyFile /tmp/dir1/file2.txt /tmp/dir1/file3.txt
./FileManager.sh clearFileContent /tmp/dir1 file3.txt
./FileManager.sh deleteFile /tmp/dir1 file2.txt

```
Note: Do not use sed command.Try to do this assignment only with linux basic commands



Assignment -01
 
In this Assignment  we will cover some basic command of linux
- First check your current working directory 
- Now create directory with name "linux" in your current directory.
- Then create a another directory  with name "Assignment-01" inside your "linux" directory  .
- Now create one more directory inside "/tmp" with name "dir1" without changing your present directory.
- At last create two more directories having below tree structure .It should create a below structure via single command only .
```
/tmp
  - dir1
      - dir2
        - dir3 
        
```   
- Find a command  that will delete a "dir3" that you have created before. 
- Now create a empty file with your "firt-name"  in /tmp directory.
- After creating a empty file , add "This is my first line " into a file without using any editor.
- Now add  one more line "this is a additional content " into a same file .Make sure it will not overwrite the previous line of the file.
- Then  create new  file with your  "last-name" along with some content like "last-name is my last name".Do not use any editor
- Now add "this is line at the  beginning" into "last-name" file  in such a manner that it will add the line at beginning of the file.Do not use any editor.
- Then add some more 8-10  lines to the same file .
- Now find a command that will show:
  - top 5 lines of the file.
  - bottom 2 lines of the  file.
  - only 6th line  of the file.
  - 3-8 lines of the file .

- Find a command that will list  below things of /tmp directory
  - list all content(including hidden files)
  - list only files
  - list only directories 
- Now copy the "last-name" into the /tmp/dir2 with same name.
- Then again copy the "last-name" into the /tmp/dir2, this time with different name i.e "last-name".copy 
- Now change the name of the "first-name" file  to some other name at same location .
- Find a command that will  move the "last-name" file  to /tmp/dir1
- find a command that will clear the content of /tmp/dir2/"last-name".copy .Make sure it will not even contain  empty line .
- Now delete the same file i.e /tmp/dir2/last-name.copy 

Note : Do not use sed command in this assignment.


 


 
