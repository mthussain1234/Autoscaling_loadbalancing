# Autoscaling and Load Balancing

![image](https://user-images.githubusercontent.com/129314018/234577046-e731407f-8133-4584-a309-28f6221364ed.png)

* Load balancing distributes incoming traffic across multiple EC2 instances, we can see this in the diagram above
* Application load balancers (ALB) is provided by AWS
  * Routes incoming traffic to **Targets** such as EC2 instances
* Network Load balancers (NLB) route traffic based on IP protocol data (TCP OR UDP)
  * Used for applications such as gaming, media streaming, lets them handle large amounts of traffic
* Classic Load Balancer (CLB) - used for simple applications - eg distributing traffic across multiple EC2 instances

* Autoscaling is a feature which can automatically adjust the number of EC2 instances based on the current demand of the appilcation
* You can scale up - increase resources allocated
* Scale out - adding more EC2 instances to handle increased workload
* Scaling down - reducing resources allocated depending on demand

* You can use both Autoscaling and Load balancing together as shown in the diagram
  * When combined, lets you create a system to automatically add/remove EC2 instances in response to the load
  * The LB will route traffic across these instances, and will deem them to be **healthy** or not
  * If needed autoscaling will ad new instance to the **auto scaling group**
  * auto scaling can remove an instance from the group
  * if an existing instance is deemed **unhealthy**, it will be taken out of the service

* ASG Policy is set of rules that govern scaling behaviour of asg 
  * Types of scaling policies - target tracking, simple scaling, step scaling

* Target tracking
  * Uses predefined metric to maintain resource util
  * EG to maintain CPU util at 50%
  * ASG will automatically adjust number of EC2 instances, to maintain this 50% CPU util

* Target Group
  * Resources registered with ALB
  * Target groups can be EC2 intances, IP addresses
  * Target group defines protocol and port used to communicate with tehse resources within the group


