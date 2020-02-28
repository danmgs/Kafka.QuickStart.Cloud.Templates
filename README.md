# Kafka.QuickStart.Cloud.Templates

Docker-compose templates for Cloud providers Microsoft Azure and AWS to deploy micro-services application leveraging Kafka producer-consumer pattern.

![alt capture](https://github.com/danmgs/Kafka.QuickStart.Cloud.Templates/blob/master/img/Azure_frontend.gif)

## 1. Folder organization

```
| -- /AWS/
     | -- Dockerrun.aws.json

| -- /AZURE/
     | -- docker-compose-extended-azure.yml
     | -- docker-compose-light-azure.yml      -> light version
```

## 2. Prerequisites

- You need to have an [Microsoft Azure account](https://portal.azure.com) or [AWS account](https://aws.amazon.com/fr/console/).
- You need to create [Twitter API keys](https://developer.twitter.com/en/apps).

## 3. High Level Architecture

![alt capture](https://github.com/danmgs/Kafka.QuickStart.Cloud.Templates/blob/master/img/architecture_hld.png)

## 4. Instructions

### 4.1. Docker images

These are docker-compose templates for deployment under Azure or AWS.

It uses docker images hosted in Docker Hub Registry.

They are compatible with for **Linux OS**.

|  Docker images                                          | Docker Repository                                                                                 | Description
| :-----------------------------------------------------: | --------------------------------------------------------------------------------------------------| --------------------------
| zookeeper:3.4.9                                         | [link](https://hub.docker.com/_/zookeeper)                                                        | Zookeeper
| confluentinc/cp-kafka:5.4.0                             | [link](https://hub.docker.com/r/confluentinc/cp-kafka)                                            | Kafka
| danmgs/kafkaquickstart-backend-console-producer:1.8     | [link](https://hub.docker.com/repository/docker/danmgs/kafkaquickstart-backend-console-producer)  | Kafka C# Console Producer
| danmgs/kafkaquickstart-backend-console-consumer:1.8     | [link](https://hub.docker.com/repository/docker/danmgs/kafkaquickstart-backend-console-consumer)  | Kafka C# Console Consumer
| danmgs/kafkaquickstart-middleware-webapi:1.7            | [link](https://hub.docker.com/repository/docker/danmgs/kafkaquickstart-middleware-webapi)         | C# WebAPI
| danmgs/kafkaquickstart-frontend-webapp:1.7              | [link](https://hub.docker.com/repository/docker/danmgs/kafkaquickstart-frontend-webapp)           | Angular WebApp


### 4.2. Configuration

Before using these templates, you need to configure the Twitter config options:


|  Options                        | Instructions                                             | Mandatory/Optional
| :-----------------------------: | ---------------------------------------------------------| --------------------
| TWITTER_OAUTH_CONSUMER_KEY      | to replace with your twitter API key                     | Mandatory
| TWITTER_OAUTH_CONSUMER_SECRET   | to replace with your twitter API secret                  | Mandatory
| TWITTER_SEARCH_INTERVAL_MS      | checks frequency in ms of tweets (*)                     | Optional
| TWITTER_SEARCH_KEYWORD          | keyword for tweet search (***musique*** by default)      | Optional

(*) Note Twitter has a [throttling limit](https://developer.twitter.com/en/docs/basics/rate-limiting) with "Too Many Requests" 429 response code. Choose milliseconds value accordingly (not too small)


### 4.3.1 Deployment under Azure

We will create a web app in **App Service**.

1. Select Publish: ***Docker container*** and Operating System: ***Linux***

<details>
  <summary>Click to expand details</summary>

  ![alt capture](https://github.com/danmgs/Kafka.QuickStart.Cloud.Templates/blob/master/img/Azure_app_service_1.PNG)

</details>

2. Select Docker Options: ***Docker compose*** and Image Source: ***Docker Hub***.

3. Upload configuration file **docker-compose-extended-azure.yml**

<details>
  <summary>Click to expand details</summary>

  ![alt capture](https://github.com/danmgs/Kafka.QuickStart.Cloud.Templates/blob/master/img/Azure_app_service_2.PNG)

</details>

### 4.3.2 Deployment under AWS

We will create a web app in **ElasticBeanstalk**.

1. Create an environment by selecting ***Web Environment tiers***
2. Select Platform: ***Multi-container Docker***
3. Upload configuration file **Dockerrun.aws.json**
4. Select **Configure More Option**, in the **Capacity**, you should select EC2 instance type: ***t3 medium*** at least (minimum requirement).

<details>
  <summary>Click to expand details</summary>

  ![alt capture](https://github.com/danmgs/Kafka.QuickStart.Cloud.Templates/blob/master/img/AWS_elasticbeanstak_1.PNG)

</details>
