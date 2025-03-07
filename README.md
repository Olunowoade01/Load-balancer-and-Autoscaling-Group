# Load-balancer-and-Autoscaling-Group
This load balancer and Autoscaling Group

1. # The purpose of this project to understand the concepts of high availability and scalability in cloud computing 

2. To learn how to create target groups and set up an Application Load Balancer

This project will be divided into 2 stages:

1. Setting up an Application Load Balancer (ALB)
2. Configuring the Auto Scaling Group.


1. ## Stage 1: Setting up the Application Load Balancer

Application Load Balancer (ALB) is a type of load balancer service that distributes incoming application traffic across multiple targets, such as EC2 instances, containers, and IP addresses, in multiple Availability Zones. 

Application Load Balancer (ALB) operates at the application layer (Layer 7) of the OSI model. This allows it to perform more advanced functions compared to traditional load balancers. Specifically, it can handle HTTP/HTTPS traffic, making it ideal for web applications.


## Step 1: Setting Up the Application Load Balancer (ALB)
 > Creating Two EC2 Instances

The first step in setting up the Application Load Balancer (ALB) is to launch two EC2 instances that will serve as the targets for the load balancer. The instances will handle the application traffic routed by the ALB.


![1](./img/1%20first%20ec2.png)


 > A new security group is created, and inbound rules are configured to allow SSH (port 22) for remote access and HTTP (port 80) to handle web traffic.


![2](./img/2%20VPC%20AUTO%20SIGN%20.png)


 - I followed the same configuration process for the second EC2 instance, ensuring that it was set up with identical settings as the first instance.

![3](./img/4%20stage%202%20ec2.png)

![4](./img/still%20stage%202.png)


- Both EC2 instances was created successfully:

![5](./img/5%20stage%202%20ec2%20created.png)


>  Firstly, we are going to test our instances by Checking if our public IPv4 addresses has access to the web server.
> 
![6](./img/copy%20first%20inatnce%20ip.png)


 > The public IP address for the first and second ec2 instance is copied and added to a web browser. The result shows our instance has access to the internet.


![running](./img/%20Ec2%20instant%20working.png)



 > I followed the same procedure for the second instance, selected it, copied its IP address, and pasted it into the web browser.

![7](./img/second%20ip.png)



  > The IP address of the second instance is working perfectly.


![running](./img/only%20use%20for%20second%20ip.png)


3. ## Create An Appliction Load Balancer

 > I Navigate to *Load Balancers* option under the Ec2 menu, select *create Load balancer*, and select *application Load balancer* as we are using HTTP for web pages.



![load balancer](./img/low%20balance.png)


> After selecting the Load Balancer console, I was taken to the next stage where I clicked on Create Load Balancer.

> This version improves the flow and readability. 



![create LB](./img/create%20load%20.png)


> After moving to the next stage, I selected the option to create a flexible feature set for an application that supports HTTP traffic.


> This version ensures the process is clear and concise.

![create](./img/create%20load%20b2.png)


 ## Creating Traget Group

> Luckily for us, AWS has made it easy to create a target group just as you are configuring your Load balancer. 

- The Target group will be named '*my-alb-tg*

- The 2 instances will be selected and '*incuded as pending below*'


![target and sg](./img/new%20security%20group.png)



 > New target group

added a new name and allow HTTP port 80

ip address IPV4

and choose my previous vpc 

ip address IPV4

![TG](./img/tg%20group.png)


i Selected both instances and click on "Include as pending below"


> My target group has been created, and the next step is to select both instances and click on "Include as Pending" below.

![TG2](./img/tg%20stage2.png)


#  The target group was successfully created. The next step is to return to my load balancer and complete the creation process.

> This version enhances readability and flow.

![tg3](./img/tg3.png)




![ld b](./img/ld%20b.png)


 > In summary, we have created an Application Load Balancer that is internet-facing, we are using the ALB-demo-SG as our security group which has port 80 open for HTTP traffic. We are using 3 different availabiltiy zones in the VPC so it is highly available, and we are listening for traffic on port 80 which would then route to our target group which has 2 instances in it.



![LB SUMMARY](./img/ld%20b.png)




> The load balancer was created successfully and is now in an active state.

![ldb](./img/ld%20balancer%20created%20.png)




# Testing the Load Balancer
1. Copy the DNS Name:

The next step is to copy the DNS name of the load balancer and paste it into the web browser to verify that it is working properly.

When I refreshed the page, I noticed that the IP address kept changing to a different host. This indicates that traffic is being distributed between the two instances.

![dns](./img/dns.png)

 > Let’s simulate a scenario where something goes wrong with the first instance. To do this, we can go back to our EC2 instances and stop one of them.




![instant](./img/instant%20stop.png)


> If we refresh the page, we will notice that one instance has stopped working while the other is still running.




![instant](./img/instant%20stop%20n2.png)



 > if we moved to the targert group and choose the demo that i created, it's going to show that one is healthy and another is unused, this show the result of the instant that we stop and we return back to the loads balance and rehpresh the page we  see that is only one hosting


![target](./img/target%20check.png)



## PART 2

### Creating an Auto Scaling Group

1. **Search for Auto Scaling Group:**

   - I Proceed to the search bar on the AWS console, search for "Auto Scaling Group" and click on it.

![ASG](./img/Part%202%20ASG%20CREATING.png)



2. **Create a Launch Template:**
   - After getting to the Auto Scaling Group console, i proceed to create a launch template.

     ![part 2](./img/PART%202%20ASG%202.png)





3. **Configure the Launch Template:**
   
- I navigated to the new tab where i have the lunch template,
i choose a name for my template "my-new-asg-lt"
on the quick start section i choose the AWS Management console this will provide me with a pre-configured AWS Maching to lunch instant
instant type i choose the t2 micro
and procced to create a new keypair(my-new-key) and attached with my public subnet that allow to access traffic flow on my web browser.




     ![template](./img/lunch%20template%201.png)
     ![template 2](./img/lunch%20template%202.png)





4. #Auto Scaling Template Creation


  > Auto scaling Template successfully created and the next page is to return back to my previous auto scaling and procced.


     ![template](./img/template%20succesfully%20created%20.png)



5. **Create the Auto Scaling Group:**

   - During process of creating Auto scaling, i provided a name for my Auto scaling group "New-asg"
and lunch with the template i already created "my-new-asg-lt"

     ![auto](./img/auto%20scsling%2011.png)



   also attached with my VPC and allow all my available network

- both subnet was attached that allow HTTP PORT-80

     ![auto](./img/auto%20scalling12.png)

6. **Set Desired Capacity:**


   - I choose 1 for Min desired capacity and 4 for Max desired capacity.


     ![auto](./img/auto%20scaling%2014.png)




7. **Auto Scaling Group Creation:**

   
- Auto scaling group succesfully created 

     ![auto](./img/auto%20scaling%20succ.png)



8. **Instance Creation:**

   Auto scaling Group has successfully created instance according to the desire capacity i specifield which in this case is 2

     ![auto](./img/auto%20management.png)



9. **Verify Load Balancer:**

   - I navigated to the Load Balancer on EC2 page and noticed that our load balancer as also been created.


     ![load balancer](./img/load%20balance%20for%20auto.png)





## Project Reflection

- Explored the significance of the high Availability and scalability in cloud infrastructure


- understood the concept of Auto scaling group and how they dynamically adjust the number of instance based on workload.




## PROJECT GOALS


1. > i learned about Load Balancers and Auto Scaling Groups in AWS



2. I explore the importance of load balancing and auto-scaling in maintaining the reliability availability and performance of web application.
























