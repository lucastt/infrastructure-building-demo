# About this project

In this repository, I will create a multi-provider platform for infrastructure creation and automation, build and deploy the app user-agent-parser-demo.

My intension with this is to study, demonstrate and have a reference for my self on how to build a production ready platform to run services in the cloud.

The tools I intend to use are make, terraform, ansible, kubernetes and spinnaker. For personal interess I will create this infrastructure for two major cloud providers GCP and AWS, but I can exted the project in the future to study other cloud providers.

For application understanding, please refer to the app repository, In this repository I will focus only in the building blocks of its infrastructure.

# Planning and project objectives

Here I'll expose what I plan to do with each tool and the priority of each task. Some of this features will be implemented on parallel since it can depend on each other, but the priority will be represented in the following list:

1. Terraform

  - Machine and service topology;
  - Design the infrastructure necessary to support the application in a extremely reliable and easy to understand manner;
  - Design a multi-cloud provider structure;
  - Write terraform files that represent the designed infrastructure.
  
2. kubernetes

  - Test the app localy with mini kube, micro k8s or something like that, to explore what we coulkd do;
  - Config k8s cluster from the ground up in a multi-region format;
  - Run the app on the cluster;
  - Implement meaningful healthchecks for the application and check it within kubernetes;
  - Use envoy as cluster ingress and load balancer;
  - Build unified logging and monitoring in the cluster;
  - Make adjusts on the app and infrastructure archtecture if needed.
  
3. Ansible

  - Automate all machine machine configuration to run kubernetes;
  - Automate kubernetes cluster configuration.
  
4. CI/CD and spinnaker

  - Configure CI/CD for the app;
  - Configure and run spinnaker;
  - Explore spinnaker options;
  - Design a good CD format using spinnaker.
  
5. Comparison and conclusions

  - Run and compare the sulution to other managed solutions like EKS and GKE;
  - Write clonclusions and thoughts
  
6. Plan the next steps...

  - What can I do to expand my knoledge? List it and start priorization and implementation;
  - A nice idea is to apply chaos engineering to the platform, implement reliability improvements exposed by the tests and compare the performance of the tests runned in the created infra structure to a similar managed solution. 
  
  
As a final observation, this project has three hard requirements:

1 - All interactions with the platform should happen through make;
2 - All implementation should be done for GCP **and** AWS;
3 - Each decision made by the developer should be documented in a journal format.


In this project I'll not accept PR from any other developer besides me, since this project is intended to help me study and understand each of this tools. **But** if anyone have any comment or sugestion would be very welcome, constructive comments and tips will accelerate my learning process and give me insights, serving for the propose of this project.

# Project structure

TODO

# Project arquitecture

TODO

# Usage

TODO
