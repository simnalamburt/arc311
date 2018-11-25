# ARC 311 - Introduction

The goal of this workshop is to show you the AWS networking technologies that allow you to **connect multiple accounts, Virtual Private Clouds (VPC) and applications together**.  This includes networking within the same region as well as cross region.  After this workshop, you should have an understanding of **Private Link, Endpoint Services, VPC Peering** and when to choose what service as well as your options when considering multi-region architectures.

# Prerequisites

* An AWS account set up with admin privilages (root account or IAM user with Admin policy attached).  **Do not share accounts as you will likely hit VPC limits if multiple people are deploying in the same account.**
* No other tools are needed.  Will be using a Cloud9 Instance in a VPC 

### [Click here to get started!](https://github.com/vaderlia/arc311/tree/master/Lab1)


# Modules

Each module will build on the previous module.  It is important that you complete the modules in order.  We will start out in the same region connecting one VPC to a containerized application in another VPC.  From there, we will add S3 Gateway Endpoints and then move into multi-region architecture.  We will deploy a copy of the same containerized application cross region and use VPC peering to create routes between VPCs.


**Module 1:  [Connect Applications via Private Link](https://github.com/vaderlia/arc311/tree/master/Lab1)**

**Module 2:  [Add S3 Gateway Endpoint](https://github.com/vaderlia/arc311/tree/master/Lab2)**

**Module 3:  [Cross Region VPC Peering](https://github.com/vaderlia/arc311/tree/master/Lab3)**

**Module 4:  [Optional: Analyze Traffic Using VPC Flow Logs with Athena](https://github.com/vaderlia/arc311/tree/master/Lab4)**

