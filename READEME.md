# DevOps Engineering on AWS Cloud Project-Group 1

## Group Members
- Tarik Maljanovic
- Melisa Geca

## Repository Description and Structure
The following repository contains the documentation of the AWS Academy Project "Building a Highly Available, Scalable Web Application", the project code, project cost estimation, architecture diagrams
throughout the phases, and any additional scripts used to successfully finish a task. </br>
In the "application-code" directory resides the code of the website deployed for this project </br>
The "docs" directory contains: </br>
- Project Documentation labeled as "Documentation.md"
- Architectural diagrams throughout the phases which are labeled as "Architectural Diagram-Phase 2", "Architectural Diagram-Phase 3", "Architectural Diagram-Phase 4" (final version of the architectural diagram)
- The Cost Estimation file, labeled as "Cost Estimate.pdf"
- The Project Presentation

## Documnetation

### Phase 1: Planning the design and estimating cost
In this phase, we planned the architecture design and estimated the cost for the proposed solution. Here’s how we did it, step by step:
#### Task 1: Creating an architectural diagram

**Understanding Requirements**
- We started by thoroughly understanding the project requirements, including the necessary functionalities, scalability needs, and security considerations.

**Gathering Tools:** 
-  We utilized AWS Architecture Icons to ensure that architectural diagram was clear, standardized, and professional.
-  Referred to AWS Reference Architecture Diagrams to find examples and templates that aligned with our project requirements.

**Designing the Architecture** 
- Identified all the necessary AWS components for the solution, such as EC2 instances for compute resources, RDS databases for data management, AWS Secrets Manager for storing database credentials, VPC for creating the subnets on which EC2 instances are and making them publicly available and Cloud9 that provides an IDE for performing tasks such as creating secrets or migriting data to the database.
- Determined how these components would interact with each other to form a cohesive architecture.
- Using a diagramming tool, we drew the architecture diagram, clearly illustrating each component and their interactions. This visual representation helped in understanding the overall structure and flow of the solution.

**Ensuring Each Requirement Was Addressed**
- We made sure that each requirement was met by the proposed architecture. This included ensuring data flow efficiency, network architecture robustness, implementing security measures, and appropriately allocating resources.

![alt text](https://github.com/tarikmaljanovic/devops-engineering-onaws-cloud-group-1/blob/dev/docs/Architecture%20Diagram-Phase%204.png?raw=true)


#### Task 2: Developing a cost estimate

**Identifying Cost Components**
- Listed all the AWS services included in the architectural design, considering factors like usage patterns, instance types, data transfer, and storage needs.

**Using AWS Pricing Calculator**
- We used the AWS Pricing Calculator to develop a detailed cost estimate. Entered the specifics for each service (e.g., number of EC2 instances or database configurations for RDS) to calculate the monthly and annual costs.
- We ensured that the estimate reflected the costs to run the solution in the us-east-1 Region for 12 months.

**Reviewing and Adjusting the Estimate**
-Reviewed the cost estimate, comparing it with the project budget and making necessary adjustments. This involved optimizing resource usage, selecting cost-effective service options, and ensuring that the architecture was both efficient and cost-effective.

![image](https://github.com/tarikmaljanovic/devops-engineering-onaws-cloud-group-1/assets/116001161/973f3e0a-b6c6-4325-8bc4-98ea7bdbb82f)

- The full cost estimate could be found on [this link](https://github.com/tarikmaljanovic/devops-engineering-onaws-cloud-group-1/blob/dev/docs/Cost%20Estimate.pdf).

### Phase 2: Creating a basic functional web application
In this phase, the goal is to create a functional web application hosted on a single virtual machine within a virtual network on AWS. This will serve as a proof of concept (POC) demonstrating the ability to host the application on the AWS Cloud.
#### Task 1: Creating a virtual network
The first task is to create a Virtual Private Network (VPC) in the us-east-1 Region. Once we created the VPC, each Availability Zone (us-east-1a and us-east-1b) was assigned one public and one private subnetwork. Additionally, we created an Internet Gateway, a public and a private Route Table, a Network Address Translation gateway (NAT gateway), associated the public subnetworks with the public route table (the has a route to the Internet Gateway), and associated the private subnetworks with the private route table (that has a route to the NAT gateway). Lastly, we created a security group that allows inbound traffic of type HTTP from any IPv4 address and MYSQL/Aurora inbound traffic on port 3306 and source 10.0.0.0/16 (the CIDR of our VPC) for later tasks.
#### Task 2: Creating a virtual machine
Once the VPC was created and setup, we created our first EC2 instance that hosts a website and a MYSQL server. During the creation of the EC2 instance, we selected the computation specifications, the VPC and subnetwork the instance is associated with, the security group that would allow all inbound HTTP trafic, and entered our JavaScript code into the UserData field, the code installs the necessary dependencies and creates the "students" table for the "STUDENTS" database within the EC2 instance: </br>
```
#!/bin/bash -xe
apt update -y
apt install nodejs unzip wget npm mysql-server -y
#wget https://aws-tc-largeobjects.s3.us-west-2.amazonaws.com/CUR-TF-200-ACCAP1-1-DEV/code.zip -P /home/ubuntu
wget https://aws-tc-largeobjects.s3.us-west-2.amazonaws.com/CUR-TF-200-ACCAP1-1-79581/1-lab-capstone-project-1/code.zip -P /home/ubuntu
cd /home/ubuntu
unzip code.zip -x "resources/codebase_partner/node_modules/*"
cd resources/codebase_partner
npm install aws aws-sdk
mysql -u root -e "CREATE USER 'nodeapp' IDENTIFIED WITH mysql_native_password BY 'student12'";
mysql -u root -e "GRANT all privileges on *.* to 'nodeapp'@'%';"
mysql -u root -e "CREATE DATABASE STUDENTS;"
mysql -u root -e "USE STUDENTS; CREATE TABLE students(
            id INT NOT NULL AUTO_INCREMENT,
            name VARCHAR(255) NOT NULL,
            address VARCHAR(255) NOT NULL,
            city VARCHAR(255) NOT NULL,
            state VARCHAR(255) NOT NULL,
            email VARCHAR(255) NOT NULL,
            phone VARCHAR(100) NOT NULL,
            PRIMARY KEY ( id ));"
sed -i 's/.*bind-address.*/bind-address = 0.0.0.0/' /etc/mysql/mysql.conf.d/mysqld.cnf
systemctl enable mysql
service mysql restart
export APP_DB_HOST=$(curl http://169.254.169.254/latest/meta-data/local-ipv4)
export APP_DB_USER=nodeapp
export APP_DB_PASSWORD=student12
export APP_DB_NAME=STUDENTS
export APP_PORT=80
npm start &
echo '#!/bin/bash -xe
cd /home/ubuntu/resources/codebase_partner
export APP_PORT=80
npm start' > /etc/rc.local
chmod +x /etc/rc.local
```
#### Task 3: Testing the deployment
The deployment was tested by simply entering either the public IPv4 address or DNS record into the URL bar within the browser and seeing whether the website loads or not. If the website loaded sucessfully, we tested it further by entering some test data, updating it and deleting it.

### Phase 3: Decoupling the application components
#### Task 1: Changing the VPC configuration
#### Task 2: Creating and configuring the Amazon RDS database
#### Task 3: Configuring the development environment
#### Task 4: Provisioning Secrets Manager
#### Task 5: Provisioning a new instance for the web server
#### Task 6: Migrating the database
#### Task 7: Testing the application

### Phase 4: Implementing high availability and scalability
#### Task 1: Creating an Application Load Balancer
#### Task 2: Implementing Amazon EC2 Auto Scaling
#### Task 3: Accessing the application
#### Task 4: Load testing the application
