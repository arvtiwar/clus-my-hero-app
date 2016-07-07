# Devnet Workshop - Mantl: How to use it.

This workshop is designed for Cisco Live "Devnet Workshop - Mantl: How to use it" session. In this workshop you will learn how to use Mantl to deploy your micro-services application and how to manage the application using Cisco's Mantl platform. In this workshop we expect attendees have basic knowledge of containers, micro-services architecture and REST APIs.  

# Section 1: Application overview

In this workshop we will be using "MyHero App" application which is being developed with micro-services paradigm to demonstrate Mantl capabilities. MyHero App is a simple application which allow users to vote for their favorite super hero and gather the voting results. The application is built in a microservice style wrapping each service in a docker container that can be deployed and run on Mantl.  In its initial form the application has three services.

1. [myhero/data](https://github.com/hpreston/myhero_data) - This service stores all the data about candidates and votes cast.
2. [myhero/app](https://github.com/hpreston/myhero_app) - This service provides the basic logic layer for accessing and recording votes.
3. [myhero/web](https://github.com/hpreston/myhero_web) - This is the main user interface for casting votes.

![MyHero Demo Application](diagrams/myhero-demo-i1.png)

# Section 2: Application Deployment

## Prerequisites

Following are the prerequisites for the attendees.

- Linux operating system based laptop (Cygwin may also work).
- GIT and CURL installed.
- Standard Web browser.

## Mantl UI walkthrough

Open "https://mantlsandbox.cisco.com" on web browser and enter credentials as provided, this will open Mantl UI. On this page you will see different tiles for Mesos, Martahon, Consul and Traefik which are the core open source technologies used by Mantl. Please click on these  tiles one by one to explore these technologies.

#### Note: More information provide over workshop.   

## Application deployment on Mantl

### Download MyHero application

#### How:

Open a Linux shell/terminal and run "git clone https://github.com/CiscoCloud/clus-my-hero-app", this will download the application from the git repository to clus-my-hero-app directory.

### Environment setup

Environment setup is the first step to interact with Mantl API, this will setup Mantl endpoints and credentials to sign in to the Mantl UI.

#### How:
From the same terminal/shell move to "clus-my-hero-app" directory and run "source myhero_setup" to enter and record the deployment name, address, application domain, username, and password for your Mantl instance as non-persistent Environment Variables. This means you will need to run this command everytime you open an new terminal session.

#### Note:
Please do not close this terminal/shell.

### Deploy my-hero-app on Mantl

#### How:
Run ./myhero-install.sh to deploy all three services (data, app, web) to your Mantl cluster.

After running the install it will take a 2-5 minutes for all three services to fully deploy and become "healthy". You can monitor this in the Marathon Web GUI.

## Access the my-hero-app

You should be able to reach the web interface for the application at http://DEPLOYMENTNAME-web.YOUR-DOMAIN where DEPLOYMENTNAME refers to the deployment name provided at setup and YOUR-DOMAIN refers to the wildcard domain configured for Traefik.

#### Note:

Application URL was give at the environment setup step.

# Section 3: Application Management

## Mantl UI walkthrough with my-hero-app

Open "https://mantlsandbox.cisco.com" on web browser and enter credentials as provided, this will open Mantl UI. On this page you will see different tiles for Mesos, Martahon, Consul and Traefik which are the core open source technologies used by Mantl.

1. Click on the Mesos tile and look at the tasks, you will find tasks related to the application name you have give while setting up the environment.

2. Click on Marathon tile to open Marathon UI, here you can investigate individual services from the MyHero application. Click on the "Configuration" tab to explore about the service configuration. You can scale up/down the service from this tab as well.

####Note:
Please ask help from the Cisco engineers if needed.    


## Use of REST API

Mantl provide REST APIs to access its individual components (Mesos, Marathon etc...), REST APIs are good for integration purpose. To make this session easy we have created a CLI (command line interface) which uses Mantl REST APIs to interact with Mantl. To use the CLI you have to set CLI environment.   

#### How:

Run "source myhero-cmd.sh" from the same linux shell/terminal to setup the environment.

### List Applications

Run "myhero_list_apps" to list the application you have just deployed. This will return response in JSON format.


### Get Application details

Run "myhero_get_app" command to get the details about application.

### Scale UP the application

Run "myhero_scale_up_web" command to scale up the application, it will prompt to you current number of instance.  

### Scale down the application

Run "myhero_scale_down_web" command to scale down the application.

## Destroy MyHero Application

In this steps we will destroy the application along with all micro-services from the Mantl cluster.

####How:

Run ./myhero-uninstall.sh to remove all three services from Marathon.

####Note:

You can verify the current state using REST API or using the Mantl UI.