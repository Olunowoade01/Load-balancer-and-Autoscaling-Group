# Load-balancer-and-Autoscaling-Group
This load balancer and Autoscaling Group

1. # The purpose of this project to understand the concepts of high availability and scalability in cloud computing 

2. To learn how to create target groups and set up an Application Load Balancer

This project will be divided into 2 stages:

1. Setting up an Application Load Balancer (ALB)
2. Configuring the Auto Scaling Group.


1. ## Stage 1: Setting up the Application Load Balancer

An Application Load Balancer is a type of load balancing service that distributes incoming application traffic across multiple targets, such as EC2 instances.

### Step 1: Setting up ALB

> create 2 instance the first inatnce will have the configuration 


![1](./img/1%20first%20ec2.png)


 > A new security is created ssh and http inbound rule is added to the security.

![2](./img/2%20VPC%20AUTO%20SIGN%20.png)


 - i configure and follow the same process for my second EC2 

![3](./img/4%20stage%202%20ec2.png)

![4](./img/still%20stage%202.png)


- Both EC2 instances was created successfully:

![5](./img/5%20stage%202%20ec2%20created.png)


2. #  The next step i click on my first instance and copy the IP address to paste on web browser

![6](./img/copy%20first%20inatnce%20ip.png)


 > i copy the first ip address and paste on the web broser and it's working properly 



![running](./img/%20Ec2%20instant%20working.png)



 > i followed the same procedure  and choose my second instance and copy the IP address to paste on web browser

![7](./img/second%20ip.png)



  > my second IP address working perfectly


![running](./img/only%20use%20for%20second%20ip.png)


3. # Create a Load Balancer

   # After a succesfully testing the both IP address the next stage is to create a load balancer to route traffic between them

> from the EC2 consol i stroll down the Load balancer and click on it 

![load balancer](./img/low%20balance.png)


# After chosing the load balancer console it take me to the next stage where i hit the create load balancer

![create LB](./img/create%20load%20.png)


 # After moving to the next stage i choose to create a flexible feature set for application with HTTP traffic


![create](./img/create%20load%20b2.png)


# during the process of creating my load balancer, i created a new security group and new target group to add to my traffic


![target and sg](./img/new%20security%20group.png)



 > New target group

added a new name and allow HTTP port 80

ip address IPV4

and choose my previous vpc 

ip address IPV4

![TG](./img/tg%20group.png)


i Selected both instances and click on "Include as pending below"


>  my taregt group as been created and the next step is to select both instance and click on include as pending bellow

![TG2](./img/tg%20stage2.png)


#  Target group successfully created the next step to return back to my load balancer and complete my creation

![tg3](./img/tg3.png)




![ld b](./img/ld%20b.png)


 > A summary of what of my application load balancer i configure by generating a name and using internert facing and allow IPv4, 
> on security group using the security group that i created (alb-demo-sg-1) which as port 80 and HTTP traffic 
> on network mappin i use the avaliable network zone in the vpc

> listener and routin, i allow HTTP port 80 and connected to my (my-alb-demo-tg) on target group 
p


![LB SUMMARY](./img/ld%20b.png)




> load balance created succeffuly
and in active state.


![ldb](./img/ld%20balancer%20created%20.png)




# Testing the Load Balancer

1. **Copy the DNS Name:**

   > The next stage is too copy the DNS name and paste it on web browser to confirm if working properly

if we refresh the page the ip keep change to another host 
this show that that traffic is been relying aroun d the two instance

![dns](./img/dns.png)

 > Let's same something goes wrong with our first instance going we can semulate by going back to our instance and select  one of the instance to stop 




![instant](./img/instant%20stop.png)


> if we  rephresh that we will noticed one instant as stop working and others still running 




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























