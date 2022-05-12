# AWS IoT Core
AWS IoT Core enables you to connect devices to AWS Services and other devices, secure data and interactions, process and act upon device data, enables applications to interact with devices even when they are offline

## AWS IoT Device SDK
The AWS IoT Device SDK enables your devices to connect, authenticate, and exchange messages with AWS IoT Core using the MQTT, HTTP, or WebSockets protocols.

## IoT Device Gateway
- The Device Gateway serves as the entry point for IoT devices connecting to AWS.
- Ensure that devices are able to securely and efficiently communicate with AWS IoT Core
- supports the MQTT, WebSockets, and HTTP 1.1 protocols.
- MQTT or WebSockets can provide bidirectional connections
- Fully managed and scales automatically to support over a billion device

## IoT Message Broker
- High throughput pub/sub message broker with low latency
- Supports messaging patterns ranging from one-to-one and one-to-many and use topic to forward message
- Fully managed service

## IoT Registry
- The Registry establishes an identity for devices and tracks metadata such as the devices’ attributes and capabilities.
- Each device get Unique ID regardless the type of device.
- Support metadata of each device(such as report temperature in C or F)
- Can create X.509 certificates to help IoT device to connect to AWS.

## Authentication
-  3 Authentication method
    - SigV4 (HTTP, WebSockets)
    - X.509 certificate based authentication (HTTP, MQTT)
    - Customer created token based authentication (HTTP)
- Mobile apps 
    - Amazon Cognito

## Device Shadow
- Json document represent the state of a connected thing
- We can set the state to a different state
- The IoT things will retrieve the state when online and adopt.

## IoT Rule Engine
- Evaluates inbound messages
- transform and deliver to another device or cloud service based on business rule
- Rules engine can route message to AWS end points including IoT Analytics, IoT Event, Lambda, Kinesis, S3, DynamoDB, CloudWatch, SNS, SQS, OpenSearch and step function.
- You can auther rules, they are SQL like syntax.

## IoT Greengrass
- Bring the compute layer to the device directly
- can execute Lambda function at device.
    - Pre-process data
    - Execute prediction based on ML model
    - Keep device data sync
    - Communicate between local device
- Operate Offline
- Deploy functions from the cloud to device directly.