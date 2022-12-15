# CLI-Commands
Steps to get the Amazon AWS access key ID and secret key
1. Go to the IAM Console and click on Users.
2. Click on the User that you want to create the access key for.
Click on the actual row and not the check box.
3. On the next screen, click on “Create Access Key”. If you have
created keys before you should be able to see them (but
can’t download them again)
4. You will see a popup that allows you to download the access
ID and key. The keys can be downloaded only once so make
sure you save it in a safe place. You can, however, create
another key later on.
5. The downloaded CSV has both the access id and key.


Configure Amazon CLI (Command Line Interface)

1. Type in “aws configure” on the command line.
2. Enter the Access ID, key and the default region.
3. That configures the CLI. This creates a directory called .aws in
home. This directory has the credentials and the config file.
4. To test the configuration we will create a security group and
then delete it from the AWS console. To create the security
group type in



Procedure :
We will add four total rules. So go ahead and add three other rules. Set the
types for all of the rules to:
 SSH
 MySQL/Aurora
 HTTP
 HTTPS
If you’re on Windows, download the latest version of PuTTY to save yourself
some time and heartache. If you’re using MacOS, you’re more than welcome
to follow along, but you can SSH into your instance from the native command
line.



AIM: To create a static website on Amazon S3 using AWS system manager.

PROCEDURE:
1) Sign in to the AWS Management Console and click on Amazon S3 Console at
https://console.aws.amazon.com/s3/ .
2) Click on create a bucket.
3) Enter the name of the bucket and the region you want to create it in
4) Accept the default settings and then click on create a bucket age.
5) In the buckets list, click on the bucket you just created and choose properties,
then under static website hosting click the enable option.
6) Then click on the upload option after selecting your bucket and upload your
project files(index.html, style.css,main.js). Also, make sure that the project files
you will upload have proper names as they are case-sensitive.

7) After configuring the website, you can use the endpoint to test the website out.
8) choose the name of the bucket you just configured and then choose
permissions under that block public access will be visible, click on the edit option
and save the changes.

9) under the bucket permissions there will be a bucket policy, click on that and
paste this code into the bucket policy editor:
{
"Version": "2012-10-17",
"Statement": [
{
"Sid": "PublicReadGetObject",
"Effect": "Allow",
"Principal": "*",
"Action": [ "s3:GetObject"],
"Resource": [ "arn:aws:s3:::myawss3bucket1/*"
]
}
]
}

10) Click on save changes




Aim: Querying Data in S3 with Amazon Athena
Step 1:
Go to buckets and create two buckets.

Step 2 :
After clicking onto the bucket add files to it.

Step 3 :

Now go to Amazon athena.

Step 4 :
Select AwsDataCatalog in the left side which is present in the data source
tab.

Step 5 :
After that go to settings and specify an output path.

Step 6:
Click on connect data source.

Step 7:
After clicking choose a query in amazon s3 and Aws glue data catalog.

Step 8:
Click on next and select setup a crawler in AWS glue to retrieve
schema information automatically.

Step 9:
After selecting that it will redirect to a new page and add crawler and follow
below steps to add a new crawler after setting up click on finish.

Step 10:
Crawler is successfully created and now click on the crawler and click run
crawler.

Step 11:
After running the crawler go back to athena you will see a table created on
table column select that and click on preview table.

Step 12:
Now the query can be executed.

Result :
Querying Data in S3 with Amazon Athena is done and output is verified.


Aim : Automate Sending Emails at a Specific Time with AWS Lambda,
CloudWatch and SES

Pre-requisites : AWS Console, Amazon SES, Amazon Lambda, Amazon
CloudWatch.

Procedure :
We are going automate sending email to a person or a group of people. AWS
Cloudwatch is used to setup a schedule to trigger AWS Lambda function and
then its going to use AWS SES (Simple Email Service) to send out emails to
people.
Steps:
1. Go to AWS SES (Simple email service), click on “Create Identity”.
Use email address as a type and type the email address.

2. Verify the email address that revieved an email from aws to tell you to
verify that.

3. Create two identities (email address).
One for sending emails and another for receiving.
4. Create an IAM role.
Give Use case as lambda and give full access to cloudwatch, SES.

5. Go to Lambda Service, create a lambda function.
Give name, runtime as NodeJS, execution role as created IAM role
previously.

6. Use this template for the code:

1)
2) var aws = require("aws-sdk");
3) var ses = new aws.SES({ region: "us-west-2" });
4) exports.handler = async function (event) {
5) var params = {
6) Destination: {
7) ToAddresses: ["RecipientEmailAddress"],

8) },
9) Message: {
10) Body: {
11) Text: { Data: "Test" },
12) },
13)
14) Subject: { Data: "Test Email" },
15) },
16) Source: "SourceEmailAddress",
17) };
18)
19) return ses.sendEmail(params).promise()
20) };

7. Click on Deploy and then TEST, you wil receive the message in your
mentioned emails.

8. For scheduled daily report, go to AWS Cloudwatch , navigate to rule
section (now called as eventBridge).

9. Create rule- give name, ruletype- schedule, use cron expression for
schedule pattern .
For e.g. : 15 19 * * ? *

10.Select Targets as lambda function, and use the above defined function.
11.Go to monitoring in Lambda service, click on View logs in cloudWatch
and check your mail inbox .

Result:
Hence, the lambda function is created and also implemented using SES,
CloudWatch to schedule daily reports.
