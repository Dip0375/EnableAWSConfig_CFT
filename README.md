**AWS Config CloudFormation Template**
This project provides a CloudFormation template to enable AWS Config with customizable parameters for configuration recording, delivery channels, and notifications. The template creates necessary resources such as S3 buckets, SNS topics, and IAM roles to manage AWS Config operations.

This CloudFormation template sets up AWS Config, which continuously monitors and records your AWS resources and provides you with history, audit, and compliance details. The template:

Configures a recorder to capture resource changes.
Sets up an S3 bucket for storing configuration snapshots.
Optionally creates an SNS topic for notifications.
Provides flexibility in terms of which resources to track and how frequently.
Template Structure
Parameter Groups: Organizes inputs for the user (Recorder, Delivery Channel, and Notification configurations).
Mappings: Converts user-defined frequencies into AWS Config’s internal format.
Resources: Creates required components like S3 buckets, IAM roles, and SNS topics.
Conditions: Dynamically controls the creation of optional resources based on input parameters.

**Conditions**
IsAllSupported: True if all resources are tracked.
CreateTopic: True if a new SNS topic is to be created.
CreateSubscription: True if email notifications are enabled.
CreateConfigSLR: True if a service-linked role must be created in the region.

**Resources**
S3 Bucket: Stores AWS Config snapshots.
SNS Topic: Optional topic for notifications.
IAM Role: Service-linked role for AWS Config.
Configuration Recorder: Captures resource changes.
Delivery Channel: Sends snapshots to the S3 bucket.
Bucket Policy: Allows AWS Config to access the bucket.
SNS Subscription: Sends notifications to an email address.

**Deployment Steps**

Clone the Repository:
git clone https://github.com/your-repository/aws-config-template.git
cd aws-config-template


Deploy the CloudFormation Stack:

aws cloudformation deploy \
  --template-file template.yaml \
  --stack-name aws-config-stack \
  --parameter-overrides \
    AllSupported=True \
    IncludeGlobalResourceTypes=False \
    RecordingFrequency=DAILY \
    Frequency=24hours \
    ServiceLinkedRoleRegion=<YourRegion> \
  --capabilities CAPABILITY_NAMED_IAM


Verify the Stack Status:
aws cloudformation describe-stacks --stack-name aws-config-stack
