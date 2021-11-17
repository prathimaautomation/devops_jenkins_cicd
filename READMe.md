# Let's build a Continuous Integration and Continuous Delivery/Deployment (CICD) Pipeline
## Jenkins
- Jenkins is an open source automation server. It helps automate the parts of software development related to building, testing, and deploying, facilitating continuous integration and continuous delivery.

### Webhooks with Git-hub
- A webhook is a mechanism to automatically trigger the build of a Jenkins project upon a commit pushed in a Git repository. In order for builds to be triggered automatically by PUSH and PULL REQUEST events, a Jenkins Web Hook needs to be added to each GitHub repository.
   
#### Automated Testing using Jenkins
- Jenkins is a popular CI orchestration tool. It provides numerous plugins for integration with multiple test automation tools and frameworks into the test pipeline. When it comes to test automation, Jenkins provides plugins that help run test suites, gather and dashboard results, and provide details on failures.
  
#### Automated Deployment on AWS EC2 for 2Tier architecture - Nodejs app and Mongodb  

- Jenkins Workflow
  
![](images/jenkins.png)

##### Contiounus Integration Continuous Delivery/Deployment 
![](images/CICD.png)

###### Let's break it down 
  ![](images/cicd_jenkins.png)

### For deployment job in Jenkins
- In the execute shell of CD job

```
# we need to by pass the key asking stage with below command:
ssh -A -o "StrictHostKeyChecking=no" ubuntu@ec2-ip << EOF	
# copy the the code
# run your provision.sh to install node with required dependencies for app instance - same goes for db instance (ensure to double check if node and db are actively running)

# create an env to connect to db
# navigate to app folder
# kill any existing pm2 process just in case
# launch the app
nohup node app.js > /dev/null 2>&1 & - use this command to run node app in the background

# To debug ssh into your ec2 and run the above commands
    

EOF
```
## Jenkins CI Lab - Solution

##### Steps
1. create a dev branch
2. checkout dev branch to work on the code and push
3. create a webhook in gitHub to trigger with every commit/push from your local host to trigger this job
4. create a prathima-test-dev job to test the dev branch as soon as the code is pushed and to trigger another job upon success(test pass)
5. create a prathima-merge job to merge the dev branch into the main and to trigger another job to deploy the code into the ec2 instance
6. 
##### Source Code Management

1. Set Branches to Build to develop
2. Under additional behaviours click add and "Merge before build"
3. name of repo "origin"
4. branch to merge "main"

### Post-Build Actions

#### Git Publisher

1. Add Post Build Action
2. Git Publisher
3. Push Only if Build Succeeds
4. Merge Results

--- 
Tigger deployment job if the merge was successfull
