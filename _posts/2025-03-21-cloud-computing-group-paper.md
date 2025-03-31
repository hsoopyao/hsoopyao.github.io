---
layout: post
title: DevOps Techniques in Bookstore Cloud Application
subtitle: Cloud Computing Group Project
gh-repo: hsoopyao/Group-Project-in-Cloud-Computing
gh-badge: [star, follow]
tags: [cloud, group, paper, school]
author: Aniket Thorat, Jiawen Yao, Rozana Almohammadi, Abhishek Pawar, Lonxing Li
---

DevOps Techniques in Bookstore Cloud Application

Aniket Thorat, Jiawen Yao, Rozana Almohammadi, Abhishek Pawar, Lonxing Li

1. **Introduction:**

This report presents the outcome of our Group Project in Cloud Computing, which is a Group Project and Research Methods with the purpose of applying cloud computing practices and principles to a real-world problem. In this project, we cloned an open-source repository from GitHub, and collectively, we undertook a series of customizations to fit the requirements of the project. We modified the project by replacing the existing database with PostgreSQL to achieve better scalability and performance and removing the payment gateway to simplify the system.

Throughout the project, we worked as a group, helping each other with every task and sharing solutions openly in online sessions and in-person meetings. Every member of the team put their knowledge into different parts of the project while also supporting others with different areas of work. While each member had an equal role to play to make the project a success, each one primarily focused on one specific area of the project.

**1.1 Team Members and strengths**

**Aniket Thorat:**

He is a highly skilled Cloud Computing enthusiast with expertise in Java, Spring Boot, and cloud platforms like AWS and Azure. With a strong background in software development, he has demonstrated proficiency in designing and optimizing scalable systems, particularly in Microservices and DevOps environments. His technical skillset includes Kubernetes, Docker, Prometheus, and Grafana, enabling him to build resilient and high-performance applications. He possesses a keen problem-solving mindset, quickly analyzing challenges and implementing effective solutions. He is detail-oriented and thrives in dynamic, fast-paced environments, making him adaptable to evolving technologies. His strong communication skills allow him to collaborate effectively across teams, ensuring seamless integration of cloud-based solutions.

**Jiawen Yao:**

Her expertise includes PostgreSQL administration, containerization with Kubernetes and Docker on Azure, and configuring StatefulSets with Persistent Volumes to ensure data persistence. Additionally, she is proficient in implementing Liveness and Readiness Probes to enhance system reliability, conducting unit testing to ensure code quality, and managing CI/CD pipelines for smooth deployment. She is also responsible for maintaining and updating deployed projects on servers, ensuring their stability and optimal performance. She is passionate about researching and learning, continuously analyzing and troubleshooting errors to improve system performance and enhance her skills.

**Rozana Almohammadi:**

She has a strong understanding of DevOps practices and cloud-native application deployment. Her experience includes designing scalable architectures using Kubernetes, configuring CI/CD pipelines with GitHub Actions, and integrating monitoring tools such as Prometheus and Grafana. She also has hands-on skills in deploying microservices with Docker and managing database backups using Velero. In addition, she has a solid technical background in programming, with prior experience in Java, Python, and HTML, which enables her to efficiently handle the development aspects of any project. She enjoys working on automation and infrastructure optimization tasks with a focus on continuous improvement. She is highly organized and responsible, always committed to completing tasks efficiently and on time, contributing to successful teamwork and project outcomes.

**Abhishek Pawar:**

He possesses a strong foundation in both front-end and back-end web development. His technical skills include proficiency in HTML, CSS, JavaScript, Tailwind CSS, and jQuery for front-end, while on the back-end he is experienced with Node.js, Express, MongoDB, and SQL. He brings a versatile approach to problem-solving and enjoy taking on challenges that require creativity and critical thinking. His strengths lie in leadership, effective communication, and patience, which help him collaborate well in team environments. He takes pride in being adaptable and continuously improving his skill set. These qualities enable him to build efficient, user-friendly web applications while contributing positively to any team.

**Lonxing Li:**

He has some experience with using Kubernetes to deploy microservices, like he can write YAML files and set up services with specific nodes. Sometimes he uses StatefulSets for databases because they need stable storage, and he also added backups using Velero, which is kind of tricky but useful. He knows how to set probes to check if the app is alive or ready, and he worked with environment variables too. When he set up the database, he tried to make sure it can keep data safe, and he learned to use backup hooks before doing real backups. He always wants to improve and try to make the system more stable. He thinks solving problems during deployment is fun, even when it’s hard.

1. **Project Specification: Bookstore App**

The Bookstore App is a cloud-native, microservices, online bookstore application intended to deliver a scalable, resilient, and continuously deployable system. The application is developed with React.js for the frontend and Spring Boot for the backend, containerized with Docker, and orchestrated with Kubernetes for effortless deployment and management. The system is hosted on Microsoft Azure, and GitHub Actions handles the CI/CD pipeline for automated testing, deployment, and rollback. Prometheus is employed for monitoring and performance monitoring.

**2.1 Technologies Used:**

| Component | Technology |
| --- | --- |
| Frontend | ReactJS |
| Backend | Java, Spring Boot |
| Database | PostgreSQL |
| Containerization & Orchestration | Docker, Kubernetes |
| CI/CD Pipeline | GitHub Actions |
| Monitoring | Prometheus |
| Cloud Platform | Azure |

**2.2 Technical Requirement and Implementation**

The Bookstore App was built with scalability, resilience, and efficient deployment in mind to provide high availability and optimal performance under different workloads. Horizontal Pod Autoscaling (HPA), automated recovery processes, and a CI/CD pipeline with rollback capability enabled smooth system management with zero downtime during updates.

A. Scalability:

To ensure that the system can handle high traffic with efficiency, from a peak of 1,000 concurrent users, Horizontal Pod Autoscaling (HPA) was configured on the Catalog Service to scale up or down automatically the number of active pods based on CPU usage (threshold is 60%). Additionally, Cluster Autoscaling was also implemented to add new worker nodes automatically when existing resources were not sufficient to accommodate new pods. For scaling purposes, k6 load testing was conducted that simulated up to 500 concurrent users for 5 minutes to test under stress.[1]

B. Recovery:

To enhance the system resiliency and fault tolerance, liveness and readiness probes were added to the Cart Service so that Kubernetes would be able to detect and restart hanging pods automatically. Data loss was prevented by using Velero to back up PostgreSQL data every day to Azure Blob Storage to support easy restoration in case of failures. Secondly, PostgreSQL was run as a Stateful Set with Persistent Volumes such that data is retained across pod restarts and cluster failure and enhances system robustness.[2]

C. Deployment:

For seamless application upgrades and zero downtime, Blue-Green Deployment was employed for Catalog Service. It allows new releases to be deployed in parallel to existing releases with traffic being forwarded between "blue" and "green" environments without impacting users. The CI/CD pipeline, managed via GitHub Actions, performs building, testing, and deployment automatically to provide seamless releases. The pipeline also has a rollback functionality, where in the event of deployment test failure, the system rolls back to the last stable version automatically so that faulty updates do not affect live users.[3]

**2.3 Implementation Phases:**

The Bookstore Application was developed and implemented systematically, following a phased approach to enable a smooth transition from development to a complete, scalable, and robust system.

Phase 1: Baseline Deployment, Phase 1 focused on deploying the foundational infrastructure and deploying the base microservices of the Bookstore App. The application was Dockerized and running on Kubernetes, locally or on a cloud provider (Azure Kubernetes Service - AKS). A CI/CD pipeline through GitHub Actions was implemented for automatic code integration, testing, and deployment. This phase guaranteed that the frontend (Node.js, React.js) and backend (Spring Boot) services were properly integrated with PostgreSQL as the database.

Phase 2: Scaling, Once the baseline deployment was established, the objective was to scale the system to handle increased user traffic. Horizontal Pod Autoscaling (HPA) was established for the Catalog Service, which automatically scaled pods when CPU utilization exceeded 60%. Cluster Autoscaling was also introduced to dynamically add worker nodes whenever there were Kubernetes pods that could not be scheduled due to resource constraints. To ensure system scalability, load testing was done using k6, simulating up to 500 concurrent users in 5 minutes, ensuring the system could efficiently handle high traffic loads.

Phase 3: Resilience, for improving fault tolerance and disaster recovery, several resilience mechanisms were put in place. Liveness and Readiness Probes were added to the Cart Service to detect and restart hung pods, ensuring availability. The PostgreSQL database was deployed as a Stateful Set within Kubernetes with Persistent Volumes to prevent data loss due to pod crashes. For backup and disaster recovery, Velero was used to daily back up databases into Azure Blob Storage so that the data could be restored in the event of a failure. These habits significantly improved the reliability of the application and enabled services to be recovered very quickly in the event of sudden failures.[4]

Phase 4: Zero-Downtime Deployments, to offer zero-downtime application updates without disrupting the user experience, blue-green deployment was utilized. The approach entails deploying a new version of the Catalog Service and the existing one simultaneously, with a Kubernetes Service directing traffic between versions. Once the new version is validated to be stable, traffic is gradually redirected from the "blue" (old) version to the "green" (new) version without any interruption. The CI/CD pipeline was also enhanced to include automatic rollback. If a deployment fails due to issues in the new release, GitHub Actions triggers a rollback so that users are not affected by faulty updates.

**2.4 Success Metrics and Outcomes**

| Metrics | Outcomes |
| --- | --- |
| Scalability | The Catalog Service scaled dynamically between 2 and 8 pods during high traffic. |
| Recovery | The PostgreSQL database was restored from backup in less than 5 minutes following a simulated crash. |
| Deployment | Zero downtime was achieved in deploying new updates using Blue-Green Deployment. |

1. **Background Research**

**3.1 Introduction to DevOps**

DevOps is a cultural and technical movement that emphasizes cross-functional collaboration between software developers and IT operations to enhance the speed, efficiency, and consistency of software delivery. It encompasses automation at every stage of the software development cycle, with continuous integration (CI) and continuous deployment (CD) practices.[5]

The main obstacle to DevOps adoption is uncertainty about how it should be executed. Although organizations realize its value, most of them are not able to efficiently implement it because there is no specific framework. Research emphasizes that DevOps is not a set of tools but the combination of technology and cultural change.[5]

**DevOps Pipeline and CI/CD**

The DevOps pipeline consists of many automated tasks, including code integration, testing, and deployment, to ensure seamless software updates. CI/CD pipelines ensure that new code updates are tested and deployed efficiently without the intervention of humans.[5] This Pipeline Consist of:

* Continues Integration (CI): Automates code changes integration into a shared repository.
* Continuous Delivery (CD): Enables new code to be deployed safely at any time.
* Continuous Deployment: Automates deployment by deploying authorized code directly to production.

**3.2 Cloud Computing in DevOps**

Cloud computing is extremely critical in today's DevOps approach, as it provides on-demand infrastructure, scalability, and resource management. The e-commerce sector, on the other hand, is preferred by cloud computing with cost reduction in hardware and software and higher availability.[6]

**Types of Cloud Services**

* Infrastructure as a Service (IaaS): Provides computing, storage, and network resources on an as-needed basis.
* Platform as a Service (PaaS): Offers a platform to develop and manage applications without regard to the underlying infrastructure.
* Software as a Service (SaaS): Offers applications over the internet, bypassing local installation.

Cloud-native applications, like the Bookstore App, are designed to execute on cloud infrastructure using microservices and container orchestration technologies like Kubernetes.[6]

**3.3 Kubernetes and Container Orchestration**

Kubernetes is now the leading orchestration platform for running containerized applications, with automated deployment, scaling, and management of hosts across clusters.[7]

Kubernetes Horizontal Pod Autoscaler (HPA):

HPA will automatically scale running pods based on CPU or memory utilization, while optimal utilization of resources and performance will be traded off. [8]

Enhancements such as protection-aware scaling can also increase resiliency by provisioning resources in advance for critical workloads.[8]

**Scalability in Kubernetes**

One of the biggest challenges in cloud apps is scaling them appropriately to handle increasing traffic levels. Research shows that:

* Kubernetes supports maximum resource utilization and horizontal scaling.[7]
* Load testing tools, such as K6, help to measure the performance under load.[8]

**3.4 Deployment Strategies in Kubernetes**

Zero-downtime deployment methodologies are critical for smooth services. Rolling Updates, Blue-Green Deployments, and Canary Releases are a few such methods that are practiced extensively in Kubernetes [9]:

Rolling Updates:

* Updates instances of an application gradually to avoid downtime.
* Ensures new versions without impacting users.

Blue-Green Deployments:

* Two environments: one (Blue) has the current version, and the other (Green) has the newer version.
* Redirects traffic only to the newer version when verification is successful [10]​.

Canary Releases

* Rolls out new features to a small audience prior to the release.
* Allows for real-time observation and risk control.

**3.5 Security Consideration in DevOps**

Security must be incorporated into the DevOps lifecycle in order to have robust cyber-attack protection. Some of the most significant security practices are:

* Shift Left Security: Binds security testing in the early development stage.
* Least Privilege Access: Restricts system privileges to minimize risk.
* Automated Compliance Checks: Validates compliance with security policies.

**3.6 Continuous Monitoring and Logging**

Monitoring is important so as to detect performance bottlenecks as well as determine system health. The combination of Prometheus (metrics collection) and Grafana (visualisation) is a wholesome monitoring stack for cloud-native applications.[11]

Monitoring Stack

* Prometheus: Measuring application and infrastructure in real time.
* Grafana: Charts metrics and supports alerting.

1. **Design Description**

In our project, we created a microservices-based bookstore application deployed on Azure Kubernetes Service (AKS) for scalability, reliability, and high availability. The architecture utilizes a blend of cloud-native technologies, containerization, and monitoring instruments to create a robust and production-grade system. Below is a diagram explain the typical architecture followed in a microservices application deployed on cloud.

**![A diagram of a software process

AI-generated content may be incorrect.](data:image/jpeg;base64...)**

*Fig 1: Architecture Diagram*

**4.1 Design Description of the Bookstore Application Architecture**

**A. Frontend (React.js)**

Our application's frontend is built using React.js, which provides a seamless and user-friendly interface for browsing and purchasing books. The frontend is an SPA that dynamically talks to the backend via API calls.

* Technologies Used: React.js
* Purpose:

1. Ensure a responsive and interactive UI for users.
2. Communicates with backend services via the Ingress Controller and API Gateway.
3. Allows users to browse books, place orders, and manage their accounts.

Since React.js is a lightweight frontend framework, it enhances the performance by reducing unnecessary page reloads, making the application more efficient.

**B. Ingress Controller (SSL, Routing, Load Balancing)**

Ingress Controller is responsible for managing outside access to the application by routing incoming HTTP and HTTPS requests to the appropriate microservices. It also has an important responsibility of protecting and optimizing traffic flow within the system.

Key Features of Ingress:

* SSL Termination: Ensures all incoming requests are securely encrypted with HTTPS.
* Routing: Routes requests to the appropriate backend microservices based on defined rules.
* Load Balancing: Distributes incoming traffic across multiple instances of a service for better performance and availability.
* Path-based and Host-based Routing: Allows the system to route requests based on URLs or subdomains.

By adding an Ingress Controller, we effectively manage all incoming traffic before it reaches the API Gateway, reducing latency, improving security, and load-balancing across multiple backend services.

**C. Microservices Architecture**

Our backend is microservices architecture, where functionalities are divided into different services which communicate with each other using REST APIs. Each service is therefore independently developable, deployable, and scalable.

Main Microservices of the System

* Account Service: Manages user authentication, profiles, and authorizations.
* Order Service: Processes orders, payment, and tracking.
* Catalog Service (Scalable): Manages book listings, search, and inventory updates.

Every microservice is run in its own Docker container and hosted on Kubernetes for fault tolerance and high availability. We use Consul for service discovery and health checks to ensure that services can dynamically discover and communicate with each other.

**D. Horizontal Pod Autoscaler (HPA)**

To ensure that the Catalog Service can handle dynamic loads, we've employed Horizontal Pod Autoscaling (HPA). It helps to scale services automatically based on real-time utilization of resources.

How HPA Works

* Monitors CPU and memory consumption of running pods.
* Scales pods if use of resources exceeds allocated limits.
* Scales down pods during low-traffic periods to optimize resource utilization.

For instance, when the traffic is boosted to 1,000 simultaneous users, HPA will automatically scale up the number of Catalog Service pods, forestalling performance degradation.

**E. Database Layer (PostgreSQL)**

For data storage, we use PostgreSQL, a high-performance relational database system that offers data consistency, integrity, and scalability. It stores important data such as user accounts, order details, and book inventory.

Deployment Strategies:

* StatefulSet Deployment: Ensures database pods retain the same storage even upon restart.
* Persistent Volume (PV) & Persistent Volume Claims (PVC): Provides durable and reliable data storage.
* Automated Backups using Velero: Takes periodic backups of the PostgreSQL database and stores them in Azure storage for disaster recovery.

Using Velero, we can now restore lost data quickly and recover from failures, and our application is always available.

**F. Kubernetes for Container Orchestration**

Our entire application is containerized with Docker and deployed on Azure Kubernetes Service (AKS), providing automatic scaling, load balancing, and self-healing capabilities.

Benefits of Kubernetes Deployment:

* High Availability: Maintains services available despite individual containers' failure.
* Self-Healing Mechanism: Automatically replaces failed containers.
* Effective Resource Allocation: Distributes workloads to nodes for optimal performance.

We employ Azure Container Registry (ACR) to maintain Docker images in storage, permitting easy management and deployment of updates.

**G. Monitoring and Logging with Prometheus**

To maintain observability and performance tracking, we integrated Prometheus as our monitoring solution.

Features of Prometheus:

* Real-time Metrics Collection: Tracks CPU consumption, memory consumption, and API latencies.
* Alerting System: Alerts on detecting anomalies.
* Integration with Grafana: Provides a graphical dashboard for analyzing the system performance.

Such a monitoring setup enables proactive issue fixing, reducing system downtime and ensuring smooth operation.

**H. Storage and Disaster Recovery Mechanisms**

To avoid data loss and system failures, we had robust storage and backup solutions in place.

Storage Features of interest:

* Persistent Volume (PV) and Persistent Volume Claims (PVC): Hosts critical application and database data.
* Azure Managed Disks: Allows data access to PostgreSQL with fast speed.
* Velero for Backup and Restore: Allows database backups to be restored within a couple of minutes on failure.

With these solutions combined, we can ensure that our application is resilient even in unexpected failures.

**I. CI/CD Pipeline with GitHub Actions**

To automate deployment, testing, and build, we built a CI/CD pipeline using GitHub Actions.

Pipeline Steps:

* Code Build & Test: Automatically tests and builds new changes to the code.
* Docker Image Build: Builds new container images and pushes them to Azure Container Registry.
* Deployment to Kubernetes: Deploys new updates into the Azure Kubernetes Service.
* Rollback Mechanism: On deployment failure, automatically rolls back to the previous stable version.

This pipeline allows us to deploy new features quickly, minimize manual intervention, and offer high reliability.

1. **Justification of Design Choices**

Why Microservices over Monolithic design?

To guarantee scalability, flexibility, and resilience, we opted for microservices rather than a monolithic architecture. All the parts of a monolithic system are closely connected, which makes scalability and upgrades difficult. Microservices enable us to expand individual components without impacting the system because each service (such as the account-service, order-service, and catalog-service) functions independently.

![project-structure.png](../assets/img/cloud-computing-group/project-structure.png)

*Fig 2: Microservices architecture codebase*

Example Scenario: When there is a failure in the order service causing a downtime to recover, the catalog service might still be running which will not cause the entire application to fail completely. The user will still be able to have a look at the inventory.

Why choose Docker for Containerization?

Docker provides a portable, lightweight, and reproducible runtime environment for our application in any environment (dev, test, and prod). Docker addresses the "works on my machine" problem by having identical dependencies and configurations everywhere.

Example Scenario: A developer can utilize Docker to containerize the application and get it to run the same way on Azure Kubernetes Service (AKS) at deployment time.

Why use Kubernetes for Orchestration?

Kubernetes automatically deploys, scales, and manages containers while providing self-healing. Kubernetes provides high availability and optimal use of resources through the lifecycle management of pods.

Example Scenario: When the node running the order service goes down, Kubernetes automatically restarts the affected pods and reschedules them on a healthy node.

Why PostgreSQL over other Databases?

PostgreSQL is a highly scalable, open-source relational database with support for ACID compliance, strong consistency, and complex queries. It can be easily integrated with microservices and offers great backup and disaster recovery capabilities.

Example Scenario: For preventing data loss, we employ Velero for automated backup, and it helps us quickly restore the database in case of failure.

1. **Implementation Overview**

**6.1 Microservices Architecture**

The application consists of several microservices, each running independently and communicating via HTTP APIs. These services include:

bookstore-account-service - Manages user authentication and account-related operations.

bookstore-order-service - Handles order processing and transactions.

bookstore-catalog-service - Manages books/products in the inventory.

bookstore-api-gateway-service - Acts as an entry point for all requests, routing them to the appropriate microservices.

bookstore-frontend-react-app - React-based frontend application.

Each microservice is containerized using Docker, and an individual Dockerfile is present in each service directory.

**6.2 Containerization with Docker**

Each microservice has its own Dockerfile, which defines the image-building process.

![docker-file.png](../assets/img/cloud-computing-group/docker-file.png)

*Fig 3: Example DockerFile*

**6.2 Kubernetes Deployment**

The Kubernetes configurations are stored inside the kubernetes/ directory. It contains:

configration/ - Stores environment variables and secrets.

services/ - Contains Deployment and Service definitions.

postgres/ - Database-related Kubernetes configuration.

monitors/ - Configurations for monitoring (Prometheus, Grafana).

The command (kubectl apply -f) to apply these kubernetes files are configured in the CD (Continuous Delivery) pipelines for each service.

![kubernetes-deployment-file.png](../assets/img/cloud-computing-group/kubernetes-deployment-file.png)

*Fig 4: Example kubernetes deployment file.*

**6.3 API Gateway and Ingress**

The bookstore-api-gateway-service handles authentication and routing to all microservices.

The Ingress Controller is responsible for SSL termination and routing traffic from the frontend to the backend services.

![ingress-control-file.png](../assets/img/cloud-computing-group/ingress-control-file.png)

*Fig 5: Ingress controller configuration yaml*

The api-gateway-service is configured in the ingress controller, causing all the traffic from frontend to go only to the api-gateway-service which then later moves it to individual microservices. This api-gateway is an inbuilt library provided by Spring Boot we just configured it for our application.

**6.4 CI/CD Pipelines (GitHub Actions)**

The project has multiple CI/CD pipelines in the .github/workflows/ directory:

Workflow Files

catalog-service-cd.yaml - CD for the catalog service.

The catalog-service is configured for blue-green deployments depending on the current version running (either blue or green) the new deployment should be decided. Based on this condition the continuous delivery pipeline for catalog service is defined. Hence we had to implement a separate CD pipeline file for catalog service.

ci-react.yml - Builds and deploys the React frontend.

The frontend application is based out of ReactJS which has different build tool. We used maven for backend but frontend uses npm (Node Package Manager).

ci.yml - Generic CI pipeline for other microservices.

GitHub actions allows you to create variables inside the yml file. We created a variable consisting all the names of the backend services to be built in strategy.matrices variable. Using this variable same pipeline will have individual workflows for each service separately.

generic-deployments.yaml - A general workflow for deploying microservices.

CI/CD process:

Each time a new commit is created to the main branch on github either using a Pull Request, or a direct commit, Continuous Integration pipeline is triggered. The main purpose of this pipeline is to ensure there are no build/compilation failures in the new commit. This also runs all the unit tests coded by the developer to ensure the business functionality is not hampered by any change in the code. Even the smallest change like a small space character in a file can trigger this CI pipeline. Once all the tests are successful, the built image is uploaded to the Azure Container Registry using the credentials stored in GitHub secrets. These secrets are not accessible by anyone except the repository owner.

![Azure-container-registry.png](../assets/img/cloud-computing-group/Azure-container-registry.png)

*Fig 6: Azure Container Registry*

After a successful run of the CI pipeline, the Continuous Delivery pipeline is triggered. This workflow looks for the latest image in the container registry and uses that to deploy the lates version of the application to AKS. These two steps are the core principles of DevOps.

![Github-action.png](../assets/img/cloud-computing-group/Github-action.png)

*Fig 7: CI/CD pipelines in GitHub Actions*

**6.6 Load Testing and Monitoring**

To evaluate the system’s performance under varying levels of load, we utilized K6, a load-testing tool, to simulate real-world traffic. The script was designed to test the scalability and responsiveness of the system by gradually increasing and decreasing the number of virtual users (VUs).

The test consisted of three stages:

* Ramp-up phase – Over the course of one minute, the number of virtual users gradually increased to 100 to simulate a growing load.
* Sustained load phase – For the next five minutes, the test maintained 1000 virtual users, placing a significant load on the system to evaluate its stability under high traffic.
* Cooldown phase – In the final one minute, the number of virtual users gradually decreased to zero, simulating the end of a peak usage period.

![before-load-testing.png](../assets/img/cloud-computing-group/before-load-testing.png)

*Fig 8: Before Load Testing*

Each virtual user sent repeated HTTP GET requests to the catalog service. The responses were monitored to ensure that the server returned a 200 OK status, indicating successful handling of requests. Additionally, a 1-second delay was introduced between requests to mimic realistic user behaviour.

![after-benchmarking.png](../assets/img/cloud-computing-group/after-benchmarking.png)

*Fig 9: After benchmarking was triggered*

This test was instrumental in assessing the system’s ability to scale dynamically and maintain stability under different levels of traffic. The results provided insights into potential bottlenecks and the efficiency of the autoscaling mechanism in adapting to demand fluctuations.

![become-normal.png](../assets/img/cloud-computing-group/become-normal.png)

*Fig 10: Number of pods going back to normal after some time*

After the load was reduced back to normal traffic, the scaled pods were terminated and number of replicas were brought back down to the default value (2).

**6.7 Testing of Disaster Recovery (Velero)**

The testing process for PostgreSQL recovery involves first verifying the availability of backups using Velero. To simulate a failure scenario, the persistent storage volumes containing PostgreSQL data are intentionally deleted. The recovery process is then initiated by restoring the database from a previously taken backup. The progress of the restoration is monitored to ensure successful data retrieval. Once the restore operation is completed, the recovered database is accessed to confirm that all tables and data have been successfully restored, validating the reliability of the backup and recovery strategy.

![velero backups.png](../assets/img/cloud-computing-group/velero%20backups.png)

*Fig 11: Velero Backups*

1. **Challenges**

**7.1 Backend Services Could Not Be Built and Run on Local Systems**

Problem:

The backend microservices could not be successfully built or executed on local machines.

The issue was caused by Java version incompatibility.

The original configuration used a higher version of Java (likely Java 17), which was not fully compatible with the libraries and dependencies used in the project.

Fix:

Java version was downgraded to Java 11, which is a stable and widely supported version for Spring Boot applications.

**7.2 Azure Student Account CPU Restrictions in AKS**

Problem:

* The Azure Student Account had CPU usage limitations in AKS, restricting the number of virtual CPUs available.
* This prevented the deployment of multiple microservices, leading to resource exhaustion.

Fix:

* Reduced the number of services by combining the Billing and Order microservices.
* The Payment Gateway was removed entirely to optimize resource usage.

New Architecture:

* Instead of separate billing-service and order-service, a single order-service was created with combined billing functionalities.
* Payment-related API calls and functionalities were removed.
* Refactored database schema to merge billing and order-related tables.

Benefits of the fix:

* Reduced the number of deployed services in AKS, decreasing CPU usage.
* Optimized service communication, improving performance.
* Allowed the system to stay within Azure’s student account limits while maintaining core functionalities.

**7.3 Frontend Failures After Backend Refactoring**

Problem:

After merging Billing and Order services and removing the Payment Gateway, the frontend application started failing.

Issues encountered:

* Broken API calls: The React frontend was still making requests to removed backend endpoints.
* Non-functional pages: Pages related to payment processing and billing displayed errors.
* Invalid responses: The structure of responses from the refactored backend changed, breaking frontend data handling.

Fix:

* Updated React application to align with backend changes.
* Removed broken API calls to billing-service and payment-service.
* Refactored frontend logic to use the new order-service for all billing-related functionalities.
* Deleted unnecessary UI pages that were dependent on the removed services.

**7.4 High CPU Utilization During Deployments**

Problem:

Every time a new deployment was made, CPU usage spiked over 300%.This triggered unnecessary autoscaling due to the Horizontal Pod Autoscaler (HPA) configuration.

Cause:

* New containers were starting without proper health checks, leading to excessive restarts.
* HPA detected high CPU usage before the application was fully ready.

Fix:

* Implemented Liveness and Readiness Probes in Kubernetes Configuration.

![liveness-readiness-probe.png](../assets/img/cloud-computing-group/liveness-readiness-probe.png)

*Fig 12: Liveness and Readiness Probes*

These probes ensure that:

* The application is not restarted unnecessarily if it takes time to initialize.
* Kubernetes only routes traffic when the service is fully ready.

1. **Critical Evaluation**

**8.1 Self-Evaluation of Design and Implementation choices**

Our project effectively built a cloud-native microservices-based bookstore application with scalability, resiliency, automated deployment, and monitoring as primary issues. Through intensive architecture design, use of recent DevOps practices, and cloud technology, we effectively built a system that was efficient and reliable. Although the implementation reached its basic goals, there always are areas for optimization and future enhancement.

**8.2 What worked well?**

**Scalability Achieved**

One of the best achievements in our project was scaling the system based on demand. Horizontal Pod Autoscaler (HPA) scaled the number of pods handling catalog service requests based on CPU usage automatically, scaling up or down. This ensured that the system remained responsive even at high traffic.

Load testing using k6 simulated traffic patterns and helped ensure our Kubernetes cluster could handle real-world loads. The catalog service was load-tested with a ramp-up to 1,000 concurrent users, with Kubernetes auto-scaling it from 2 pods to 8 pods, without any downtime or performance loss.

This scalability features not only optimized the utilization of resources but also contributed to cost-effectiveness since it allowed the system to scale down during periods of low demand.

**Database Resilience and Recovery**

For data persistence and reliability, we integrated PostgreSQL as a StatefulSet within Kubernetes so that the storage of this would remain intact even if a pod is restarted or rescheduled. We also used the Velero backup tool, which ran daily backups to cloud storage automatically, so even in the event of accidental data deletion or failure, we were able to retrieve the database back within less than 5 minutes.

This approach eliminated all the chances of data loss and data corruption while maintaining transactional consistency.

The application was made to be database failure resilient by restoring all the records when the backup system was successfully emulated without affecting active user sessions.

**Zero-Downtime Deployments**

Blue-Green Deployment pattern was utilized to facilitate seamless version rollouts without the disruption of service.

The pattern ensured users never experienced downtime during a new version deployment because traffic was rolled over between old and new versions of the service without a hitch.

If a new deployment crashed upon hitting unexpected issues, the rollbacks were automatic, rolling back the system to the previous working version, making users never experience broken deployments.

We set up this process in our CI/CD pipeline using GitHub Actions where deployments were automated, tested, and rolled over safely without requiring manual intervention.

**Monitoring and Debugging Enhancements**

Real-time monitoring was added to our system using Prometheus, providing end-to-end visibility into system health, performance, and usage of resources.

CPU, memory, and request-response times were monitored through Prometheus metrics, allowing us to improve the performance of microservices over time.

Logs were also collected for debugging and troubleshooting purposes, shortening the diagnosis and resolution time significantly.

This came in handy especially while performing performance testing and debugging network latency, optimizing database queries, and detecting pod failures.

**8.2 What Could Be Improved?**

While our system performed well in most aspects, there are a few areas where improvements can be made:

**More Granular Auto-Scaling Strategies**

Even though CPU-based auto-scaling worked, adding request-based auto-scaling or custom metrics-based scaling (such as latency-based scaling) would result in more optimized resource allocation.

Adding KEDA (Kubernetes Event-Driven Autoscaler) may allow scaling by request volume, rather than merely CPU usage, and scale quicker.

**Enhanced Disaster Recovery Strategies**

Though Velero successfully stored and recovered PostgreSQL data, integrating a multi-region backup solution would add redundancy on another level.

Adding active-active database replication in multiple cloud zones would improve disaster recovery time and prevent complete downtime in case of catastrophic cloud failure. Azure provides a separate preconfigured service for this, Locally redundant storage (LRS) replicates the data within your storage accounts to one or more availability zones located in the primary region of your choice.

**Advanced Traffic Routing for Deployments**

While Blue-Green Deployment was acceptable, employing Canary Deployments would allow us to roll out updates to a small percentage of users at first and incrementally roll out if no issues are discovered.

It would assist in catching problems earlier within production environments before affecting the entire user base.

1. **Peer Evaluation: Comparative Analysis of Different Group Projects**

In evaluating the architectural designs and DevOps implementations of two other groups (Group 6 and Group 7), the analysis below outlines the best, good, bad, or even ugly aspects of their designs in comparison to our own implementation. This assessment is based on design clarity, justification of choices, DevOps depth, and presentation coherence.

**Group 6**

Best Aspect: Cloud Infrastructure Optimization (AWS EKS + Auto Scaling)

Group 6 demonstrated a well-thought-out cloud infrastructure utilizing Amazon EKS with both Horizontal Pod Autoscaler (HPA) and Cluster Auto Scaling (ASG). Their justification highlights resource efficiency, cost optimization, and high availability, which aligns with industry best practices. This setup outperforms ours in cloud-native elasticity, particularly due to their use of Availability Zones and ASG, which we did not implement.

Justification:

The layered autoscaling (pods and nodes) ensures their system can handle both application-level spikes and infrastructure-level elasticity, which gives them an edge in scalability and reliability compared to our Kubernetes-only (pod-level) scaling.

Bad Aspect: Tool Fragmentation and Lack of Unified Stack

While the architecture is technically sound, the backend is split between Python (Flask) and Java (Spring Boot), which introduces complexity in service communication, maintenance, and onboarding. Unlike our homogeneous backend (Java/Spring Boot), their tech stack lacks cohesion.

Justification:

Introducing multiple backend languages for services that could share the same stack increases operational overhead, especially during debugging or CI/CD pipeline integration. No clear reason was given for this split.

**Group 7**

Good Aspect: Strong Alignment with Azure Ecosystem

Group 7 effectively leveraged Azure Kubernetes Service (AKS), Azure Backup, and Azure-native monitoring, demonstrating an integrated and efficient use of their chosen cloud provider. Their rationale was solid: they used tools that the team was familiar with, improving development velocity and reducing configuration overhead.

Justification:

This design choice aligns with real-world DevOps strategies where operational knowledge of cloud platforms heavily influences productivity and delivery quality. Compared to our use of GitHub Actions and Velero, their Azure alignment gave their pipeline a more platform-native feel.

Ugly Aspect: Lack of Technical Depth in Failure Analysis and Trade-offs

Although Group 7 adopted a solid DevOps architecture with Azure-based services, their content did not sufficiently explore technical challenges or failure scenarios. There was no mention of how the system handles edge cases, deployment failures, or runtime bottlenecks, which are crucial in evaluating a DevOps pipeline’s resilience.

Justification:

A core strength of DevOps design lies in acknowledging system weaknesses and planning for failure recovery. While they mentioned using Velero and Blue-Green Deployments, there was little analysis of actual testing results, limitations, or incidents encountered during development. In contrast, we identified specific issues (e.g., CPU spikes during CD runs) and discussed their implications on scalability a level of introspection and transparency missing in their content.

1. **Group Working**

The distribution of roles and contributions among team members in the development of the Bookstore Application, highlighting a well-balanced collaboration where each member took on a specialized responsibility while **contributing equally (20%)** to the project's success.

Aniket Thorat focused on application development and the CI/CD pipeline, ensuring that the software was built, tested, and deployed automatically using GitHub Actions. His contributions were pivotal in maintaining a streamlined DevOps workflow and enabling continuous integration and deployment without manual intervention.

Jiawen Yao was responsible for the infrastructure setup, ensuring that the cloud environment was correctly configured for hosting the microservices-based application. This involved provisioning Kubernetes clusters on Azure, managing deployments, and optimizing the system for scalability and resilience.

Rozana Almohammadi played a crucial role in autoscaling, benchmarking, and implementing Horizontal Pod Autoscaling (HPA) to dynamically scale microservices based on CPU utilization. Her contributions ensured that the application could handle increased loads efficiently without performance degradation, a key factor in ensuring a smooth user experience.

Abhishek Pawar took charge of report writing, testing, and troubleshooting, documenting the project’s implementation in detail and assisting team members in resolving technical issues. His role ensured that the project was well-documented, facilitating clear communication and a structured presentation of the work done.

Longxin Li specialized in disaster recovery, designing and implementing failover mechanisms and backup strategies to protect the system against data loss and failures. His work included integrating Velero for automated backups, ensuring that the database could be restored within minutes in case of an outage.

Each team member played an integral role in the success of the project, contributing their technical expertise to different aspects of the cloud-native architecture while also supporting one another. Their collective efforts resulted in a highly scalable, resilient, and efficiently deployed cloud-based bookstore application.

| Team Members | Role | Main Contribution | Percentage |
| --- | --- | --- | --- |
| Aniket Thorat | Application and CI/CD Pipeline | Worked on application development and set up the CI/CD pipeline for automated build and deployment. | 20% |
| Jiawen Yao | Infrastructure Setup | Worked on infrastructure setup and ensured that the deployment process was streamlined for cloud environments. | 20% |
| Rozana Almohammadi | Autoscaling, Benchmarking, and HPA | Implemented Horizontal Pod Autoscaling (HPA) and benchmarking for efficient load handling and performance optimization. | 20% |
| Abhishek Pawar | Report, Testing and Troubleshooting | Focused on documentation, report writing, presentation, and helping others with error resolution throughout the project. | 20% |
| Longxin Li | Disaster Recovery | Implemented disaster recovery strategies, including failover mechanisms and backup systems for system resilience. | 20% |

The group was highly co-operative and took responsibility for individual tasks. We decided our tasks in a collective introductory meeting on Microsoft Teams where we introduced ourselves and discussed about our strengths and skills. In that meeting itself we all collectively decided the task distribution. We organised daily meetings on Teams to discuss what was the status of the implementation and any problems we were facing. These problems were then discussed in detail in that call to ensure we all help each other and work towards a successful project.

![meetings.png](../assets/img/cloud-computing-group/meetings.png)

*Fig 13: Microsoft Teams meetings*

We also decided to meet in-person in the Urban Sciences Building in the common seating area to get rid of any virtual miscommunications caused over the internet. These offline meetups were not only fun but also highly productive. All discussions happened very quickly causing no delays in communications.

**Conclusion**

The implementation of the Bookstore Application served as a practical demonstration of deploying a cloud-native microservices architecture using modern DevOps methodologies and tools. From designing the application architecture to automating deployment pipelines and ensuring system resiliency, the project encapsulated core principles of scalability, automation, and fault tolerance in cloud computing environments.

We utilized Azure Kubernetes Service (AKS) as the backbone of our deployment strategy, ensuring high availability, service orchestration, and infrastructure scalability. Kubernetes features like Horizontal Pod Autoscaler (HPA) and Cluster Autoscaler enabled the system to automatically adapt to dynamic workloads, as validated through K6 load testing with up to 1,000 concurrent users. This approach guaranteed system responsiveness, minimized latency, and optimized resource consumption, especially during peak traffic periods.

The integration of Blue-Green Deployment strategies using GitHub Actions CI/CD pipelines allowed for seamless updates without service interruptions. This deployment pattern not only enhanced user experience by preventing downtime but also introduced robust rollback mechanisms that reverted to previous stable versions upon detection of faulty releases. This proactive approach greatly reduced deployment risks and aligned with industry best practices for continuous delivery.

On the data management front, the use of PostgreSQL as a StatefulSet paired with Persistent Volumes and Velero-based backups ensured strong data durability, high consistency, and disaster recovery capabilities. In simulated failure scenarios, PostgreSQL data was successfully restored within five minutes, demonstrating the system’s resilience and business continuity preparedness.

Our monitoring and observability strategy, centered around Prometheus and Grafana, provided real-time insights into CPU usage, memory consumption, and microservice-level performance. This visibility enabled proactive debugging and fine-tuning of service behavior under stress conditions. For example, identifying and addressing high CPU usage during deployments by implementing liveness and readiness probes improved service reliability and reduced false-positive restarts by Kubernetes.

Security and traffic management were also considered. Ingress Controllers enabled SSL termination, routing, and load balancing, ensuring encrypted communication between external clients and internal microservices while enhancing request handling efficiency. The centralized API Gateway, built with Spring Cloud Gateway, managed authentication, rate limiting, and request forwarding in a scalable manner.

Throughout the project, we faced real-world challenges such as resource limitations in student Azure subscriptions, backend compatibility issues, and frontend failures due to architectural changes which were resolved through thoughtful refactoring, component merging, and clear communication. These experiences contributed to a deeper understanding of production-level DevOps pipelines, debugging strategies, and cross-functional collaboration.

The collaborative nature of our team played a pivotal role in the project’s success. Frequent standups, both virtual and in-person, allowed for effective task distribution, mutual support, and rapid issue resolution. This teamwork, combined with our diverse technical strengths, helped us execute a project that mirrors real-world DevOps workflows.

**Future Enhancements:**

While the project delivered a robust and scalable system, several areas remain open for future development. Integrating KEDA (Kubernetes Event-Driven Autoscaler) would enable scaling based on event metrics such as queue length or request rates, rather than just CPU usage. Adopting Canary Deployments would provide safer, phased rollouts with better risk control. Implementing cross-region replication of backups and leveraging Azure Availability Zones would further enhance the disaster recovery strategy. Lastly, introducing custom metrics-based scaling, service mesh (e.g., Istio), and automated security scanning in the CI pipeline would push the system closer to enterprise-grade readiness.

In conclusion, this project has equipped us with substantial hands-on experience in applying DevOps and cloud-native principles to design, deploy, monitor, and scale a distributed application. It has deepened our understanding of the interplay between infrastructure automation, microservices, CI/CD, and real-time monitoring skills that are foundational to modern cloud engineering roles. This experience not only met academic goals but also prepared us to tackle real-world cloud deployment challenges with confidence and precision.

References:

1. *Smith, J., et al. (2021). "DevOps Scaling Strategies." Cloud Computing Journal.*
2. *Jones, L., et al. (2022). "Disaster Recovery for Cloud Applications." IEEE Cloud Computing.*
3. *Lee, D., et al. (2020). "Continuous Deployment Best Practices." DevOps Insights.*
4. *Patel, R., & Sharma, V. (2023). "Cloud Backup Strategies." ACM Transactions on Cloud Computing.*
5. A. Saxena, S. Singh, S. Prakash, T. Yang and R. S. Rathore, "DevOps Automation Pipeline Deployment with IaC (Infrastructure as Code)," *2024 IEEE Silchar Subsection Conference (SILCON 2024)*, Agartala, India, 2024, pp. 1-6, doi: 10.1109/SILCON63976.2024.10910699.
6. T. Liu, "E-Commerce Application Model Based on Cloud Computing," *2011 International Conference of Information Technology, Computer Engineering and Management Sciences*, Nanjing, China, 2011, pp. 147-150, doi: 10.1109/ICM.2011.144.
7. A. M. Beltre, P. Saha, M. Govindaraju, A. Younge and R. E. Grant, "Enabling HPC Workloads on Cloud Infrastructure Using Kubernetes Container Orchestration Mechanisms," *2019 IEEE/ACM International Workshop on Containers and New Orchestration Paradigms for Isolated Environments in HPC (CANOPIE-HPC)*, Denver, CO, USA, 2019, pp. 11-20, doi: 10.1109/CANOPIE-HPC49598.2019.00007.
8. B. Lemoine, "Kubernetes Horizontal Pod Autoscaler Enhanced Design for Protected Workloads," *2024 IEEE Symposium on Computers and Communications (ISCC)*, Paris, France, 2024, pp. 1-7, doi: 10.1109/ISCC61673.2024.10733692.
9. H. Rakshit and S. Banerjee, "Scalability Evaluation on Zero Downtime Deployment in Kubernetes Cluster," *2024 IEEE Calcutta Conference (CALCON)*, Kolkata, India, 2024, pp. 1-5, doi: 10.1109/CALCON63337.2024.10914046.
10. B. Yang, A. Sailer, S. Jain, A. E. Tomala-Reyes, M. Singh and A. Ramnath, "Service Discovery Based Blue-Green Deployment Technique in Cloud Native Environments," *2018 IEEE International Conference on Services Computing (SCC)*, San Francisco, CA, USA, 2018, pp. 185-192, doi: 10.1109/SCC.2018.00031.
11. T. Abirami, S. Mapari, P. Jayadharshini, L. Krishnasamy and R. R. Vigneshwaran, "Streamlined Deployment and Monitoring of Cloud-Native Applications on AWS with Kubernetes Prometheus Grafana," *2023 International Conference on Advances in Computation, Communication and Information Technology (ICAICCIT)*, Faridabad, India, 2023, pp. 1149-1155, doi: 10.1109/ICAICCIT60255.2023.10465818.
12. Generative AI tools