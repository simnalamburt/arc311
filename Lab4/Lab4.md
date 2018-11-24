## Lab 4:  Query VPC Flow Logs with Athena

1.  From the Management Console, choose the **Athena** service under *Analytics*.
2. On the left hand side, choose **default** as the database
3. Paste the following in to the New Query

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

4.  Now the table is create, let's create the partiitons.  Click the `+` to open a new query tab.  Paste in:

	```sql
	
	ALTER TABLE vpc_flow_logs
	ADD PARTITION (dt='YYYY-MM-dd')
	location 's3://your_log_bucket/prefix/AWSLogs/{account_id}/vpcflowlogs/{region_code}/YYYY/MM/dd';
	```
	> It is very important to include the `YY/MM/dd` because this is how it is partitioned in S3. 

5.  
 