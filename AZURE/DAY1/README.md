# Day 1 - Azure Learning Plan

## Cloud Fundamentals

### Introduction to Cloud Computing

- Definition and benefits of cloud computing
  A service that is available over the internet, allowing users to access computing resources on-demand.

### Types of Cloud Deployments

- Private Cloud: Cloud infrastructure operated solely for a single organization.
  - Maintaining control over data and security.
  - Customization to meet specific business needs.


- Public Cloud: Cloud services offered over the public internet and available to anyone.
  - Cost-effective and scalable.
  - Managed by third-party providers.
  - Scale without changing underlying infrastructure.
  - can access resources from anywhere with an internet connection.
  - cost saving because cloud services are shared between multiple users.


- Hybrid Cloud: A combination of private and public clouds, allowing data and applications to be shared between them.
  - Flexibility to choose optimal deployment for each workload.
  - Enhanced security for sensitive data.
  - Cost efficiency by leveraging public cloud resources when needed.
  - Cons complexity in management and integration.

### Compare capex and opex in different cloud models.
- Capital Expenditure (CapEx): Upfront costs for physical hardware and infrastructure in traditional IT setups.
- Operational Expenditure (OpEx): Ongoing costs for cloud services, typically billed based on usage, allowing for more predictable budgeting and reduced upfront investment.

**Consumption-based** pricing model: Pay only for the resources you use, allowing for cost efficiency and scalability, better cost prediction, and reduced upfront investment.

### Cloud Service Models
![Cloud Models](image.png)
- Types of cloud services: *IaaS*, *PaaS*, *SaaS*
  - IaaS (Infrastructure as a Service): Provides virtualized computing resources over the internet.
  Most flexible
  - PaaS (Platform as a Service): Provides a platform allowing customers to develop, run, and manage applications.
  Focus on application development without worrying about underlying infrastructure.
  - SaaS (Software as a Service): Delivers software applications over the internet, on a subscription basis.
  Pay as you go model, ready to use applications.

![Shared Responsibility Model](image-1.svg)

### Cloud Benifits
- High Availability
- Elasticity
- Scalability
    * vertical scaling - adding more power (CPU, RAM) to an existing machine.
    * horizontal scaling - adding more machines to handle increased load.
- Reliability
- Predicibility
- Security
- Governance - policies and rules to manage cloud resources effectively, production standards, compliance, and cost management.
- Managability

### Related Concepts

- **Virtualization:** Creating virtual versions of resources like servers or storage to maximize hardware use.  
  *Example: Running several virtual servers on one physical machine.*

- **Hypervisor:** Software that enables virtualization by running and managing virtual machines.  
  *Example: VMware ESXi, Microsoft Hyper-V.*

- **API (Application Programming Interface):** A set of rules for software to communicate and interact.  
  *Example: Using REST APIs to automate cloud resource management.*

- **Regions:** Physical locations around the world where cloud providers host data centers.  
  *Example: Azure "East US" or "West Europe".*

- **Availability Zones:** Separate, isolated locations within a region for higher redundancy and reliability.  
  *Example: Deploying resources across zones to ensure uptime if one fails.*

- **Scalability:** The ability to grow or shrink resources to meet demand.  
  *Example: Adding servers during peak usage.*

- **Elasticity:** Automatically adjusting resources based on real-time demand.  
  *Example: Auto-scaling web servers up or down as traffic changes.*

- **High Availability:** Designing systems to minimize downtime and ensure continuous service.  
  *Example: Using redundant servers and load balancers.*

- **Disaster Recovery:** Plans and tools to restore data and services after failures or disasters.  
  *Example: Backing up data to another region for quick recovery.*

- **Agility:** Rapidly adapting to changes and deploying new solutions.  
  *Example: Rolling out new app features in hours instead of weeks.*
