# Lab 3:  Cross Region VPC Peering

So far, we have connected our VPC where our Cloud9 instance runs to our application running in a different VPC.  This works for scenarios where you need a VPC to connect to a specific service in a different VPC or account. 

This may not meet every use case as sometimes you may need to route between 2 networks (VPCs).  VPC peering is simply a route between 2 VPCs.  Once you create a peering connection, you will see these routes in your route table.  You can create a peering connection between 2 VPCs in a region or across regions.

Additionally, PrivateLink does not support cross region, therefore if you do have an application or service that needs to replicate cross region or make an API call cross region, you may want to consider Cross Region VPC Peering.  

> One note, be very careful with your design if you do have applications that communicate cross region.  It is important that if one region fails, that your application is not reliant on the resource in the secondary region.  Therefore, use cases like replicating databases and other data are better use cases for cross region vpc peering.
> 
> Use caution when designing systems that have a service that makes a call to another service in a different region!  This pattern should be avoided unless you have a solution for when the cross region API call fails.

#### Create Cross Region Environment

We have VPC 1 and VPC 2 in one region.  **It is time to take this multi-region!**  

2. Let's start by running a *CloudFormation template* to spin up a VPC3 in a *different region* (i.e. if VPC 1 and 2 are in us-west-2, pick us-east-1).  You will follow the same steps from before in the Cloudformation console.  **Make sure you are in a different region!**

> This may take a few minutes.  Once complete, finish below.

You can launch this CloudFormation stack in your account:

Region| Launch
------|-----
| US East (Ohio) - us-east-2 | [![cloudformation-launch-button](images/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=us-east-2#/stacks/new?stackName=CrossRegion&templateURL=https://s3.amazonaws.com/arc311-crossregion/master.yaml) |
| US East (N. Virginia) - us-east-1 | [![cloudformation-launch-button](images/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/new?stackName=CrossRegion&templateURL=https://s3.amazonaws.com/arc311-crossregion/master.yaml) |
| US West (Oregon) - us-west-2 | [![cloudformation-launch-button](images/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=us-west-2#/stacks/new?stackName=CrossRegion&templateURL=https://s3.amazonaws.com/arc311-crossregion/master.yaml) |

2.  This Cloudformation template spun up another VPC with the same containerized applications running in ECS and behind a ALB.  

3.  We need to set up a peering connection between VPC2 and our new VPC in another region.  We can also set up a "mesh" to connect each of the VPCs together.  This way, clients in VPC 1 can route to destinations in VPC2 and VPC3.

#### Inter Region Peering

4.  From the VPC console, select **Peering Connections** on the left hand side. Next, click on **Create Peering Connection**

5.  Give your peering connection a tag like **VPC1 peer to VPC2**

6.  Select VPC1 (10.100.0.0/16) as the VPC requestor.  

7.  Select VPC2 (10.200.0.0/16) as the VPC to peer with.  Click **Create Peering Connection**

8.  The peering connection should be in a status of *Pending Acceptance*.  Click on the **Actions** Drop down and click **Accept Request**.

9. Now we have peering set up!  However, you still need to add a route in your route table.  You can do this by clicking on Route Tables in the left hand pane and altering your route tables for VPC1 and VPC2.


####  Cross Region VPC Peering

10.  From the VPC console, select **Peering Connections** on the left hand side. Next, click on **Create Peering Connection**

11.  Give your peering connection a tag like **VPC2 peer to VPC3**

12.  Select VPC2 (10.200.0.0/16) as the VPC requestor.  

13.  Select VPC3 (Cross Region) as the VPC to peer with.  

14. Click the *Other Region* radio button, select your other region and the cross region VPC.  Click **Create Peering Connection**

15.  The peering connection should be in a status of *Pending Acceptance*.  Click on the **Actions** Drop down and click **Accept Request**.

16. Now we have peering set up!  However, you still need to add a route in your route table.  You can do this by clicking on Route Tables in the left hand pane and altering your route tables for each of the VPCs.


