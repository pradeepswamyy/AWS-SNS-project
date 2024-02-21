

# SNS NOTIFICATION ON S3 EVENTS

## Project Overview

This project demonstrates the setup of Amazon Simple Notification Service (SNS) to receive email notifications upon events in an Amazon S3 bucket. The end-to-end event-driven communication involves creating an SNS topic, setting up a subscription for email alerts, configuring S3 bucket event notifications, and testing the configuration.

## Steps

### Step 1: Create an SNS Topic

1. Navigate to the SNS service.
2. Click on "Topics" and then select "Create Topic."
3. Choose "Standard" as the topic type.
4. Provide a name of your choice.
5. Leave all other settings as default and scroll down.
6. Click on "Create Topic."

### Step 2: Create a Subscription

1. Click on "Create Subscription."
2. Choose the protocol as "Email."
3. Enter your email address as the endpoint.
4. Click on "Create."
5. Check your email inbox, refresh, and confirm the subscription.

### Step 3: Edit SNS Topic and Set Policy

1. Navigate back to your SNS topic.
2. Click on "Edit" and scroll down to the "Access Policy" section.
3. Replace the default policy with the provided example policy.
4. Replace the topic ARN with your topic ARN.
5. Replace the source ARN with the S3 bucket ARN.
6. Replace the source account with your account ID.
7. Click on "Save Changes."

#### Policy Example:
```json
{
  "Version": "2012-10-17",
  "Id": "example-ID",
  "Statement": [
    {
      "Sid": "Example SNS topic policy",
      "Effect": "Allow",
      "Principal": {
        "Service": "s3.amazonaws.com"
      },
      "Action": [
        "SNS:Publish"
      ],
      "Resource": "SNS-topic-ARN",
      "Condition": {
        "ArnLike": {
          "aws:SourceArn": "arn:aws:s3:*:*:bucket-name"
        },
        "StringEquals": {
          "aws:SourceAccount": "bucket-owner-account-id"
        }
      }
    }
  ]
}
```

### Step 4: Configure S3 Bucket Event Notification

1. Go back to your S3 bucket.
2. Go to properties and scroll down to "Event Notifications."
3. Select "Create Notification."
4. Provide a name for the event.
5. Choose "All object create events."
6. Select "SNS Topic" as the destination.
7. Choose your SNS topic for the SNS Topic field.
8. Click "Save."

### Step 5: Test the Configuration

1. Upload a test file to the S3 bucket.
2. Verify that you receive a notification.



