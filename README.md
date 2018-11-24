# ARC 311 - Introduction

The goal of this workshop is to show you the AWS networking technologies that allow to **connect multiple accounts, Virtual Private Clouds (VPC) and applications together**.  This includes networking within the same region as well as cross region.  After this workshop, you should hav an understanding of **Private Link, Endpoint Services, VPC Peering** and when to choose what service as well as your options when considering multi-region architectures.

# Prerequisites

Provide a list of prerequisites that are required to successfully complete your workshop. This should include setting up an AWS account (note if you support multiple students sharing a single account), installing and configuring the CLI, and setting up any other tools students may need. Additionally, if there are specific skills or technologies students need to have existing knowledge of, you should list those here.

* An AWS account set up with admin privilages (root account or IAM user with Admin policy attached).  **Do not share accounts as you will likely hit VPC limits if multiple people are deploying in the same account.**
* No other tools are needed.  Will be using a Cloud9 Instance in a VPC 


# Modules

Each module will build on the previous module.  It is important that you complete the modules in order.  We will start out in the same region connecting our VPC to a containerized application in another VPC.  From there, we will add S3 Gateway Endpoints and then move into multi-region architecture.  We will deploy a copy of the same containerized application cross region and use VPC peering to create multple routes between VPCs.


**Module 1:  Connect Applications via Private Link**

**Module 2:  S3 Gateway Endpoint**

**Module 3:  Cross Region VPC Peering**

**Module 4:  VPC Flow Logs with Athena**

