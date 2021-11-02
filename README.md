# PROYECT: OLYMPIC GAMES NEWS

# INDEX
* [Objetives](#objetives)
  * [General Objetives](#general-objetives)
  * [Specific Objetives](#specific-objetives)
* [General Description](#general-description)
* [General Diagram of The System](#general-diagram-of-the-system)
* [System Flow Explanation](#system-flow-explanation)
  * [Local Machine](#local-machine)
  * [Google Load Balancer](#google-load-balancer)
  * [API Replicas](#api-replicas)
  * [Services on Google Cloud Platform](#services-on-google-cloud-platform)
  * [Virtual Machines On The Cloud](#virtual-machines-on-the-cloud)
  * [Google Pub Sub](#google-pub-sub)
  * [App Engine](#app-engine)
  * [Cloud Run - App](#cloud-run---app)
  * [Databases](#databases)
* [Reflection Questions](#reflection-questions)

## Objetives

### General Objetives

Create a distributed computing system, cloud native, by using different services from **Google Cloud Platform**, **operating-system-level virutalization** with **Docker** and **ContainerD** and traffic generators to be applied to a current topic.

### Specific Objetives

- Apply the knowledge of containers, images, composition files, and networks between containers.
- Experiment with and use **Cloud Native Technologies** that help develop modern distributed systems.
- Generate traffic and divide it on the network using specific tools such as **Locust** and **Cloud Load Balancer.**
- Create a web app using the library **React**, one of the frameworks with the most labor demand in the market.
- Use a wide range of **IaaS**, **PaaS** and **SaaS** cloud services from the GCP provider.
- Use modern languages to create a distributed application.
- Compare two different databases in the cloud: **Azure Cosmos DB** and **Google Cloud SQL.**

## General Description

After the end of the Tokyo 2021 Olympic games, the initiative is taken by your group of students from the course of
operating systems 1 in order create a visualizer of the news and commentary of the Olympics
that the spectators are doing.
The system will be entirely in the cloud, using different services from the Google Cloud Platform and a database on
Cosmos DB from Microsoft Azure. It will have a massive load of data from different
traffic generators, the information to send will be detailed later. In addition to this system,
there will be an "Administrator" mode in which you can view relevant graphs and metrics of the
news, and information on RAM and virtual machines to be created in the cloud.

## General Diagram of The System

> Areas:

- [Local Machine](#local-machine) (Purple Rectangle)
- [API Replicas](#api-replicas) (Blue Rectangle)
- Google Gloud Platform (External skyblue square)
  - [Virtual Machines In The Cloud](#virtual-machines-on-the-cloud) (Internal skyblue square)
- [Databases](#databases) (Green Rectangle)

> <img src = ''>

## System Flow Explanation

The system will have different parts, each of which is crucial for the system to work properly. These parts are divided by colors in the [diagram above](#general-diagram-of-the-system).

### Local Machine

The components in this part will be stored in the members' local machine, these do not need be in the cloud.
The purpose of the applications in this part is to send traffic to the **Google Cloud Load Balancer**
(detailed later). Basically these applications have to have the following functionalities:

- Read a `.json` file that contains an array of data (the respective data for each traffic generator).
- Process the file and send traffic to an endpoint.
- Show how much data was sent and how much data had error.

The information to be sent by the three traffic generators is the following:

> <img src = ''>

### Google Load Balancer

A Cloud Load Balancer must be configured [https://cloud.google.com/load-balancing](https://cloud.google.com/load-balancing) which will receive all the
traffic created by `Locust` and the other two traffic generators, this will redirect the traffic to the different services to implement.


### API Replicas

There will be three APIs that will work in exactly the same way (hence the "replica") but they will be
made in different languages. The functionality of these APIs is to receive the traffic that is generated and passes through
the Load Balancer, to then pass this information to the database and create a notification using Google
PubSub. The student should consider which routes are necessary to pass this traffic, but as a start
and suggestion are the following:

- `/startLoad`: A path that will be able to connect to the database and wait for the data to be loaded.
- `/publish`: A path that will have the option of publishing the information to the database.
- `/finalLoad`: A route that will close the connection to the databases and send a notification through from Google PubSub.

The three languages to implement will be:

- Python
- Go
- Rust

For each of these languages, the same API functionality to connect to the database must created
so that they send information from traffic generators. Also, a notification via `Google Pub/Sub` must be created to know how many records were uploaded.

### Services on Google Cloud Platform

### Virtual Machines On The Cloud

### Google Pub Sub

### App Engine

### Cloud Run - App

### Databases

## Reflection Questions
