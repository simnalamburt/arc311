## Lab 4:  Query VPC Flow Logs with Athena

Amazon Athena is an interactive query service that makes it easy to analyze data in Amazon S3 using standard SQL. Athena is serverless, so there is no infrastructure to manage, and you pay only for the queries that you run.  This can be used as an analytics tool, but it can also be helpful to do analysis on your service logs such as VPC flow logs.

If you recall, we enabled VPC flow logs in Lab 1.  We can now query these logs using the Athena service.

1.  In your primary region (with the ARC311 stack), from the Management Console, choose the **Athena** service under *Analytics*.
2. Click **Get Started** .
3. In the **New Query** pane, run the following to create a *database*.
	`CREATE DATABASE awslogs;`
4. Click **Run Query**.
5. From the left-hand pane, click the **Database** drop down and select your new `awslogs` database.
6. Click the `+` tab to open a new query and paste the following in to the New Query.  You will need to update the location on **Line 20** with you **S3 Bucket** and path.  If you are unsure of the account ID and region code, you can browse to the S3 console, click on your bucket and follow to path.  

	```sql
	CREATE EXTERNAL TABLE IF NOT EXISTS vpc_flow_logs (
	  version int,
	  account string,
	  interfaceid string,
	  sourceaddress string,
	  destinationaddress string,
	  sourceport int,
	  destinationport int,
	  protocol int,
	  numpackets int,
	  numbytes bigint,
	  starttime int,
	  endtime int,
	  action string,
	  logstatus string
	)  
	PARTITIONED BY (dt string)
	ROW FORMAT DELIMITED
	FIELDS TERMINATED BY ' '
	LOCATION 's3://REPLACE-WITH-YOUR-BUCKET-NAME/prefix/AWSLogs/REPLACE-WITH-YOUR-ACCOUNT-ID/vpcflowlogs/YOUR-REGION-CODE/'
	TBLPROPERTIES ("skip.header.line.count"="1");
	
	```

7.  Now the table is create, let's create the partiitons.  Click the `+` to open a new query tab.  Paste in the following and update`YY/MM/dd` with the proper dates (ex. `2018-11-26`)


	```sql
	
	ALTER TABLE vpc_flow_logs
	ADD PARTITION (dt='YYYY-MM-dd')
	location 's3://your_log_bucket/prefix/AWSLogs/{account_id}/vpcflowlogs/{region_code}/YYYY/MM/dd';
	```


8.  Open a new query tab and paste the following to aggregate all the REJECT action.

	```sql
	SELECT sourceaddress, count(*) cnt
	FROM vpc_flow_logs
	WHERE action = 'REJECT'
	GROUP BY sourceaddress
	ORDER BY cnt desc
	LIMIT 25;
	``` 
9.  Run the following to see all requests to you PrivateLink endpoint address.  Be sure to replace with the proper address that was returned when you performed a `dig +short` against the DNS name of your VPC endpoint.

	```sql
	SELECT day_of_week(from_iso8601_timestamp(dt)) AS
	  day,
	  dt,
	  interfaceid,
	  sourceaddress,
	  sourceport, 
	  destinationaddress, 
	  destinationport, 
	  action,
	  protocol
	FROM vpc_flow_logs
	WHERE destinationaddress = '10.200.0.31'
	LIMIT 100;
	```
10.  Feel free to play around with the queries and write you own to analyze your flow log data!


#### You have now completed all the modules in this workshop!  Thank you! 

##Clean-up
In this lab, we built quite a few resources on top of our CloudFormation stacks that we need to delete first.  Make sure you perform the following in order!

1.  First, you need to empty your ***S3 Bucket***
2. From the Cloud9 IDE, run the following to force delete:

	`aws s3 rb s3://MY-BUCKET-NAME --force`

3.  In the primary region (ARC311 stack is deployed here), delete your peering connection.
4. In the same region, delete the ***Endpoints***, both the *Interface* and the *Gateway* endpoints.
5. In the same region. delete the ***Endpoint Service***.
6. In the ***ECS console***, select the ARC311 cluster, select the `new-website-service` and delete.  Do the same for the `new-product-service`.
7. From the ***EC2 console***, delete the Network Load Balancer you created earlier.
8. From the ***CloudFormation*** console, select the parent **ARC311** stack and choose delete.
9. Switch regions to the **Cross Region** and delete the CrossRegion Cloudformation stack.