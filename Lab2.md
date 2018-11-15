#Lab 2:  Using VPC Gateway Endpoints

As we discussed in the lecture, there are interface endpoints and gateway VPC endpoints.  Both endpoints allow you to connect to services using private IP ranges, but the Gateway Endpoints are actually specified in your route table instead of creating an ENI in your VPC.  We support **S3** and **DyanmoDB** Gateway Endpoints.

In additon to being able to route traffic to S3 and DynamoDB via private IPs, Gateway endpoints also prevent the traffic from going thrugh your NAT Gateway or Interenet Gateway.  *There is no data processing or hourly charges for using Gateway Type VPC endpoints*, so these endpoints should be considered for any architecture as a part of your cost optimization.

#### Let's configure a Gateway Endpoint for S3 


1.  Open the VPC console.  From the left hand navigation pane, select **Endpoints**.  

2.  Click **Create Endpoint** at the top of the page.  This will open the **Create Endpoint** workflow.

3.  Make sure that the **AWS services** radio buttion is selected for *Service Category* and select **S3** in the *Service Name* pane.

4. Click in the VPC drop down and select vpc2 (10.200.0.0/16).

5.  Below the **VPC** drop down, select all route tables to add the S3 Gatway Endpoint route to.

6.  Leave the Policy at *Full Access*, but in production, you can restrict access if you choose to.

7.  Click **Create Endpoint**

8.  Once created, select the endpoint to view the details, route tables, and the policy.  Note that from the Actions menu, you can manage the route tables and the policy.