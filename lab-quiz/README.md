# CloudFormation Quiz

###1. Create an empty ECS cluster.

**Input Requirements** (20'):
+ Allow to specify the cluster name
+ Allow to specify the status of Container Insights for the ECS cluster

**Output Requirements** (10'):
+ Output the arn of the ECS cluster

**Bonus 1** (10'):
+ Prevent further updates to the ECS cluster

**Bonus 2** (10'):
+ Use [nested stack](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/using-cfn-nested-stacks.html) to spin up the ECS cluster. (Create a root stack on top of the ECS cluster stack.)
+ Output the Amazon Resource Name (ARN)

###2. Create a SNS topic to subscript the events for a cloudformation stack creating a S3 bucket

**Bonus 1** (15'):
+ A SNS topic and email subscription are created in one cloudformation stack

**Bonus 2** (15')
+ A S3 bucket is created in another cloudformation stack

**Bonus 3** (20')
+ The SNS topic created above is able to publish **S3** stack related events to your email, please refer to [here](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-stack.html#aws-properties-stack-properties) for the configuration.
+ No hardcode configuration on the SNS topic config
