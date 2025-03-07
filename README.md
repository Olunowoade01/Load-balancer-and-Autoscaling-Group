# Load-balancer-and-Autoscaling-Group
This load balancer and Autoscaling Group

This project will be divided into 2 stages:

1. Setting up an Application Load Balancer (ALB)
2. Configuring the Auto Scaling Group.


1. ## Stage 1: Setting up the Application Load Balancer

An Application Load Balancer is a type of load balancing service that distributes incoming application traffic across multiple targets, such as EC2 instances.

### Step 1: Setting up ALB

1. **Create 2 EC2 Instances:**
   - The first instance i have the following configuration:


![1](./img/1%20first%20ec2.png)


- A new security group is created with SSH and HTTP inbound rules:

![2](./img/2%20VPC%20AUTO%20SIGN%20.png)


 - I Follow the same process for the second EC2 instance:

![3](./img/4%20stage%202%20ec2.png)

![4](./img/still%20stage%202.png)


- Both EC2 instances were created successfully:

![5](./img/5%20stage%202%20ec2%20created.png)


2. **Test the Instances:**
   - I click on the first instance and copy the IP address to paste into a web browser:

![6](./img/copy%20first%20inatnce%20ip.png)


 - The first instance is working properly:


![running](./img/%20Ec2%20instant%20working.png)



 - I Follow the same procedure for the second instance:
![7](./img/second%20ip.png)



 - The second instance is working perfectly:

![running](./img/only%20use%20for%20second%20ip.png)


3. **Create a Load Balancer:**
   - From the EC2 console,i scroll down to Load Balancers and click on it:

![load balancer](./img/low%20balance.png)



- i Click on "Create Load Balancer":

![create LB](./img/create%20load%20.png)


 - i Choose to create a flexible feature set for applications with HTTP traffic:


![create](./img/create%20load%20b2.png)


- During the process, i create a new security group and a new target group to add to your traffic:


![target and sg](./img/new%20security%20group.png)



 - I added a new name and allow HTTP port 80, and select my previous VPC:

added a new name and allow HTTP port 80

ip address IPV4

![TG](./img/tg%20group.png)


i Selected both instances and click on "Include as pending below"

![TG2](./img/tg%20stage2.png)


- The target group is successfully created. I return to the load balancer and complete the creation:

![tg3](./img/tg3.png)


- A summary of the application load balancer configuration:


![ld b](./img/ld%20b.png)


 - Name: `my-alb`
     - Scheme: Internet-facing
     - IP Address Type: IPv4
     - Security Group: `alb-demo-sg-1` (allows port 80 and HTTP traffic)
     - Network Mapping: Use the available network zones in the VPC
     - Listener and Routing: Allow HTTP port 80 and connect to `my-alb-demo-tg` on the target group


![LB SUMMARY](./img/ld%20b.png)




> > The load balancer was created successfully and is in an active state.


![ldb](./img/ld%20balancer%20created%20.png)




### Testing the Load Balancer

1. **Copy the DNS Name:**

   - i Copy the DNS name of the load balancer and paste it into a web browser to confirm it is working properly.

![dns](./img/dns.png)

 - I refreshed the page, the IP address  change to another host, indicating that traffic is being routed between the two instances.


**Simulate an Instance Failure:**
   - If something goes wrong with the first instance, you can simulate this by stopping one of the instances:


![instant](./img/instant%20stop.png)



- i refresh the page and notice that one instance has stopped working while the other is still running:


![instant](./img/instant%20stop%20n2.png)



- I procced to the target group and choose the demo target group, it show that one instance is healthy and the other is unused. This indicates the result of stopping the instance. Return to the load balancer and refresh the page to see that only one instance is hosting:

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
   - I Navigate to the new tab where you have the launch template.
   - I Choose a name for my template
 (`my-new-asg-lt`).


   - In the quick start section i choose the AWS Management Console. This will provide me with a pre-configured AWS Machine to launch instances.
   - For instance type, i choose  `t2.micro`.



   - I Proceed to create a new key pair (`my-new-key`) and attach it to my public subnet that allows access to traffic flow on my web browser.

     ![template](./img/lunch%20template%201.png)
     ![template 2](./img/lunch%20template%202.png)





4. **Auto Scaling Template Creation:**
   - The Auto Scaling template is successfully created. I return to the Auto Scaling Group console and proceed.

     ![template](./img/template%20succesfully%20created%20.png)



5. **Create the Auto Scaling Group:**
   - During the process of creating the Auto Scaling group, i provide a name for my Auto Scaling group (`New-asg`).


   - I launch with the template i  already created (`my-new-asg-lt`)

     ![auto](./img/auto%20scsling%2011.png)



   - I attach it to my VPC and allow all available networks.

   - I attach both subnets that allow HTTP PORT-80.

     ![auto](./img/auto%20scalling12.png)

6. **Set Desired Capacity:**
   - I choose 1 for Min desired capacity and 4 for Max desired capacity.


     ![auto](./img/auto%20scaling%2014.png)




7. **Auto Scaling Group Creation:**
   - The Auto Scaling group is successfully created.

     ![auto](./img/auto%20scaling%20succ.png)



8. **Instance Creation:**
   - The Auto Scaling Group has successfully created instances according to the desired capacity specified, which in this case is 2.

     ![auto](./img/auto%20management.png)



9. **Verify Load Balancer:**
   - I navigate to the Load Balancer on the EC2 page and notice that the load balancer has also been created.

     ![load balancer](./img/load%20balance%20for%20auto.png)





## Project Reflection

- Explored the significance of high availability and scalability in cloud infrastructure.
- Understood the concept of Auto Scaling groups and how they dynamically adjust the number of instances based on workload.




















