
# 4 Golden Signals of monitoring - what to monitor

Latency: Time taken for request to complete. Help identify performance bottleneck, network issues .etc.

Traffic: Volume of requests processed bys sytem ,help understand usage patterens, scalability needs, spikes or drops in demand

Errors: rate of failed requests, help identify bugs, software issues, external dependencies causing disruptions or impacting system functionality negatively.

Saturation: measures system resource utilisation, such as cpu, memory disk, network. Monitoring this, can help resource exhaustion, performance decrease, and failures due to resource constraints.

# 4 Golden Rules of Monitoring - how to monitor

Monitor everything that matters: monitor all critical components, and metrics that impact performance, availability and security of systems. 

Monitor proactively, not reactively: stop waiting for issues to occur, proactive monitoring aims to detect and address problems before they impact the syste, ensures optimal system performance, and minimise downtime

Monitor from the user's perspective: reflect end user experience, measuring response time, transaction success rates and user interaction, can provide insight for whrre to improve

Alert intelligently and take action: generating alerts is important, make sure that they are relevant, actionable and not overwhelming. Thresholds and fine tuning the alert rules can enable effective and timely resolution of the issues


# Why we need to monitor

# What is alert management

# SNS simple notification service

# SQS simple queue service

![image](https://user-images.githubusercontent.com/129314018/235122550-5b579a5d-f54d-488e-b58b-9a175b27e67f.png)

![image](https://user-images.githubusercontent.com/129314018/235124560-5a5fc93d-8b8c-469d-90f9-3b7fe7a803d8.png)


# Cloud Watch
## SNS topic
* Launch an instance  through EC2
* On the search bar type `SNS` and click the amazon sns service
* on the left click `topics` and `create topic`
* provide a name for your topic we use `mohammad-tech221-sns`
* and create the topic

## Email sub
* In the SNS interface, select the topic we just made
* click `create subscription` and choose the protocol as `email`
* enter your email address as the `endpoint`
* create subscription and check your email to confirm this subcription


## Cloudwatch alarm
* Search cloudwatch in search bar and click
* on the left click alarms then create alarms
* the ec2 instance we made, on another tab navigate to details and copy the instance id
* back on cloudwatch interface, on the metrics, we paste our id and after clicking instances, we then click and find the cpu utilisation metric for that instance
* On conditions set your desired threshold, we use 10% as upon previous testing it refused to go above 50 due to simple while loops, we also set the period to 1 minute, if it doesnt work, use 5 minutes at first and you can copy it after and change it to 1 min
* then under actions, we click send notification to amazon sns topic
* we then choose the sns topic we made earlier
* and then click create alarm

## Create Dashboard
* on the left of cloudwatch interface, we click dashboards -> create dashboards
* provide a name for your dashboard, we use the similar naming convention as before, but we add `-dashboard` at the end
* we then create dashboard -> add widget, select preferred widget we went with graph type
* repeat what we did before and paste instance id to select our metric, and find cpu utilisation
* if further customisation is needed do as you please
* create widget
* and it should now be present on your dashboard

## Testing
* to test this we ssh into our ec2 instance
* make a `cpu_load.py` file to test if an alarm is sent to email
* a simple while loop can stimulate cpu utilisation

```
import time

while True:
    # Print a message to simulate CPU utilization
    print("CPU is busy!")

    # Sleep for a short duration to control the loop speed
    time.sleep(0.1)
```

* While it is stimulating, refer to your dashboard on cloudwatch, by navigating on the left hand bar, and click on your newly made dashboard
* if you can see it goes above the threshold check your email now and then
* eventually you should recieve an email which would look something like this, which should show it is in fact working.

![image](https://user-images.githubusercontent.com/129314018/235139470-a7f2c9ff-0b1c-4cef-abbe-95272da687b5.png)






