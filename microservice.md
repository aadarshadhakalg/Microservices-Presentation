---
title: Microservice Architecture
sub_title: Service-Oriented Architecture done Right
author: Aadarsha Dhakal, Avaya Bajracharya, Aditya Jha
theme:
  override:
    code:
      theme_name: ansi
      padding:
        horizontal: 2
        vertical: 1
---

*src:// learn.microsoft.com*


Microservices derive from SOA, but SOA is different from microservices architecture. Features like large central brokers, central orchestrators at the organization level, and the Enterprise Service Bus (ESB) are typical in SOA. But in most cases, these are anti-patterns in the microservice community. In fact, some people argue that "The microservice architecture is SOA done right."

<!-- pause -->

**"The microservice architecture is SOA done right"**
===
<!-- end_slide -->

# But Why?

## What is SOA?
<!-- pause -->
SOA means that you structure your application by decomposing it into multiple services (most commonly as HTTP services) that can be classified as different types like subsystems or tiers.
<!-- pause -->
## What is Microservice?
<!-- pause -->
A microservices architecture is an approach to building a server application as a set of small services.

<!-- pause -->
Microservices are SOA but not all the SOA are Microservices.
===
<!-- end_slide -->
# More on Service-Oriented Architecture


- **Communication Protocols:** Simple Object Access Protocol (SOAP), RESTful HTTP, Apache Thrift, Apache ActiveMQ, Rabbit MQ, Java Message Service(JMS)
- **Interoperability**
- **Loose Coupling**
- **Granularity**
- **Resources are shared in SOA**: Limited Scalibility, Increasing Interdependencies (Shared resources such as centralized database can slow down the system)
- **Enterprise Service Bus(ESB):** Single Point of Failure

&emsp; "An enterprise service bus (ESB) is software that you can use when communicating with a system that has multiple services. It establishes communication between services and service consumers no matter what the technology."

<!-- end_slide -->



# More on Microservice Architecture

- Very small and completely independent software components, called microservice
- Each microservice specialize and focus on one task only
- Consumer communicates through lightweight APIs, thus removing the need for a centralized ESB.
- Favor data duplication as opposed to data sharing

<!-- end_slide -->


# SOA vs Microservice Architecture

<!-- column_layout: [1, 1] -->

<!-- column: 0 -->

## SOA
- Different services with shared resources
- ESB uses multiple messaging protocols like SOAP, AMQP, and MSMQ.
- Shared data storage
- A full rebuild is required for small changes.
- Reusable services through shared common resources. 
- Slows down as more services are added on. 
- Consistent data governance across all services.

<!-- column: 1 -->

## Microservices
- Independent and purpose-specific smaller services.
- APIs, Java Message Service, Pub/Sub
- Independent data storage.
- Easy to deploy. Each microservice can be containerized.
- Every service has its own independent resources. You can reuse microservices through their APIs.
- Consistent speed as traffic grows.
- Different data governance policies for each storage.

<!-- end_slide -->
# Simple Service-Oriented Architecture
```
┌─────────────┐        ┌───────────┐        ┌────────────┐
│ Desktop App │        │  Web App  │        │ Mobile App │
└─────────────┘        └───────────┘        └────────────┘
         │                   │                    │
         │                   │                    │
┌───────────────────────────────────────────────────────────┐ 
│                  Enterprise Service Bus                   │
└───────────────────────────────────────────────────────────┘
         │                                    │
         │                                    │
┌────────────────┐                 ┌──────────────────────┐        
│ Search Patient │                 │  Prescribe Medicine  │
└────────────────┘                 └──────────────────────┘
         │                                        │
         │                                        │
┌───────────────────────────────────────────────────────────┐ 
│                 Multiple Databases                        │
└───────────────────────────────────────────────────────────┘

```
<!-- end_slide -->
# Simple Microservice Architecure

```
┌─────────────┐   ┌───────────┐     ┌────────────┐
│ Desktop App │   │  Web App  │     │ Mobile App │
└─────────────┘   └───────────┘     └────────────┘
         │          ╱      ╲              │
         │         ╱        ╲             │
         │        ╱          ╲            │
         │       ╱            ╲           │
┌────────────────┐            ┌──────────────────────┐        
│ Search Patient │ <────────> │  Prescribe Medicine  │
└────────────────┘            └──────────────────────┘
         │                                │
         │                                │
┌───────────────────┐        ┌─────────────────────────┐ 
│  Patient Database │        │  Prescription Database  │
└───────────────────┘        └─────────────────────────┘
```


<!-- end_slide -->
# What AWS Cloud Offers for Microservice Architecture?

AWS is a great place to build modern applications with modular architectural patterns, serverless operational models, and agile development processes. 

- Build, isolate, and run secure microservices in Managed Containers [](https://aws.amazon.com/containers/) to simplify operations and reduce management overhead.
- Use AWS Lambda [](https://aws.amazon.com/lambda/) to run  microservices without provisioning and managing servers.
- Choose from 15 relational and non-relational purpose-built AWS databases [](https://aws.amazon.com/products/databases/) to support microservices architecture.
- Easily monitor and control microservices running on AWS with AWS App Mesh [](https://aws.amazon.com/app-mesh/).
- Monitor and troubleshoot complex microservice interactions with AWS X-Ray [](https://aws.amazon.com/xray/).

<!-- end_slide -->

# What Azure Offers for Microservice Architecture?

Azure mirrors AWS for building modern microservices:

- Containers: AKS [](https://azure.microsoft.com/en-us/products/kubernetes-service) for orchestration, ACI [](https://azure.microsoft.com/en-us/products/container-instances) and Container Apps [](https://azure.microsoft.com/en-us/products/container-apps/) for containerization.
- Serverless: Azure Functions [](https://azure.microsoft.com/en-us/products/functions) for event-driven code, Logic Apps for visual workflow automation.
- Databases: Cosmos DB for [](https://azure.microsoft.com/en-us/products/cosmos-db) for both NoSQL and SQL highly available and scalable database,and open-source options like PostgreSQL and MySQL.
- Monitoring and Troubleshooting: Azure Monitor [](https://azure.microsoft.com/en-us/products/monitor) for monitoring, centralized logs and diagnostics, Log Analytics for detailed log analysis.

<!-- end_slide -->

# Are you bored?

<!-- pause -->
```
I've got a joke about microservices
But,
it's kind of complex and frankly no one understands it.
```

<!-- pause -->

जोक थियो यो।  हाँस्ने बेला भयो। 
===

<!-- end_slide -->

# Let's deploy a microservice architecture in Azure

You can find the project here: [](https://github.com/aadarshadhakalg/nodejs-microservices-template)
```bash +exec
eog --fullscreen architecture.png
```

## Overview of the Project

```
.azure/           # Azure infrastructure templates and scripts
.devcontainer/    # Dev container configuration
packages/         # The different services of our app
|- gateway-api/   # The API gateway, created with generator-express
|- settings-api/  # The settings API, created with Fastify CLI
|- dice-api/      # The dice API, created with NestJS CLI
+- website/       # The website, created with Vite CLI
api.http          # HTTP requests to test our APIs
package.json      # NPM workspace configuration
```

<!-- end_slide -->

# Setup Azure

Prerequisites:
- Azure and Github Account
- Azure CLI and Github CLI installed on your system

## Login to Azure using Azure CLI
```bash
az login
az account list
az account set --subscription ${SUBSCRIPTION_ID}
```

## Login to Github using Github CLI
```bash
gh auth login
```

<!-- end_slide -->

# Azure Service Principle and Github Secrets Setup

<!-- column_layout: [1, 1] -->

<!-- column: 0 -->

- Fetch Current Active Subscription ID
- Create a service principle
    - Name: sp-${PROJECT_NAME} 
    - Scope: Current Subscription
    - Role: Contributor
- Retrive project's github url
- Add Service Principle's ID in Github Secrets

<!-- column: 1 -->
```bash +exec
cd nodejs-microservices-template
.azure/setup.sh -s
```

<!-- end_slide -->

# Infrastructure as Code

**Bicep:** Domain Specific Language (DSL) for deploying Azure resources declaratively. 

👀: *$PROJECT_HOME/.azure/infra*

You write code to describe the resources you need, and this code is committed to your project repository so you can use it to create, update, and delete your infrastructure as part of your CI/CD pipeline or locally.

## Let's create required resources in azure
1. Create a Resource Group: `az group create`
2. Create or update resources using the Bicep Templates: `az deployment group create`
3. Reformat the JSON deployment output from the previous command into the file .$environment.env. You should see the file .azure/.prod.env that was created earlier.
4. Run az commands specific to the resources created, to retrieve secrets like the connection string for database or the registry credentials, and store them in the .env file.

<!-- end_slide -->

# Creating Resources

```bash +exec
cd nodejs-microservices-template
.azure/infra.sh update
```

<!-- end_slide -->

# Listing Resources

```bash +exec
az resource list --query "[?resourceGroup=='rg-node-microservices-prod'].{name:name,location:location,resource:resourceGroup}" --output table
```

<!-- end_slide -->

# Deploying using CI/CD
```bash +exec
bat nodejs-microservices-template/.github/workflows/deploy.yml
```

<!-- end_slide -->


# Testing the application

```bash +exec
cd nodejs-microservices-template
source .azure/.prod.env 
echo "https://$STATIC_WEB_APP_HOSTNAMES"
```

<!-- end_slide -->

Any Questions?
===

<!-- end_slide -->

# Thank You!

Get Slides: [](https://github.com/aadarshadhakalg/Microservices-Presentation)
Practice Workshop: [](https://moaw.dev/workshop/gh:azure-samples/nodejs-microservices/main/docs/)

## Additional Resources
- [](https://learn.microsoft.com/en-us/dotnet/architecture/microservices/architect-microservice-container-applications/microservices-architecture)
- [](https://aws.amazon.com/what-is/service-oriented-architecture/)
- [](https://azure.microsoft.com/blog/microservices-an-application-revolution-powered-by-the-cloud/)
- [](https://docs.github.com/en/actions)
- [](https://learn.microsoft.com/en-us/cli/azure/)

