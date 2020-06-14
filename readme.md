# ACME App

- To stand up the kubernetes cluster go into the `environment` directory and follow the directions in the make file

Assignment 3 System Deployment and Operations

Name: Eng Wen Shing

Student ID : s3699661

Disclaimer: Due to the classroom github repository lacking of credits to be used in the circleci, i have used 2 other private repositories to perform testing for the code in circleci. My first repository also ran out of credits hence the second repository as well. Below attached are the screenshots of the repositories that has been created for this assignment.

SCREENSHOT OF GITHUB REPOSITORY:
![github1](https://github.com/RMIT-COSC2759-SDO/assessment3-student-s3699661/blob/master/screenshot/github1.png)
![github2](https://github.com/RMIT-COSC2759-SDO/assessment3-student-s3699661/blob/master/screenshot/github2.png)

Dependencies :
Terraform
- Download terraform for linux through this website: https://www.terraform.io/downloads.html
- follow the guide to install and move to bin folder in your linux machine ( sudo mv terraform user/local/bin )
- in terminal/shell, use 'terraform --version' to validate the installation.

Visual Studio Code
- The IDE that is reccomended to use when deploying this application is visual studio code. Any IDE would be able to work but Visual Studio code is highly recommended.
- You can download the linux version of Visual Studio Code through this link : https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2-linux.html

AWS Educate 
- An AWS Educate account is used to create the required configuration for the process in deploying the application.

Github
- A github repository is used for submission/sharing of this application. Therefore, it is highly recommended to clone this application and to share/configure through github.

Circleci
- Circleci is used for the creation and testing of the pipeline
- In Circleci, you can use github to access it making it easier as every push from the source code file would lead to it being tested instantly through the configuration file created for circleci.
- You can access the website circleci.com to speculate and to check whether the pipeline has passed or failed.

Deploy Instruction :
- In this assignment, the 3 main tools that has been used would be aws, terraform and circleci. Through these tools, terraform was used to instruct aws to create the components allowing the app to be deployed, tested and ran. With circle ci, the app was not only automated with its deployment, but also it's testing.
- To start the deployment of this application, firstly you have to access the makefile in the infra folder to fill up the credentials allowing terraform to access aws to create the components allowing the app to be deployed.
- Secondly, you will have to access the environment folder, and following the instructions of the makefile and performing and make up which would create the components for the deployment of the application.
- Lastly, you would want to push the application to github, with the config code file, circleci would follow through the code allowing for everything else to be automatically deployed and running.

Analysis of the problem:
Creating a helm chart: 
- Helm is a package manager that is meant for kubernetes to allow developers and operators to easily package,configure and deploy applications into the kubernetes clusters.
- In this assignment, upon looking through the provided files and folders, i realised that there was no helm file that has been created. Therefore, without the helm file, i wasn't able to create and to allow the database to configure with the application and its ports. Without the helm file, i would also not be able to create the deployment and service files to allow the application to be properly packaged, and database to be migrated.

Deploying application into non-production environment:
- A non-production environment would usually mean that it is not being deployed in a live prodcution time. A production environment would usually mean that the service/application is currently live and in real time usage.
- In the config.yml file for circleci in the folder, i have realised that there is only a production environment that is being given. Therefore, if there is only a production environment, this would mean that there is no testing environment. Hence, it is required to create multiple environments to allow the application to be updated when it hits different stages of progress and development.

Change e2e to run against non-production environment:
- e2e is a technique of testing that tests the entire softare product from the beginning to the end to ensure that the app runs as expected. It ensures that everything is working perfectly without any issues.
- In this assignment, after looking through the codes for circleci in the assignment, there is only 1 npm run which allows the e2e to be tested through the localhost:3000 which would mean that is it running in a production environment. This would be a problem as if any errors were to arise, there would only be 1 environment which means that everything would be affected and to cause problems.

Deploy application into production environment:
- As mentioned above, a non-production environment is to deploy an app into a not live setting. In this assignment, there wasn't a live production environment that would allow the app to be deployed anywhere. Upon having a non-production environment that would allow for testing, a production environment is also required for the deployment of the final product allowing consumers to be able to use and view them.

Create a stage gate before deployments are allowed into production:
- A stage gate is an authorisation gate that confirms the permission of deployment of files to the production environment. With the stage gate, less rollbacks would be made as everything would have to be confirmed before it being pushed as a final application to the production environment. In this assignment, setting aside the lack of test and production environment, there was also no stage gate that would stop the action of pushing to production before it being properly checked and finalised.

Cloudwatch and logging:
- As a specification in the assignment, amazon cloud watch is used and chosen as the monitoring and logging tool for the application. The amazon cloud watch provides data and insight from was to the users allowing the users to be able to access the application performance and operational data in forms of logs and metrics from a single platform. During the process of creating this application, a cloud watch logging tool is encouraged to be implemented as you would be able to see the performance of the application and how the data flows and runs.

Explanation and justification of solution:
Creating a helm chart:
- In this assignment, i have created a helm file which consists of the deployment file, service file, values file and chart file. 
- In the values file, it consists of variable values that allows the values to be passed on to the other file. Inside the values file there is the db username value, db password value, replica count value, image value, ECR image and db host value.
- In the deployment file, it consists of the deployment details that allows for the deployment of the application. Inside the deployment file, there are variables that would read through and to allow the db credentials and the image to be able to be passed through. Providing the deployment to have a more dynamic and flexible approach when it comes to the deployment of the application.

Deploying application into non-production environment:
- In this assignment, due to the lack of environments in this assignment. I have created 2 namespace environments for the assignment. The 2 namespace environments that i have created is a non-production environment called test and a production environment called prod.
- With helm and it's credentials, i was also able to utilise its command through the deployment file in helm calling and running the deployment file allowing circleci to automate the database and database migration script to be deployed and to ran against the database. 
- with helm upgrade, i was able to deploy the app through the image allowing for the application to be deployed through helm.
- with the kubernetes tool, i was also able to update the database of the application with sequelise db migrate.

Change e2e to run against non-production environment:
- For this specification, i have created another command which allows the e2e to instead being ran from the production environment link (localhost:3000) to instead to be ran and tested from a external static IP to be e2e tested.

Deploy application into production environment:
- In this assignment, a production environment was being given but without packaging the application and deploying it, there was simply no application to be deployed. Therefore, i have used helm to package the helm application files and also using helm upgrade to once again deploy the app files but this time instead of the test environment, it is being deployed into the production environment where it would be used in live time.

Create a stage gate before deployments are allowed into production:
- In this assignment, finally after the creation and deployments of the 2 environments, a stage gate was to be implemented in between them as a production environment is usually used for final product. For this, i have added in the workflow the stage gate where it has to be approved before it would be able to continue running.

Cloudwatch and logging:
- In this assignment, I have created an additional namespace for the cloud watch and also ensuring that the nodes has been created. In addition to that, I have also ensured that the logs has been deployed from the kubernetes cluster and to be stored in the cloud watch. I have also used applied and downloaded the fluent manifest file to ensure that the daemonset app for cloud watch would be created allowing for the logs to be deployed properly.


SCREENSHOT OF NAMESPACE BEIGN CREATED:
![namespacetest](https://github.com/RMIT-COSC2759-SDO/assessment3-student-s3699661/blob/master/screenshot/namespacetest.png)
![namespaceprod](https://github.com/RMIT-COSC2759-SDO/assessment3-student-s3699661/blob/master/screenshot/namespaceprod.png)

SCREENSHOT OF FAILURES CIRCLECI:
![failedcircleci](https://github.com/RMIT-COSC2759-SDO/assessment3-student-s3699661/blob/master/screenshot/failedcircleci.png)

SCREENSHOT OF ON HOLD APPROVAL CIRCLECI:
![onhold1](https://github.com/RMIT-COSC2759-SDO/assessment3-student-s3699661/blob/master/screenshot/onholdcircleci.png)
![onhold2](https://github.com/RMIT-COSC2759-SDO/assessment3-student-s3699661/blob/master/screenshot/onholdcircleci2.png)

SCREENSHOT OF FINAL SUCCESS INTEGRATION ON CIRCLECI:
![pass](https://github.com/RMIT-COSC2759-SDO/assessment3-student-s3699661/blob/master/screenshot/circlecipass.png)

SCREENSHOT OF CLOUDWATCH NAMESPACE AND CLUSTER INFO BEING CREATED:
![cloudwatch1](https://github.com/RMIT-COSC2759-SDO/assessment3-student-s3699661/blob/master/screenshot/cloudwatch1.png)
![cloudwatch2](https://github.com/RMIT-COSC2759-SDO/assessment3-student-s3699661/blob/master/screenshot/cloudwatch2.png)

cleanup instructions:

A make file has been created to ease the applying and destroying process of terraform for this application. In the make file there contains 2 commands that could be used :

make up : terraform apply --auto-approve

make down: terraform destroy --auto-approve

Application of make down is suggested for both infra folders, to ensure all components in aws has been shut down and no credits has been lost.