# About this project

In this repository, I will create a multi-provider platform for infrastructure automation, build and deploy of the app [user-agent-parser-demo](https://github.com/lucastt/useragent-parser-demo).

My intention with this is to study, demonstrate and have a reference for my self on how to build a production ready platform to run services in the cloud.

The tools I intend to use are `make`, `terraform`, `ansible`, `kubernetes` and `spinnaker`. For personal interess I will create this infrastructure for two major cloud providers GCP and AWS, but I can exted the project in the future to study other cloud providers.

For application understanding, please refer to the app repository, In this repository I will focus only in the building blocks of its infrastructure.

# Planning and project objectives

Here I'll expose what I plan to do with each tool and the priority of each task. Some of this features will be implemented on parallel since it can depend on each other, but the priority will be represented in the following list:

1. Terraform

  - [x] Machine and service topology;
  - [x] Design the infrastructure necessary to support the application in a extremely reliable and easy to understand manner (meaning the underlying resouces, e.g. networking, loadbalancing etc);
  - [x] Design a multi-cloud provider structure;
  - [ ] Write terraform files that represent the designed infrastructure:
    - [ ] Build dockefile, makefile to run the automation code isolated;
    - [ ] Create a network host project;
    - [ ] Create subnets;
    - [ ] Create the app server project;
    - [ ] Create VMs;
    - [ ] Create user-agent-parser project and build the datalayer within it.
  
2. kubernetes

  - [ ] Test the app localy with mini kube, micro k8s or something like that, to explore what we coulkd do;
  - [ ] Config k8s cluster from the ground up in a multi-region format;
  - [ ] Run the app on the cluster;
  - [ ] Implement meaningful healthchecks for the application and check it within kubernetes;
  - [ ] Use envoy as cluster ingress and load balancer;
  - [ ] Build unified logging and monitoring in the cluster;
  - [ ] Make adjusts on the app and infrastructure archtecture if needed.
  
3. Ansible

  - [ ] Automate all machine machine configuration to run kubernetes;
  - [ ] Automate kubernetes cluster configuration.
  
4. CI/CD and spinnaker

  - [ ] Configure CI/CD for the app;
  - [ ] Configure and run spinnaker;
  - [ ] Explore spinnaker options;
  - [ ] Design a good CD format using spinnaker.
  
5. Comparison and conclusions

  - [ ] Run and compare the sulution to other managed solutions like EKS and GKE;
  - [ ] Write clonclusions and thoughts
  
6. Plan the next steps...

What can I do to expand my knoledge? List it and start priorization and implementation:
  - Adicionar monitoramento + trancing + metricas (SLOs), agregar e visualizar essas métricas no kibana;
  - A nice idea is to apply chaos engineering to the platform, implement reliability improvements exposed by the tests and compare the performance of the tests runned in the created infra structure to a similar managed solution;
  - It would be nice to manage a multi-cluster infrastructure in the future, create and edge loadbalancing layer in front of the clusters.
  
  
As a final observation, this project has three hard requirements:

1. All interactions with the platform should happen through make;
2. All implementation should be done for GCP **and** AWS;
3. Each decision made by the developer should be documented in a journal format.


In this project I'll not accept PR from any other developer besides me, since this project is intended to help me study and understand each of this tools. **But** if anyone have any comment or sugestion would be very welcome, constructive comments and tips will accelerate my learning process and give me insights, serving for the propose of this project.

# Project structure

I'm not sure how I would integrate the infrastructure with the code. Some people say that is better to keep this infrastructure project in the same repository of the code, but I saw many projects working well with these files separated. In this project I want to make a generic structure. The structure will be like this:

```
.
├── docs
│   ├── diagrams
│   └── images
├── Makefile
├── README.md
└── src
    ├── dev
    │   ├── ansible
    │   ├── k8s
    │   └── terraform
    │       ├── aws
    │       │   └── cloud-resource-name
    │       └── gcp
    │           └── cloud-resource-name
    └── prd
        ├── ansible
        ├── k8s
        └── terraform
            ├── aws
            │   └── cloud-resource-name
            └── gcp
                └── cloud-resource-name
```

This structure should be generic for both aproaches.

# Project arquitecture

### System topology

###### Compute layer (k8s)
![Compute layer (k8s)](docs/images/compute_layer.png?raw=true "")

Initially the cluster will have six machines in the compute layer. The master (M1) will be alocated in the region us-east1, and the master replica (M2) will be alocated in us-west1, two other nodes will be alocated in each region.

Initially, each master/node will run in a really samall machine, for GCP f1-micro, for AWS the equivalent of f1-micro. This is not really defined yet, since I don't know if the node can support the application.


###### Data layer (MongoDB)

![Data layer (MongoDB)](docs/images/data_layer.png?raw=true "Data layer (MongoDB)")
  
The application uses mongo DB, because mongo is web scale. Just kidding, when I wrote the app I was going to work in a brief project that use mongo DB, so I used my dummy app as a excuse to learn more about mongo.

Mongo DB will run in two VMs. One of the VMs will run two instances of mongo DB (or one instance of mongod and other of mongo arbiter, that is not defined yet) and the other VM will run just one instance. Each VM will be in a different region. And last, but not least, a bucket will be created to store database backups, this bucket will be located in a third region us-central1. This settup will ensure great availability and reliability.

### System design

![System design overview](docs/images/demo_infra_design.png?raw=true "System design overview")

There is not much to say here. All the project will be in the same network, only two structures will have public IP, bastion protected with IAM and firewalls and te cluster ingress. Databases will be in a separate subnet protected by firewall. Backup will be stored in a cloud storage product (google storage or S3), it will be protected with IAM and encription.I tried to keep the system simple, if someday I build a multi cluster structure  this diagram will change a bit. Some other structures are not present in this diagram, thing like DNS. By no means this diagram is complete, I'll increment it as the project goes.

The table bellow will specify the subnets and their IP ranges.

| Subnet name    | Subnet IP range |
| :------------- | :----------:    |
| App subnet     | TODO            |
| DB subnet      | TODO            |
| Bastion subnet | TODO            |


# Usage

TODO
