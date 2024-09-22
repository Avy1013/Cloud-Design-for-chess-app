# AWS Cloud Solution Design Assessment

Design an AWS solution for deploying a chess game app using Next.js, NestJS, PostgreSQL, Redis, and WebSockets.

## Index 
Based on the assignment.

 [﻿1. Areas to Address / Architecture](https://app.eraser.io/workspace/LXyWDIR0FnhhI3qyr58x#k63luBNs44BG2ZsrbFS4t) 

 [﻿2. Web socket scaling](https://app.eraser.io/workspace/LXyWDIR0FnhhI3qyr58x#K6PeO2XIaXtcVLz58mdpX) 

 [﻿3. Scaling & Cost Efficiency ](https://app.eraser.io/workspace/LXyWDIR0FnhhI3qyr58x#fV23ysPdagzfaaFpVIXC2) 

 [﻿4. Security ](https://app.eraser.io/workspace/LXyWDIR0FnhhI3qyr58x#ZiSp_FxmBMU4fiY5DtqJA) 

 [﻿5. Database ](https://app.eraser.io/workspace/LXyWDIR0FnhhI3qyr58x#CrPmzObHiTk6V2UED8_dI) 

 [﻿6. Scheduling ](https://app.eraser.io/workspace/LXyWDIR0FnhhI3qyr58x#hwuT0vhWRlE5qx7_fzon3) 

 [﻿7. Miscellaneous](https://app.eraser.io/workspace/LXyWDIR0FnhhI3qyr58x#JaqFQ66rYNUtx85mmpUo_) 

## 1. Areas to Address / Architecture
![image.png](https://eraser.imgix.net/workspaces/LXyWDIR0FnhhI3qyr58x/Wj1jhlmToeb6zuLN9H866cyMv1L2/2sTvTDPim4r7t0aMW6yQA.png?ixlib=js-3.7.0 "image.png")

**Technologies used**: 

- **ECS**: Manages and orchestrates Docker containers with EC2
- **EC2**: Provides scalable virtual servers.
- **Route 53**: Manages DNS and domain routing.
- **CloudFront**: Delivers content via a global CDN.
- **Application Load Balancer (ALB)**: Distributes incoming application traffic.
- **Next.js**: Framework for building server-rendered React applications.
- **NestJS**: Backend framework for building scalable server-side applications.
- **PostgreSQL (RDS)**: Managed relational database service.
- **Redis (ElastiCache)**: In-memory caching for improved performance.
- **IAM**: Manages access and permissions for AWS resources.
- **Secrets Manager**: Safely stores and manages sensitive information.
- **CloudWatch**: Monitors and logs AWS resources and applications.
## 2. Web socket scaling
### Api Gateways
AWS API Gateway is used as it serverless nature handles WebSocket scaling by automatically managing the number of concurrent connections, ensuring high availability and reducing infrastructure management overhead. 

## 3. Scaling & Cost Efficiency 
 • **Auto-Scaling**:

 • Utilize ECS/Fargate with Auto Scaling policies based on CPU and memory usage to dynamically adjust the number of containers.

 • For RDS, enable read replicas and use RDS Auto Scaling to handle variable database loads efficiently.

 • **WebSocket Handling**:

 • Use API Gateway for WebSocket scaling to automatically manage concurrent connections without manual server management.

 • **Cost Optimization**:

 • Use Reserved/spot Ec2 instances for savings

 • Implement **CloudFront** as a CDN to cache static content globally, reducing server load and bandwidth costs.

 • Cache frequently accessed data in **ElastiCache (Redis)** to reduce database queries and improve response times.

## 4. Security 
 • **IAM (Identity and Access Management)**:

 • Implement the principle of least privilege by granting minimal permissions necessary for users and services.

 • Use IAM roles and policies for secure, granular control over access to AWS resources.

 • Enable Multi-Factor Authentication (MFA) for added security on critical accounts.

 • **VPC (Virtual Private Cloud) and Subnets**:

 • Deploy resources in a VPC with private and public subnets to control network traffic.(as shown in the figure)

 • Use security groups to restrict inbound and outbound traffic to only required ports and IP ranges.

 • Implement Network Access Control Lists (NACLs) for an additional layer of security.(Not shown in the figure)

 • **Secrets Manager**:

 • Securely store and manage sensitive information like database credentials and API keys.

 • Enable automatic rotation of secrets to enhance security and reduce the risk of credential exposure.

 • **CloudWatch**:

 • Monitor AWS resources and applications using metrics, logs, and alarms.

 • Set up CloudWatch Alarms to notify the team of unusual activity or potential issues.

 • Use CloudWatch Logs to track access and error logs for security audits and troubleshooting.

## 5. Database 
 1. **Vertical Scaling**: Increase the RDS instance size when handling higher game loads, such as tournaments or peak times, and scale down during off-peak hours.

 2. **Read Replicas**: Set up read replicas to offload read-heavy operations like fetching game states, player stats, and leaderboard data, ensuring faster response times during high traffic.

 3. **Auto Scaling**: Use RDS Auto Scaling for replicas to dynamically add or remove replicas based on game traffic, maintaining performance and cost-efficiency.

 4. **Multi-AZ for High Availability**: Ensure continuous game availability and quick recovery in case of database failure by deploying RDS in a Multi-AZ configuration.

 5. Utilize ElastiCache to reduce load on the database for frequently accessed data.

## 6. Scheduling 
-  **Automated Game Cleanups**: Redis + lambda can be used to automatically remove old or inactive game sessions at regular intervals, ensuring efficient use of resources without manual intervention.
 • **Leaderboard Updates**: Schedule periodic updates to recalculate and      rank player scores, keeping leaderboards current and accurate for all users.

## 7. Miscellaneous
### For server-- Ec2/ecs vs Fargate
- You can also implement also Fargate instead of ec2 with ecs. If u don't have a idea about the duration and amount of traffic
- Using reserved instances will save costs. If we have idea about the traffic.
- If simplicity is desired over cost Fargate could be a good serverless option.




