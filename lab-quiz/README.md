# CloudFormation Quiz

###  Create an empty ECS cluster.

**Input Requirements** (20'):
+ Allow to specify the cluster name
+ Allow to specify the status of Container Insights for the ECS cluster

**Output Requirements** (10'):
+ Output the arn of the ECS cluster

**Other requirements** (10'):
+ Prevent further updates to the ECS cluster

**Bonus** (10'):
+ Use [nested stack](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/using-cfn-nested-stacks.html) to spin up the ECS cluster. (Create a root stack on top of the ECS cluster stack.)
