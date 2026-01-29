
![[Cloud Computing#What is Cloud Computing]]

# Infrastructure as Software

Cloud computing fundamentally changes how we think about IT infrastructure.

### Traditional Computing Model

Traditional Computing Model treats infrastructure as hardware.

**Characteristics of hardware solutions**:

- Require physical space in data centers
- Require staff to manage and maintain
- Require physical security measures
- Require extensive planning
- Require significant **[[Capital Expenditure]]** (upfront costs)
- Have long **[[Hardware Procurement Cycles]]**—acquiring, provisioning, and maintaining takes weeks or months
- Require provisioning capacity by guessing theoretical maximum peaks

### Cloud Computing Model

![[Cloud Computing#Core Characteristics of Cloud Computing]]

## Service Models

![[Cloud Computing#Cloud Service Models]]

## Cloud Computing Deployment Models

## Public Cloud

![[Cloud Computing#Public Cloud]]

## Private Cloud

Deploys resources on-premises using virtualization and resource management tools.

![[Cloud Computing#Private Cloud]]

## Hybrid Cloud

**Most common method**: Between the cloud and existing on-premises infrastructure.

**Purpose**: Enables organizations to extend and grow their infrastructure into the cloud while connecting cloud resources to internal systems.

![[Cloud Computing#Hybrid Cloud]]

## Multi-Cloud

![[Cloud Computing#Multi-Cloud]]

## Six Advantages of Cloud Computing

1. **Capital Expenses** (CapEx): Funds used to acquire, upgrade, and maintain physical assets like property, buildings, or equipment. 
	- **Cloud solution**: **Variable Expense**—pay only when you consume resources and only for the amount you consume.

2. **[[Economies of Scale]]**: By aggregating usage from hundreds of thousands of customers, providers like AWS achieve higher economies of scale.

3. You either have expensive idle resources (over-provisioned) or insufficient capacity (under-provisioned). 
	- **Cloud solution**: Access as much or as little as you need and **[[Elastic Scaling]]**—scale up and down with only a few minutes' notice.

4. New IT resources are available in **minutes**. Dramatic increase in **[[Organizational Agility]]**—the cost and time to experiment and develop are significantly lower.

5. Focus on projects that **differentiate your business** instead of infrastructure management.

6. Deploy applications in multiple **[[AWS Regions]]** around the world with just a few clicks.

## Categories of AWS Services

- **Compute**: Processing power ([[Amazon EC2]], [[AWS Lambda]])
- **Storage**: Data storage ([[Amazon S3]], [[Amazon EBS]])
- **Database**: Data management ([[Amazon RDS]], [[Amazon DynamoDB]])
- **Networking**: Connectivity ([[Amazon VPC]], [[Amazon CloudFront]])
- **Security**: Access control ([[IAM]], [[AWS WAF]])
- **Management**: Monitoring and automation ([[Amazon CloudWatch]])

## Choosing the Right AWS Service

Which service you choose depends on **business goals** and **technology requirements**.

### Example: Compute Services

AWS offers many compute options beyond EC2:

- **[[Amazon EC2]]**: Virtual servers in the cloud
- **[[AWS Lambda]]**: Serverless computing (run code without managing servers)
- **[[AWS Elastic Beanstalk]]**: Platform for deploying web applications
- **[[Amazon Lightsail]]**: Simple virtual private servers
- **[[AWS Batch]]**: Batch computing jobs
- **[[AWS Outposts]]**: AWS infrastructure on-premises
- **[[Amazon ECS]]**: Container orchestration service
- **[[Amazon EKS]]**: Managed Kubernetes service
- **[[AWS Fargate]]**: Serverless containers
- **[[VMware Cloud on AWS]]**: VMware workloads on AWS

## Three Ways to Interact with AWS

### 1. AWS Management Console

**[[AWS Management Console]]**: A web-based graphical interface.

### 2. AWS Command Line Interface (AWS CLI)

**[[AWS CLI]]**: A suite of command-line utilities.

- Can be launched from command scripts
- Supported on Linux, macOS, and Microsoft Windows
- Ideal for automation and scripting

### 3. Software Development Kits (SDKs)

**[[AWS SDKs]]**: Packages for accessing AWS in popular programming languages.

- Integrate AWS into existing applications
- Create applications that deploy and monitor complex systems entirely through code
- Programmatic access to AWS services

## AWS Cloud Adoption Framework (AWS CAF)

The **[[AWS Cloud Adoption Framework]]** (AWS CAF) provides guidance and best practices to help organizations successfully adopt cloud computing.

### Why AWS CAF Exists

**The challenge**: Cloud adoption requires alignment of three elements:

1. **People** (stakeholders, skills, culture)
2. **Process** (workflows, governance, operations)
3. **Technology** (infrastructure, services, architecture)

**The shift**: Cloud computing introduces significant changes in:

- How technology is obtained, used, and managed
- How organizations budget and pay for technology
- Organizational structure and responsibilities

**The need**: Organizations must discuss and consider fundamental changes across the entire organization, with stakeholder support from all units (within and outside IT).

### How AWS CAF Works

The AWS CAF helps organizations:

- Identify **gaps in skills and processes**
- Build a comprehensive approach to cloud computing across the organization and throughout the IT lifecycle
- Understand their **current state**, **target state**, and the **transition** needed
- Set goals and create processes for staff
- Create **prescriptive work streams** that support successful cloud adoption

## The Six Perspectives Explained

### Business Perspective

**[[Business Perspective]]** stakeholders:

- Business managers
- Finance managers
- Budget owners
- Strategy stakeholders

**Purpose**: Create a strong **business case for cloud adoption** and prioritize cloud adoption initiatives.

### People Perspective

**[[People Perspective]]** stakeholders:

- Human resources
- Staffing managers
- People managers

**Purpose**: Evaluate organizational structures, roles, skill requirements, and process requirements.

**Actions**:

- Perform analysis of needs and gaps
- Prioritize training, staffing, and organizational changes
- Build an **[[Agile Organization]]**

### Governance Perspective

**[[Governance Perspective]]** stakeholders:

- Chief Information Officer (CIO)
- Program managers
- Enterprise architects
- Business analysts
- Portfolio managers

**Purpose**: Focus on skills and processes needed to align IT strategy with business strategy.

**Goal**: Maximize business value of IT investment and minimize business risks.

### Platform Perspective

**[[Platform Perspective]]** stakeholders:

- Chief Technology Officer (CTO)
- IT managers
- Solutions architects

**Purpose**: Understand and communicate the nature of IT systems and their relationships using architectural dimensions and models.

**Focus**:

- Describe target state environment architecture in detail
- Implement new solutions on the cloud
- Migrate on-premises workloads to the cloud

**Includes**: Principles and patterns for implementation and migration.

### Security Perspective

**[[Security Perspective]]** stakeholders:

- Chief Information Security Officer (CISO)
- IT security managers
- IT security analysts

**Purpose**: Ensure the organization meets security objectives.

**Focus areas**:

- **Visibility**: Monitor and understand security posture
- **Auditability**: Track and record security events
- **Control**: Enforce security policies
- **Agility**: Respond quickly to security threats

**Actions**: Structure selection and implementation of security controls that meet organizational needs.

### Operations Perspective

**[[Operations Perspective]]** stakeholders:

- IT operations managers
- IT support managers

**Purpose**: Define how business is conducted day-to-day, quarter-to-quarter, and year-to-year.

**Focus**: Align with and support business operations.

**Actions**:

- Define current operating procedures
- Identify process changes needed for successful cloud adoption
- Plan training requirements

---

## Key Concepts to Review

### Cloud Computing Fundamentals

- [[Cloud Computing]]
- [[Pay-as-You-Go Pricing]]
- [[Data Centers]]
- [[Cloud Service Provider]]
- [[Traditional Computing Model]]
- [[Cloud Computing Model]]
- [[Capital Expenditure]]
- [[Variable Expense]]
- [[Operational Expense]]
- [[Hardware Procurement Cycles]]
- [[Elastic Scaling]]
- [[Organizational Agility]]

### Cloud Service Models

- [[Cloud Service Models]]
- [[IaaS]]
- [[PaaS]]
- [[SaaS]]

### Cloud Deployment Models

- [[Cloud Deployment Models]]
- [[Cloud Deployment]]
- [[Hybrid Deployment]]
- [[On-Premises Deployment]]
- [[Private Cloud]]

### Economic Concepts

- [[Economies of Scale]]
- [[Latency]]

### AWS Core Services

- [[Amazon Web Services]]
- [[AWS]]
- [[AWS Regions]]

### Compute Services

- [[Amazon EC2]]
- [[AWS Lambda]]
- [[AWS Elastic Beanstalk]]
- [[Amazon Lightsail]]
- [[AWS Batch]]
- [[AWS Outposts]]
- [[Amazon ECS]]
- [[Amazon EKS]]
- [[AWS Fargate]]
- [[VMware Cloud on AWS]]

### Storage Services

- [[Amazon S3]]
- [[Amazon EBS]]
- [[Amazon EFS]]

### Database Services

- [[Amazon RDS]]
- [[Amazon DynamoDB]]

### Networking Services

- [[Amazon VPC]]
- [[Elastic Load Balancing]]
- [[Amazon CloudFront]]

### Security and Management

- [[AWS Security Groups]]
- [[Network ACLs]]
- [[IAM]]
- [[AWS WAF]]
- [[Amazon CloudWatch]]
- [[Amazon Machine Images]]

### Traditional IT Components

- [[DAS]]
- [[SAN]]
- [[NAS]]
- [[RDBMS]]

### Web Technologies

- [[Web Service]]
- [[APIs]]
- [[XML]]
- [[JSON]]

### AWS Interaction Methods

- [[AWS Management Console]]
- [[AWS CLI]]
- [[AWS SDKs]]

### AWS Cloud Adoption Framework

- [[AWS Cloud Adoption Framework]]
- [[Perspectives]]
- [[Capabilities]]
- [[Business Perspective]]
- [[People Perspective]]
- [[Governance Perspective]]
- [[Platform Perspective]]
- [[Security Perspective]]
- [[Operations Perspective]]
- [[Agile Organization]]

---

## Review Questions

1. Define cloud computing in your own words. What are the five main types of IT resources delivered via cloud computing?
    
2. What is the fundamental difference between thinking of infrastructure as "hardware" versus "software"? Explain using the traditional vs. cloud computing models.
    
3. List three problems with the traditional computing model's hardware procurement cycle. How does cloud computing solve each problem?
    
4. Compare and contrast the three cloud service models (IaaS, PaaS, and SaaS). For each, describe what you manage vs. what the provider manages.
    
5. Give a real-world example of a SaaS application you use regularly. Why is it considered SaaS rather than IaaS or PaaS?
    
6. Explain the three cloud deployment models (Cloud, Hybrid, On-Premises). When would an organization choose each one?
    
7. What is meant by "pay-as-you-go pricing"? How does this represent trading capital expense for variable expense?
    
8. Describe the advantage "Stop guessing capacity." What are the two problems that occur when you guess capacity incorrectly in traditional computing?
    
9. Explain how cloud computing provides "massive economies of scale." Why can AWS offer lower prices than what you could achieve on your own?
    
10. What does "Go global in minutes" mean? How does this advantage benefit customers and what AWS feature enables it?
    
11. List and explain the six advantages of cloud computing. Which advantage do you think is most important for a startup company? For an enterprise? Justify your answers.
    
12. What is the difference between a "web service" and "AWS"? How do web services use APIs?
    
13. Describe a simple AWS solution architecture that includes services from at least three different categories. Explain how these services work together.
    
14. AWS offers 10 different compute services (EC2, Lambda, ECS, etc.). Why would AWS offer so many options instead of just one compute service?
    
15. What are the three ways to interact with AWS? Which method would be best for: (a) a beginner exploring AWS, (b) automating repetitive tasks, (c) building an application that programmatically creates resources?
    
16. What is the AWS Cloud Adoption Framework (AWS CAF)? Why was it created?
    
17. What are the three elements that must be in alignment for successful cloud adoption? Why is technology alone not sufficient?
    
18. Explain the difference between the six perspectives in AWS CAF. Which three focus on business capabilities and which three focus on technical capabilities?
    
19. You are the CIO of a company planning to migrate to AWS. Which AWS CAF perspective is most relevant to your role? What would you focus on using that perspective?
    
20. Describe the role of stakeholders in the People Perspective. What kinds of gaps might they identify and how would they address them?
    
21. A company has sensitive customer data that cannot leave their physical data center due to regulations, but they want to use cloud for their web application and analytics. Which deployment model should they use and why?
    
22. Calculate the cost difference: You run a traditional data center that costs $100,000 upfront and $2,000/month in maintenance. You use only 40% of its capacity on average. Compare this to a cloud solution that costs $0 upfront and $1,200/month based on actual usage. What's the total cost for each over 3 years?
    
23. Your company website experiences traffic spikes during holiday sales—10x normal traffic for 2 weeks per year. Explain how the "elastic scaling" advantage of cloud computing helps with this scenario vs. traditional infrastructure.
    
24. Match each AWS service analog to its traditional IT component:
    
    - Amazon EC2 → ?
    - IAM → ?
    - Amazon S3 → ?
    - Elastic Load Balancing → ?
25. A startup asks for your advice: "Should we build our own data center or use AWS?" Using the six advantages of cloud computing, construct an argument for why they should use AWS.
    

---

## Discussion Topics

1. **Cost Analysis**: Is cloud computing always cheaper than traditional infrastructure? Under what circumstances might on-premises infrastructure be more cost-effective?
    
2. **Control vs. Convenience**: As you move from IaaS → PaaS → SaaS, you gain convenience but lose control. What are the trade-offs? When is control more important than convenience?
    
3. **Career Impact**: How does the shift from infrastructure-as-hardware to infrastructure-as-software change the skills needed by IT professionals? What should students focus on learning?
    
4. **Security**: Some organizations are hesitant to move to the cloud due to security concerns. Are these concerns valid? Is data more or less secure in the cloud vs. on-premises?
    
5. **Vendor Lock-in**: Once you build your application on AWS, it can be difficult to move to another provider. Is this a significant risk? How can organizations mitigate it?
    

---

## Practical Scenarios

1. **Scenario**: You're launching an e-commerce website and expect 100 customers/day initially, but could grow to 10,000 customers/day within a year. Design a solution using cloud advantages. Which advantages are most relevant?
    
2. **Scenario**: Your organization has a legacy COBOL application running on mainframes, a modern web application you want to migrate to cloud, and highly sensitive data that legally cannot leave your country. Design a deployment strategy using the three deployment models.
    
3. **Scenario**: You're the IT director planning AWS adoption. Using the AWS CAF, identify which perspectives you need to address first. What gaps might you find in your organization and how would you prioritize addressing them?
    

---

## Practical Tags for Obsidian

#CloudComputing #AWS #AWSArchitecture #CloudAdoption #IaaS #PaaS #SaaS #CloudDeployment #AWSServices #CloudEconomics #AWSCAF #CloudStrategy #ITInfrastructure #DigitalTransformation #CloudMigration #EnterpriseIT #Scalability #CostOptimization #CloudSecurity #AWSBestPractices