# Introduction

Every topic has a hands on lab

## What will be covered
- Devops Pre-Requisites
- Fundamentals of Java, NodeJS, Python 
- GIT
- Containers
- Docker
- Kubernetes
- YAML
- Microservices Architecture
- Ansible and Terraform

## DevOps Tools

1. Develop 
2. Build
    + ./build.sh (build script to call build tools)
        + Maven
        + Gradle
        + etc...
3. Deploy
    + Move the built application executable and associated libraries to production from Development

### Development
Development teams
- Git helps multiple developers manage code itterations and changes
    + Github, Gitlab and Bitbucket are common publicly hosted central respositories for Git
    + 'git pull' pulls data from the repository to use locally
    + 'git push' pushes local copy of data to the central repository

### Build
Pushing new code to production is risky so testing is required prior to production deploy.

This makes the new flow:
1. Develop
2. Build
3. Test
4. Deploy

Manual testing and deployment makes code releases a time consuming process that is prone to errors. That is where Continuous Integration and Continuous Deployment (CI/CD) tools come into play.

#### CI/CD Pipeline

Tools:
- Jenkins
- Github Actions
- Gitlab CI/CD

The CI/CD tool pulls the commited application changes from the git repository and automates the build, test and deploy processes. This speeds the release of version changes with less manual intervention.

The application realease process is now automated but that means that underlying infrastucture changes that need to be made to facilitate the new or revised application are a point of contention for release of the application. Also, the build, test and production environments should be configured similarly to ensure that the application works as expected in production.

#### Containers

Containers can be used to package the application and dependancies into a single wrapper without having to be concerned that the requirements are incorrect in the various environments. 

- Docker 
    + Creates a Dockerfile that which specified dependancies and can be used during the build to create a, image that can then be run on any Docker environment using the 'Docker run' command

Now we have a Docker container image that can be run on any Docker engine. As the application usage increases, we can add the image to multiple Docker servers to spread the load but will need to ensure container status. This is where container orchestration tools come into play.

#### Container Orchestration

- Kubernetes is a popular container orchestration system. It can manage the container resources, auto scaling, manage fault tolerance, and underlying server resource usage. 

#### Infrastructure as Code (IaC)

The underlying infrastructure for the environment including servers, network, applications to be installed (Docker, Kubernetes Worker, etc... ), security, etc... will all need to be managed. Manually creating these items can be time consuming and prone to errors.

Provisioning tools like Terraform can automate the deploy, upgrade and removal of infrastructure and ensures that the servers configured are always in the same state.

If there is a change made outside of Terraform, it can be revered back to the required state as maintained in the Terraform state file.

Because the provisioning files are code, they can be stored in the Git repository. 

#### Configuration Management

While Terraform and other IaC tools (like Cloudformation, Powershell DSC, etc) can be used to maintain the infrastructure provisioning, configuration of the underlying OS, application installs and configuration, etc, require a Configuration Management tool or process. 

Ansible is used for post provisioning configuration. It uses code in the form of Ansible Playbooks. 

This code can also be stored in the Git repository

#### Monitoring and Observability

Once the environemnt is provisioned and configured, in order to verify there are no issues, monitoring and observability tools and processes are needed. 

Prometheus is a popular monitoring framework. 

Grafana is a popular dashboard and visualization tool for observability data.

Devops is a combination of People, Processes and Tools that bring you from an idea to a supportable and sustainable product release. 









