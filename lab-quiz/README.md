# CloudFormation Quiz

### 1. Create a VPC.

VPC Architecture:
![vpc-arc](images/create-a-vpc.jpg)

**Input Requirements** (15'):
+ Create 1 VPC across 2 availibility zones. Each AZ has 1 public subnet and 1 private subnet
+ Create 1 EIP in each AZ
+ Create 1 NAT Gateway in each AZ
+ Create 1 Internet Gateway
+ Set IGW as public subnet default gateway, and NAT Gateway as private subnet default gateway

**Bonus 1** (5'):
+ Use parameter for VPC and Subnet CIDR input

**Bonus 2** (5'):
+ Enable VPC Flowlog, and send log to cloudwatch log group

**Bonus 3** (5'):
+ Enable S3 VPC endpoin

### 2. Create an empty ECS cluster.

Below is the resource defination for ECS cluster with container sights enabled:

```yaml
ECSCluster:
  Type: 'AWS::ECS::Cluster'
  Properties:
    ClusterName: MyCluster
    ClusterSettings:
      - Name: containerInsights
        Value: enabled
```

More info for the resource defination in CloudFormation, please check [here](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-ecs-cluster.html)

**Input Requirements** (20'):
+ Allow to specify the cluster name
+ Allow to specify the status of Container Insights for the ECS cluster

**Output Requirements** (10'):
+ Output the ARN of the ECS cluster

**Bonus 1** (10'):
+ Create [stack policy](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/protect-stack-resources.html) for the stack to prevent further updates to the ECS cluster

**Bonus 2** (10'):
+ Use [nested stack](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/using-cfn-nested-stacks.html) to spin up the ECS cluster. (Create a root stack on top of the ECS cluster stack.)
+ Output the ARN of the ECS cluster

**Bonus 3** (10'):
+ Export the ARN of the ECS cluster, the name of the export variable is `myECSArn`

### 3. Create a SNS topic to subscript the events for a cloudformation stack

**Bonus 1** (15'):
+ A SNS topic and email subscription are created in one cloudformation stack

**Bonus 2** (15')
+ A S3 bucket is created in another cloudformation stack

**Bonus 3** (20')
+ The SNS topic created above is able to publish **S3** stack related events to your email, please refer to [here](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-stack.html#aws-properties-stack-properties) for the configuration.
+ No hardcode configuration on the SNS topic config
