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

       ![image](https://github.com/lokeshwankhede-star-star/Event-Bridge-Architecture-on-EventBridge/assets/81281161/2e3b316b-bfc7-4aae-b021-7948675d58c0)

C) Send Event through " Event buses ":
  
  - Navigate and click on " Event buses ".
  
  ![image](https://github.com/lokeshwankhede-star-star/Event-Bridge-Architecture-on-EventBridge/assets/81281161/afeca5ca-be9c-49f8-9a8c-45ea436fb883)

  - Click on your Event bus ex. " orders "
  - Click on " Send events " (on top)
  
  ![image](https://github.com/lokeshwankhede-star-star/Event-Bridge-Architecture-on-EventBridge/assets/81281161/5fb00cc8-73d2-4ed0-bcd1-32ffd440f9db)

- Send events:
    - Destination: Event bus
    - Event bus: ex. orders
    - Event source: com.anycompany.orders
    - Detail type: new-order
    - Event detail: copy and paste " event.json " file code
    - Send
  
  a. Priority shipping event
  
  ![image](https://github.com/lokeshwankhede-star-star/Event-Bridge-Architecture-on-EventBridge/assets/81281161/b9d6da3d-00e7-4e06-8f71-df451148b86d)

  ![image](https://github.com/lokeshwankhede-star-star/Event-Bridge-Architecture-on-EventBridge/assets/81281161/3d5058b1-5b86-4c9f-b172-c24a532090fc)
  
  ![image](https://github.com/lokeshwankhede-star-star/Event-Bridge-Architecture-on-EventBridge/assets/81281161/43449657-fbca-4a3d-80ec-04b5968d44d1)

  b. Cannada shipping event

  - Click on your Event bus ex. " orders "
  - Click on " Send events " (on top)
  
  ![image](https://github.com/lokeshwankhede-star-star/Event-Bridge-Architecture-on-EventBridge/assets/81281161/5fb00cc8-73d2-4ed0-bcd1-32ffd440f9db)

    - Send events:
        - Destination: Event bus
        - Event bus: ex. orders
        - Event source: com.anycompany.orders
        - Detail type: new-order
        - Event detail: copy and paste " event.json " file code
        - Send

  ![image](https://github.com/lokeshwankhede-star-star/Event-Bridge-Architecture-on-EventBridge/assets/81281161/e5238cc1-93ab-494f-99d3-2009ae11cbf0)

  ![image](https://github.com/lokeshwankhede-star-star/Event-Bridge-Architecture-on-EventBridge/assets/81281161/b73554d6-94ad-4ed3-ab22-e89a7b3f7117)

  
D) Check Cloudwatch log group:

  - Search for " CloudWatch " in console
    
    ![image](https://github.com/lokeshwankhede-star-star/Event-Bridge-Architecture-on-EventBridge/assets/81281161/4742d4ea-0d72-4bae-8b42-82480ae7cc89)

  - Inside " Logs "  click on " Log group " (Present in left naviagation panel)
  
    ![image](https://github.com/lokeshwankhede-star-star/Event-Bridge-Architecture-on-EventBridge/assets/81281161/8ea1936f-b5af-4ce0-8566-b8dfb19312c8)
    
  - Click on " /aws/events/priority-shipping " log group.
  - Click on " Log streams " recent event
  
    ![image](https://github.com/lokeshwankhede-star-star/Event-Bridge-Architecture-on-EventBridge/assets/81281161/6edfbea1-3504-4a79-bd67-4275c51bb27e)

  - Expand " Timestamp " and review message
  
    ![image](https://github.com/lokeshwankhede-star-star/Event-Bridge-Architecture-on-EventBridge/assets/81281161/c5a7ae9f-548d-44ee-a023-adf6c1714c44)

  - Go back and click on " /aws/events/canada-shipping " log group.
    
    ![image](https://github.com/lokeshwankhede-star-star/Event-Bridge-Architecture-on-EventBridge/assets/81281161/dab45ee7-42e6-452e-ae6b-8ceab9fd6051)

  - Click on " Log streams " recent event

    ![image](https://github.com/lokeshwankhede-star-star/Event-Bridge-Architecture-on-EventBridge/assets/81281161/f3e09803-18f0-42b8-af60-fcc296929226)
    
  -  Expand " Timestamp " and review message

  ![image](https://github.com/lokeshwankhede-star-star/Event-Bridge-Architecture-on-EventBridge/assets/81281161/d395ac59-da49-4a87-8c2d-345f0f79a9b5)
  
---
## API Destination:

EventBridge an API destination refer to the endpoint where eventbridge sends events for further processing. When configuring an API destination in eventbridge you 
specify an API endpoint that can recieve HTTP events this event could be an AWS service a third-party application or a custom HTTP endpoint

----
A) Get " API endpoint " 
  
  - Go on Webhook site (https://webhook.site/#!/9bfc5ac3-073a-47e5-8d69-b71446d52861/389c27d3-c611-4bc3-b2ad-4879ed9d040a/1)
  - Copy and Save the address " Your unique URL "
      - Note: Don't close the tab
      
 ![image](https://github.com/lokeshwankhede-star-star/Event-Bridge-Architecture-on-EventBridge/assets/81281161/3887380c-6b17-4ad9-9d48-11912bffb374)
           
B) Set up " API Destination "

  - Go on " AWS EventBridge "  
  - Click on " API Destination " (in down left navigation panel).
  
  ![image](https://github.com/lokeshwankhede-star-star/Event-Bridge-Architecture-on-EventBridge/assets/81281161/c6b6b81a-4456-459e-87ae-4241b4a32ba5)

  - Create " API Destination " 
      - Name: priority-shipping
      - Description - optional
      - API destination endpoint: paste the address that you copy from Webhook site ("https://webhook.site/9bfc5ac3-073a-47e5-8d69-b71446d52861")
      - HTTP method: POST
      - Invocation rate limit per second - optional
      - Connection: Create a new connection
          - Connection name: Priority-shipping-auth
          - Description - optional
          - Destination type: Other
          - Authentication type: Basic (Username/Password)
          - Username: ex. Anycompany
          - Password: ex. Anycompany     
      - Create
      
  ![image](https://github.com/lokeshwankhede-star-star/Event-Bridge-Architecture-on-EventBridge/assets/81281161/7fdb1fe1-15e7-46b0-b0bc-c38011534d29)
  
  ![image](https://github.com/lokeshwankhede-star-star/Event-Bridge-Architecture-on-EventBridge/assets/81281161/6cda93cf-df6e-4a0c-85be-74bcd4761976)
   
  ![image](https://github.com/lokeshwankhede-star-star/Event-Bridge-Architecture-on-EventBridge/assets/81281161/b8bd9a51-b9e7-482c-ac81-283cdc841462)
 
  ![image](https://github.com/lokeshwankhede-star-star/Event-Bridge-Architecture-on-EventBridge/assets/81281161/48a51e89-af18-4db0-8d31-5acc9c80cf78)

C) Add " API Destination " in " Rule "

  - Click on " Rule " (in left navigation panel).
  - Choose " Orders " in Event bus section
  - Select and Click on " Priority-Shipping "
  
          ![image](https://github.com/lokeshwankhede-star-star/Event-Bridge-Architecture-on-EventBridge/assets/81281161/e0ff72e2-533e-4548-9c7b-7975fe2cef7e)

  - Go in Target tab
      - Edit
   
          ![image](https://github.com/lokeshwankhede-star-star/Event-Bridge-Architecture-on-EventBridge/assets/81281161/63087599-bc5b-441d-92ed-25e6f36417c1)
 
  - Select target 
      - Add another target
      - Target types: EventBridge API destination  
      - API destination: priority-shipping    
      
          ![image](https://github.com/lokeshwankhede-star-star/Event-Bridge-Architecture-on-EventBridge/assets/81281161/e07bdd0f-d0a8-449e-887d-e42557182cfd)    
  
          ![image](https://github.com/lokeshwankhede-star-star/Event-Bridge-Architecture-on-EventBridge/assets/81281161/0f1eb7fe-02b6-4d66-ac5d-c966035bf0cb)

  - Additional Settings (Expand)
      - Configured target input: Input Transformer
      
          ![image](https://github.com/lokeshwankhede-star-star/Event-Bridge-Architecture-on-EventBridge/assets/81281161/c8730487-deed-426b-a9c7-d270158606c7)

      - Click on Configured Input Transformer
      
          ![image](https://github.com/lokeshwankhede-star-star/Event-Bridge-Architecture-on-EventBridge/assets/81281161/8cc0f193-e2e0-4a58-bb36-dd362470f150)

  - Sample event : Enter my own
      -  Copy and paste " sample_event_type.json " file code
      
          ![image](https://github.com/lokeshwankhede-star-star/Event-Bridge-Architecture-on-EventBridge/assets/81281161/8f0ead1d-db1d-4779-8a9b-f8b2a55a4953)

  -  Target Input Transformer:
      -  Input path 
          - Copy and paste " target_input_transformer.json " file code
              
          ![image](https://github.com/lokeshwankhede-star-star/Event-Bridge-Architecture-on-EventBridge/assets/81281161/a5fa7326-094b-4e1b-b148-ac759cbf14b3)
  
  -  Templater:
      -  Copy and paste " target_input_transformer_template.json " file code
            
            ![image](https://github.com/lokeshwankhede-star-star/Event-Bridge-Architecture-on-EventBridge/assets/81281161/9a1585ea-cc0a-4c79-bfed-fe0b471cdbe3)

            - Click on output
            
            ![image](https://github.com/lokeshwankhede-star-star/Event-Bridge-Architecture-on-EventBridge/assets/81281161/7b2297d6-e9de-45e2-8072-e5c1107f18e4)

            - Review all detail (If right go next)
       - Confirm
       - Next
       
      ![image](https://github.com/lokeshwankhede-star-star/Event-Bridge-Architecture-on-EventBridge/assets/81281161/23a10ccc-dba5-48d3-b3d3-098f95473b93)

  - Next
  
      ![image](https://github.com/lokeshwankhede-star-star/Event-Bridge-Architecture-on-EventBridge/assets/81281161/13cae46d-33c1-4862-b0ae-5ce383261fbd)

  - Review and Update rule
      
      ![image](https://github.com/lokeshwankhede-star-star/Event-Bridge-Architecture-on-EventBridge/assets/81281161/9ba0a3a6-6578-4b4c-8c16-21fa230dc513)
     
      ![image](https://github.com/lokeshwankhede-star-star/Event-Bridge-Architecture-on-EventBridge/assets/81281161/0612d0ca-6f79-4773-a668-7373038eb287)

D) Send " Event " through " Event bus "

  - Click on " Event buses" (on left navigation panel)
  
      ![image](https://github.com/lokeshwankhede-star-star/Event-Bridge-Architecture-on-EventBridge/assets/81281161/6be4fb4e-3069-4710-9eb1-dcbe2e9ed0cd)

  - Click on your event bus ex. " orders "
      
  - Click on " Send Event "
      
      ![image](https://github.com/lokeshwankhede-star-star/Event-Bridge-Architecture-on-EventBridge/assets/81281161/b33fd6ce-d107-4cb7-87e1-2289777a2b75)

    - Send events:
        - Destination: Event bus
        - Event bus: ex. orders
        - Event source: com.anycompany.orders
        - Detail type: new-order
        - Event detail: copy and paste " event.json " file code (Note: Priority Shipping code)
        - Send
  
      ![image](https://github.com/lokeshwankhede-star-star/Event-Bridge-Architecture-on-EventBridge/assets/81281161/f4cdc2f6-38fa-4a33-9658-595c7fcafb94)
 
      ![image](https://github.com/lokeshwankhede-star-star/Event-Bridge-Architecture-on-EventBridge/assets/81281161/020e0898-1471-47db-a957-33e445341fc4)
      
      ![image](https://github.com/lokeshwankhede-star-star/Event-Bridge-Architecture-on-EventBridge/assets/81281161/613dae6a-e3a6-4cd1-98ec-0b087cbbca54)


E) Final Stage

  - Go on Webhook site.
  - Check message details on site  

      ![image](https://github.com/lokeshwankhede-star-star/Event-Bridge-Architecture-on-EventBridge/assets/81281161/7ffa9f74-e997-4a86-b675-961eb0a406d3)

---
  ## Congratulations 🎊 you have completed event driven architecture with EventBridge
---
