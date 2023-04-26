# Launch from template

1. On EC2, on the left click on Launch Template then create launch template

![image](https://user-images.githubusercontent.com/129314018/234646886-b4532536-52cf-4f54-be1f-a4f2f8ebc82b.png)

2. On the following page give your template a name using a similar naming convention shown below, and check the Auto scaling guidance.
3. Then Find your AMI, in our case we used Ubuntu 18.04 (18.04 LTS, amd64 bionic image build on 2022-09-01)

![image](https://user-images.githubusercontent.com/129314018/234649175-ad55fd6c-d853-4272-8fce-ae32769213b2.png)

4. Make instance type t2.micro, and key pair name as your key pair, in our case this was tech221.
5. On Security Groups, we use an existing pair with our HTTP, SSH and 3000 ports, HTTP and 3000 on anywhere adn SSH to our ip

![image](https://user-images.githubusercontent.com/129314018/234649520-9db9e888-1a53-4d85-92e7-5daba4a9c588.png)
![image](https://user-images.githubusercontent.com/129314018/234649576-0f59920e-1aa5-4b83-aa61-dcdf6a67ae6d.png)

6. Under Advanced Details, we scroll to User data and input the following code

```
#!/bin/bash 
sudo apt update -y 
sudo apt upgrade -y 
sudo apt install nginx -y
```

![image](https://user-images.githubusercontent.com/129314018/234650164-d573cb44-b9c6-4529-9508-85e87b29b97f.png)

7. Click create launch template, and navigate on the left to Auto scaling groups

![image](https://user-images.githubusercontent.com/129314018/234650302-1fb6fcc7-0354-4bd5-a932-c9413d1739c0.png)

8. Launch ASG, and now we use similar naming convention to before for the group name, and then we select our Launch template we created before, click next

![image](https://user-images.githubusercontent.com/129314018/234650732-58da977c-5b1e-407a-8764-0949d76cbc88.png)

9. We use default vpc, and for our Availability Zones (AZ) we select 3 AZs, click next

![image](https://user-images.githubusercontent.com/129314018/234650910-62bb80e3-56d6-43ec-8ded-b05cbaf85e31.png)

10. Attach Load balancer, then we use application load balancer as we are dealing with HTTP and HTTPS, and make sure we are internet facing , as we are working over the internet

![image](https://user-images.githubusercontent.com/129314018/234651089-614ebd87-bdae-4d0a-91f8-4b4888c95b55.png)

11. Under default routing, we create a target group, and using a similar naming convention to below we name our target group (tells a load balancer where to direct traffic to)

![image](https://user-images.githubusercontent.com/129314018/234651233-12f1a069-4178-4d8b-be5a-917c887bbeab.png)

12. On health checks, we check to turn on the health checks, when unhealthy, auto scaling can create new EC2 instances when necessary, click next.

![image](https://user-images.githubusercontent.com/129314018/234651346-4b27ecdc-fcc9-45ee-ae77-951af0e051b1.png)

13. Set the group size, desired capacity at 2, min capacity at 2, and maximum capacity at 3, so there is always 2 instances, and if needed, the maximum it can make is 3 instances. For scaling policies click target tracking scaling policy, change it if necessary and we keep it the same. Click next

![image](https://user-images.githubusercontent.com/129314018/234651493-2e229743-12cb-4d86-85e7-c548872ef971.png)

14. On the tags, we add Name to the Key, and we use a naming convention like `mohammad-tech221-asg-alb-app`, click create Auto scaling group.

![image](https://user-images.githubusercontent.com/129314018/234651975-80396ee1-a254-4b8c-b69a-45c876f3eb45.png)


![image](https://user-images.githubusercontent.com/129314018/234652022-5af259df-3655-452a-8c88-1e893567d209.png)
![image](https://user-images.githubusercontent.com/129314018/234652115-ec934db2-9e66-4c15-bb5c-22d651e8685a.png)
