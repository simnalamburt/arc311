# Lab 1:

In this section you will launch a CloudFormation stack that will create Amazon Virtual Private Cloud (VPC)s environment, an application running in ECS and a Cloud9 IDE Instance that you will use in the rest of the workshop.

Cloud9 is only used in this case to avoid requiring participants from having to install the AWS CLI or use tools like curl directly from their laptop.

## Step-by-step Instructions

1. Go the AWS Management Console, click Services then select CloudFormation under Management Tools.

2. In the CloudFormation console, click Create stack and in Step 1, choose S3 Link and paste :
You can launch this CloudFormation stack in your account:

| AWS Region | Short name | | 
| -- | -- | -- |
| US East (Ohio) | us-east-2 | [![cloudformation-launch-button](images/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=us-east-2#/stacks/new?stackName=ARC311&templateURL=https://s3-us-west-2.amazonaws.com/arc311-region1-cloudformation/master.yaml) |
| US East (N. Virginia) | us-east-1 | [![cloudformation-launch-button](images/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/new?stackName=ARC311&templateURL=https://s3-us-west-2.amazonaws.com/arc311-region1-cloudformation/master.yaml) |
| US West (Oregon) | us-west-2 | [![cloudformation-launch-button](images/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=us-west-2#/stacks/new?stackName=ARC311&templateURL=https://s3-us-west-2.amazonaws.com/arc311-region1-cloudformation/master.yaml) |
| US West (N. California) | us-west-1 | [![cloudformation-launch-button](images/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=us-west-1#/stacks/new?stackName=ARC311&templateURL=https://s3-us-west-2.amazonaws.com/arc311-region1-cloudformation/master.yaml) |
| Canada (Central) | ca-central-1 | [![cloudformation-launch-button](images/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=ca-central-1#/stacks/new?stackName=ARC311&templateURL=https://s3-us-west-2.amazonaws.com/arc311-region1-cloudformation/master.yaml) |
| EU (Paris) | eu-west-3 | [![cloudformation-launch-button](images/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=eu-west-3#/stacks/new?stackName=ARC311&templateURL=https://s3-us-west-2.amazonaws.com/arc311-region1-cloudformation/master.yaml) |
| EU (London) | eu-west-2 | [![cloudformation-launch-button](images/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=eu-west-2#/stacks/new?stackName=ARC311&templateURL=https://s3-us-west-2.amazonaws.com/arc311-region1-cloudformation/master.yaml) |
| EU (Ireland) | eu-west-1 | [![cloudformation-launch-button](images/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=eu-west-1#/stacks/new?stackName=ARC311&templateURL=https://s3-us-west-2.amazonaws.com/arc311-region1-cloudformation/master.yaml) |
| EU (Frankfurt) | eu-central-1 | [![cloudformation-launch-button](images/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=eu-central-1#/stacks/new?stackName=ARC311&templateURL=https://s3-us-west-2.amazonaws.com/arc311-region1-cloudformation/master.yaml) |
| Asia Pacific (Seoul) | ap-northeast-2 | [![cloudformation-launch-button](images/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=ap-northeast-2#/stacks/new?stackName=ARC311&templateURL=https://s3-us-west-2.amazonaws.com/arc311-region1-cloudformation/master.yaml) |
| Asia Pacific (Tokyo) | ap-northeast-1 | [![cloudformation-launch-button](images/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=ap-northeast-1#/stacks/new?stackName=ARC311&templateURL=https://s3-us-west-2.amazonaws.com/arc311-region1-cloudformation/master.yaml) |
| Asia Pacific (Sydney) | ap-southeast-2 | [![cloudformation-launch-button](images/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=ap-southeast-2#/stacks/new?stackName=ARC311&templateURL=https://s3-us-west-2.amazonaws.com/arc311-region1-cloudformation/master.yaml) |
| Asia Pacific (Singapore) | ap-southeast-1 | [![cloudformation-launch-button](images/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=ap-southeast-1#/stacks/new?stackName=ARC311&templateURL=https://s3-us-west-2.amazonaws.com/arc311-region1-cloudformation/master.yaml) |
| Asia Pacific (Mumbai) | ap-south-1 |  [![cloudformation-launch-button](images/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=ap-south-1#/stacks/new?stackName=ARC311&templateURL=https://s3-us-west-2.amazonaws.com/arc311-region1-cloudformation/master.yaml) |
| South America (São Paulo) | sa-east-1 |  [![cloudformation-launch-button](images/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=sa-east-1#/stacks/new?stackName=ARC311&templateURL=https://s3-us-west-2.amazonaws.com/arc311-region1-cloudformation/master.yaml) |

3. On the next screen, Step 2, enter a Stack name such as VPC-Cloud9-<YOUR INITIALS> and click Next

4. On the Configure Stack Options page, accept all the defaults and click Next. Finally on the Review page, click Create stack.
It will take a few minutes for the Stack to create. Wait until the stack is fully launched and shows a Status of CREATE_COMPLETE.

5. Open the VPC console and from the right hand pane, click VPCs.  You should see 2 VPCs created by Cloudformatin as well as the default VPC.

6. Select VPC A.  This VPC has your application running in it.  This is a containerized application that ECS is managing.  Click on the Route table.

> You will notice that the route table has a 0.0.0.0/0 route to the Internet gateway and a local route for the VPC.  Other than that, there are no other routes.  This is important to note because our Cloud9 instance is running in VPC B.  If we want to route from Cloud9 to the our application over private IPs, we will not be able to.  Let's test this.

7. From the Cloudformation Console, thick on your stack.  When the stack creation is complete, click the Outputs tab for the stack and select the value for Cloud9 IDE. Open that URL in a new browser tab to load your IDE environment.

8. In the lower pane, you will have a terminal that looks like the below.  From the Cloudformation outputs tab, copy the private dns name for the application and attempt to curl.


```
curl myprivateapp
```


> This should fail.  To allow our Cloud9 instance to connect to our application, we could use VPC peering to route between the 2 VPCs, but in our case we want to use private link.  PrivateLink will allow us to whitelist the consumers of the service by account, IAM user or IAM role and it also does not add a route in the route table.  Route tables can have up to a total of 100 routes and at the scale of this workshop, that is fine.  However, when we scale our services and have more than 100 VPCs that need to connect to our service over private IP space, Private Link becomes a better option for us.

9. Let's set up Private link so that our Cloud9 instance or perhaps another microservice in our VPC B can connect.  First, we need to create an endpoint service in VPC A for our application.  Open the EC2 console at https://console.aws.amazon.com/ec2/

10. From the left hand pane, choose Load Balancers.

11. Click on the Create Load Balancer button

        You will see 3 options of load balancers.  We will need to use the Layer 4 load balancer which is the Network Load Balancer.  Find the Network Load Balancer in the middle and select Create.

12. Give your load balancer a name link PrivateLink-<MYINITIALS>.  Select VPC-A Public subnet.  Leave the rest of the options at the defaults.

13. Click Next Configure Routing.  Select the target group for our application.
[finish rest of the load balancer]

14. Open the Amazon VPC console at https://console.aws.amazon.com/vpc/.  In the navigation pane, choose Endpoint Services, Create Endpoint Service.

15. For Associate Network Load Balancers, select the Network Load Balancers to associate with the endpoint service.

16. For Require acceptance for endpoint, select the check box to accept connection requests to your service manually. If you do not select this option, endpoint connections are automatically accepted.

17. Choose Create service.

18. After you've created your endpoint service configuration, you can control which service consumers can create an interface endpoint to connect to your service. Service consumers are IAM principals—IAM users, IAM roles, and AWS accounts.

19. You should still be in the VPC console.  In the navigation pane, choose Endpoint Services and select your endpoint service.

20. Choose Actions, Add principals to whitelist.  Specify * to add permissions for all principals.  NOTE:  this is not following the least privilage security model and we are only doing this for the purpose of this lab.  We suggest you whitelist the appropriate accounts, IAM roles and users.

21. Choose Add to Whitelisted principals.



22. Now we have a service, but we need to create an interface endpoint in VPC B

23. To create an interface endpoint to an endpoint service, open the Amazon VPC console at https://console.aws.amazon.com/vpc/.

24. In the navigation pane, choose Endpoints, Create Endpoint.

25. For Service category, choose Find service by name.

26. For Service Name, enter the name of the service (for example, com.amazonaws.vpce.us-east-1.vpce-svc-0e123abc123198abc) and choose Verify.

27. Complete the following information and then choose Create endpoint.

28. For VPC, select a VPC in which to create the endpoint.

29. For Subnets, select the subnets (Availability Zones) in which to create the endpoint network interfaces.

30. For Security group, select the security groups to associate with the endpoint network interfaces.

> Now we need to accept the interface endpoint. After you've created an endpoint service, service consumers for which you've added permission can create an interface endpoint to connect to your service.

> We have specified that acceptance is required for connection requests, therefore you must make a API call or use the console to accept or reject interface endpoint connection requests to your endpoint service. After an interface endpoint is accepted, it becomes available.


31. Open the Amazon VPC console

32. In the navigation pane, choose Endpoint Services and select your endpoint service.

33. The Endpoint Connections tab lists endpoint connections that are currently pending your approval. Select the endpoint, choose Actions, and choose Accept.

34. Copy the DNS name from your endpoint service.

35. Now we can test our service again!  From the Cloud9 IDE, open that URL in a new browser tab to load your IDE environment.  We will use curl against the DNS name of our endpoint service.

curl myprivateapp
