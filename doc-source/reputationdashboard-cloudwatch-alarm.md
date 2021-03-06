# Creating Reputation Monitoring Alarms Using CloudWatch<a name="reputationdashboard-cloudwatch-alarm"></a>

Amazon SES automatically publishes two reputation\-related metrics to Amazon CloudWatch: `Reputation.BounceRate` and `Reputation.ComplaintRate`\. You can use these metrics to create alarms that notify you when your bounce or complaint rates reach levels that could impact your ability to send email\.

The values of `Reputation.BounceRate` and `Reputation.ComplaintRate` are decimal numbers between 0 and 1\. Multiply either of these metrics by 100 to determine the percentage of your emails that are bouncing or resulting in complaints\.

**To create a CloudWatch alarm**

1. Sign in to the AWS Management Console and open the Amazon SNS console at [https://console\.aws\.amazon\.com/sns/v2/home](https://console.aws.amazon.com/sns/v2/home)\.

1. Create a new Amazon SNS topic, and then subscribe to it using your preferred endpoint \(such as email or SMS\)\. For more information, see [Create a Topic](https://docs.aws.amazon.com/sns/latest/dg/CreateTopic.html) and [Subscribe to a Topic](https://docs.aws.amazon.com/sns/latest/dg/SubscribeTopic.html) in the [Amazon Simple Notification Service Developer Guide](https://docs.aws.amazon.com/sns/latest/dg/)\.

1. Open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. In the navigation panel on the left side of the screen, choose **Alarms**\.

1. Choose **Create Alarm**\.

1. Under **CloudWatch Metrics by Category**, choose **SES Metrics**\.

1. Under **Metric name**, choose the metric for which you want to create the alarm\.

   For example, if you want to create an alarm when your bounce rate reaches a certain level, choose **Reputation\.BounceRate**\. If you want to create an alarm when your complaint rate reaches a certain level, choose **Reputation\.ComplaintRate**\.

   Choose **Next**\.
**Note**  
The reputation metrics might not appear in CloudWatch if your account hasn't had any bounces or complaints\. If you don't see the **Reputation\.BounceRate** or **Reputation\.ComplaintRate** metrics on this page, use the [Amazon SES mailbox simulator](mailbox-simulator.md) to simulate a bounce or complaint event\. After you simulate a bounce or complaint event, you might have to wait several minutes for the reputation metrics to appear in CloudWatch\.

1. Under **Alarm Threshold**, for **Name**, type a name for the alarm\.

1. In the alarm threshold area, specify the value that should cause CloudWatch to raise an alarm\.

   If you're creating an alarm to monitor your bounce rate, note that Amazon SES recommends that you maintain a bounce rate under 5%, and if your account's bounce rate is greater than 10%, we might automatically pause your account's ability to send email\. For this reason, you should configure CloudWatch to raise an alarm when the bounce rate is greater than or equal to 0\.05 \(5%\), as shown in the following image\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/ses/latest/DeveloperGuide/images/create_cloudwatch_alarm_bounce.png)

   If you're creating an alarm to monitor your complaint rate, note that Amazon SES recommends that you maintain a complaint rate under 0\.1%, and if your account's complaint rate is greater than 0\.5%, we might automatically pause your account's ability to send email\. For this reason, you should configure CloudWatch to raise an alarm when the bounce rate is greater than or equal to 0\.001 \(0\.1%\), as shown in the following image\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/ses/latest/DeveloperGuide/images/create_cloudwatch_alarm_complaint.png)

1. Under **Additional settings**, for **Treat missing data as**, choose **ignore \(maintain the alarm state\)**\.

1. Under **Alarm Preview**, for **Period**, choose an alarm period\.
**Note**  
Amazon SES sends `Reputation.BounceRate` and `Reputation.ComplaintRate` metrics to CloudWatch every 15 minutes\. For this reason, we recommend that you choose an alarm period of 15 minutes or greater\. You won't see any added benefit by choosing an alarm period of less than 15 minutes\.

1. Under **Actions**, for **Whenever this alarm**, choose **State is ALARM**\. For **Send notification to**, choose the topic that you created and subscribed to in step 2\. 

1. Choose **Create Alarm**\.

**Note**  
These procedures omit some information about optional settings for CloudWatch alarms\. For detailed instructions, see [Creating Amazon CloudWatch Alarms](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/AlarmThatSendsEmail.html) in the [Amazon CloudWatch User Guide](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/)\.