# Event Bridge Architecture on EventBridge
Event Driven Architecture with Event Bridge include Event Bus, Rules, API Destination, Log Group

---
## Amazon EventBridge: 
It is a serverless event bus service that makes it better and easier to build event driven application at scale using events from your application integrated with SaaS.

- Pay for event you publish to your event bus.
- It's uses event to trigger and communicate between decoupled service it is common in microservices.
- Multiple event source and target to integrate.
- Powerful event routing and filitering capability.
- Want to build a central event bus for your application.

## Another choice:

- AWS Lambda
- AWS SQS
- AWS SNS
- AWS DynamoDB Streams

## When to use which:

- AWS Lambda:
  - Execute custom code in response to events.
  - On demand compute and auto-scaling.
  - Short lived function require quick and execution.

- AWS SQS (Simple Queue Service):
  - Reliable and asynchronous communication between comp.
  - Want to develop component and manage high volume event processing.
  - Feature like message durability,scaliability,fault tolarance.

- AWS SNS (Simple Notification Service):
  - Send notification or message to multiple subscribers.
  - Flexible push/subscriber messaging service.
  - Want to support various protocols and endpoints for message delivery.

- AWS DynamoDB Streams :
  - Capture and process changes to data in real time.
  - You need to track and react to changed in DB tables.
  - Want to trigger specific action based on thouse changes.

## Problem Statement:
  - Anyone company is a shipping provider company there needs are:
      - Anyone expanding there company in canada require new shipping provider.
      - US based customer who worth 100 $ of goods there they have to provide priority based shipping provider faster required new shipping provider.
      - Launches loyality program check customer buy program or belnog to program acquire rewards points for them.

# Project:
---

A) Create " Event buses ":
  
  - Log in to AWS console (https://aws.amazon.com/).
  - Search for " Amazon EventBridge ".
  
  ![image](https://github.com/lokeshwankhede-star-star/Event-Bridge-Architecture-on-EventBridge/assets/81281161/f2a8a9d8-5e6e-4fd6-9854-4d35177cf24e)
  
  - On left navigation panel click on " Event buses ".
  
  ![image](https://github.com/lokeshwankhede-star-star/Event-Bridge-Architecture-on-EventBridge/assets/81281161/c6f19bd6-9dfc-420f-a691-e87d5b6fc917)
  
  - Click on " Create event bus ".
      - Name: ex. orders
      - Event archive: disabled
      - Schema discovery: disabled
      
  ![image](https://github.com/lokeshwankhede-star-star/Event-Bridge-Architecture-on-EventBridge/assets/81281161/0c25a9cf-cc65-476e-9f4c-0ce45c8fb25d)
  
  ![image](https://github.com/lokeshwankhede-star-star/Event-Bridge-Architecture-on-EventBridge/assets/81281161/c5af3117-85a4-4670-b459-8577c2161375)
  
B) Create " Rules ":
  
  - Click on " Rules "
  - Select Event bus as " orders "
  - Click on " Create rule "
  
  ![image](https://github.com/lokeshwankhede-star-star/Event-Bridge-Architecture-on-EventBridge/assets/81281161/f6f37ed1-1046-4006-a868-4e2dcabcc57a)
  
a. Priority-Shipping:

  - Click on " Create rule "
  - Define rule detail:
 
       - Name: Priority-Shipping
       - Description: When customer from US and buy more than 100 $ provide priority shipping.
       - Event bus: orders
       - Rule type: Rule with an event pattern
       
       ![image](https://github.com/lokeshwankhede-star-star/Event-Bridge-Architecture-on-EventBridge/assets/81281161/69ad6930-acc9-4f51-839a-2591f8c96d07)

  - Build event pattern:
 
       - Event source: Other
       - Creation method: Custom pattern (JSON editor)
       - Event pattern: copy and paste " priority_shipping_code.json " file code
       
       ![image](https://github.com/lokeshwankhede-star-star/Event-Bridge-Architecture-on-EventBridge/assets/81281161/5a6c5fe2-393a-4a25-bf4f-393f5e245bad)
       
       ![image](https://github.com/lokeshwankhede-star-star/Event-Bridge-Architecture-on-EventBridge/assets/81281161/e76d558f-5efa-4fbf-a1a9-2f31da2e9592)

  - Select target(s):
 
       - Target types: AWS service
       - Select a target: CloudWatch log group
       - Log Group: priority-shipping
       
       ![image](https://github.com/lokeshwankhede-star-star/Event-Bridge-Architecture-on-EventBridge/assets/81281161/39c4ac69-2cc6-418b-9fa7-b977eb36e598)

  - Configure tags - optional:
 
       - Next
       
  - Review and create:
 
       - Review
       - Create rule
       
b. Canada-Shipping:
  
  - Click on " Create rule "
      - Note: Make sure you seleted " orders " in " Event bus ".
   
       ![image](https://github.com/lokeshwankhede-star-star/Event-Bridge-Architecture-on-EventBridge/assets/81281161/ccaaa8f9-517d-45ff-aa63-c5dcc31260fc)
 
  - Define rule detail:
 
       - Name: Canada-Shipping
       - Description: When customer from CA provide canadian shipping.
       - Event bus: orders
       - Rule type: Rule with an event pattern
       
       ![image](https://github.com/lokeshwankhede-star-star/Event-Bridge-Architecture-on-EventBridge/assets/81281161/1975a0c2-44be-48b8-bda2-71b078cbb7c9)

  - Build event pattern:
 
       - Event source: Other
       - Creation method: Custom pattern (JSON editor)
       - Event pattern: copy and paste " canada_shipping_code.json " file code
       
       ![image](https://github.com/lokeshwankhede-star-star/Event-Bridge-Architecture-on-EventBridge/assets/81281161/5a6c5fe2-393a-4a25-bf4f-393f5e245bad)
       
       ![image](https://github.com/lokeshwankhede-star-star/Event-Bridge-Architecture-on-EventBridge/assets/81281161/4623aafb-735f-4e33-b4a5-c97c8b61fce0)

  - Select target(s):
 
       - Target types: AWS service
       - Select a target: CloudWatch log group
       - Log Group: canada-shipping
       
       ![image](https://github.com/lokeshwankhede-star-star/Event-Bridge-Architecture-on-EventBridge/assets/81281161/362a827b-cff6-4436-96e2-7453e013e7e3)

  - Configure tags - optional:
 
       - Next
       
  - Review and create:
 
       - Review
       - Create rule     

A) Send Event through " Event buses ":
  
  - Navigate and click on " Event buses ".
  
  ![image](https://github.com/lokeshwankhede-star-star/Event-Bridge-Architecture-on-EventBridge/assets/81281161/afeca5ca-be9c-49f8-9a8c-45ea436fb883)

  - Click on your Event buses ex. " orders "
  - Click on " Send events " (on top)
  
  ![image](https://github.com/lokeshwankhede-star-star/Event-Bridge-Architecture-on-EventBridge/assets/81281161/5fb00cc8-73d2-4ed0-bcd1-32ffd440f9db)

- Send events:
    - Destination: Event bus
    - Event bus: ex. orders
    - Event source: com.anycompany.orders
    - Detail type: new-order
    - Event detail: copy and paste " event.json " file code
    
    
  ![image](https://github.com/lokeshwankhede-star-star/Event-Bridge-Architecture-on-EventBridge/assets/81281161/5299ffde-b160-47ab-8ed3-36d44a5e549c)

  ![image](https://github.com/lokeshwankhede-star-star/Event-Bridge-Architecture-on-EventBridge/assets/81281161/3d5058b1-5b86-4c9f-b172-c24a532090fc)




       
       
     



