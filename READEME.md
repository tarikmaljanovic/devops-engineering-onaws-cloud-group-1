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
#### Task 1: Creating a virtual network
#### Task 2: Creating a virtual machine
#### Task 3: Testing the deployment

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
