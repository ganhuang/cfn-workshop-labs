### Overview

When you need to make changes to a stack's settings or change its resources, you update the stack instead of deleting it and creating a new stack. For example, if you have a stack with a S3 bucket, you can update the stack to change the S3 versioning configuration.

### Topics Covered

By the end of this lab, you will be able to:

+ Update stack directly
+ Update stack using change sets

### Start Lab

#### 1. Create S3 bucket (dev)

1. Open the **[AWS CloudFormation](https://console.aws.amazon.com/cloudformation)** link in a new tab and log in to your AWS account.
1. Click on **Create stack** (_With new resources (Standard)_ if you have clicked in the top right corner).
1. In **Prepare template**, choose **Template is ready**.
1. In **Template source**, choose **Upload a template file**.
1. Click on **Choose file** button and navigate to your workshop directory.
1. Select the file `lab03-stack.yaml`.
1. Click **Next**.
1. Provide a **Stack name**: **cfn-workshop-003**.
    + The _Stack name_ identifies the stack. Use a name to help you distinguish the purpose of this stack.
    + Click **Next**.
1. Choose a **EnvironmentType**: **dev**.
1. You can leave **Configure stack options** default, click **Next**.
1. On the **Review <stack_name>** page, scroll down to the bottom and click on **Create stack**.
1. You can click the **refresh** button a few times until you see in the status **CREATE_COMPLETE**.
1. You can navigate to **Outputs** tab, you can see the **BucketName** which contains **dev** string.

#### 2. Update Stack directly by changing the bucket name (test)

1. Navigate to Cloudformation service in the AWS console.
1. Select the **cfn-workshop-003** stack.
1. In the top right corner click on **Update**.
1. In **Prepare template**, choose **Use current template**, click **Next**.
1. Choose the **EnvironmentType** parameter to **test**, click **Next**.
1. You can leave **Configure stack options** default, click **Next**.
1. On the **Review <stack_name>** page, scroll down to the bottom and click on **Update stack**.
1. You can click the **refresh** button a few times until you see in the status **UPDATE_COMPLETE**.
1. You can navigate to **Outputs** tab, you can see the **BucketName** which contains **test** string.

#### 3. Update stack using change sets (prod)

1. Navigate to Cloudformation service in the AWS console.
1. Select the **cfn-workshop-003** stack.
1. In the stack details pane, choose **Stack actions**, and then choose **Create change set for current stack**.
1. In **Prepare template**, choose **Use current template**, click **Next**.
1. Choose the **EnvironmentType** parameter to **prod**, click **Next**.
1. You can leave **Configure stack options** default, click **Next**.
1. On the **Review <stack_name>** page, scroll down to the bottom and click on **Create change set**. Specify a name for the change set and optionally specify a description of the change set to identify its purpose. Then, choose Create change set.

You're redirected to the Changes tab of the change set's details page. While CloudFormation generates the change set, the status of the change set is CREATE_IN_PROGRESS. After it has created the change set, CloudFormation sets the status to CREATE_COMPLETE. In the Changes section, CloudFormation lists all of the changes that it will make to your stack. Viewing change sets:

> From the change sets, we can notice that update the **EnvironmentType** would have to re-create the s3 bucket, that we need to pay attention to.

1. Navigate to Cloudformation service in the AWS console.
1. Choose and click the **cfn-workshop-003** stack.
1. In the navigation pane, choose **Change Sets** to view a list of the stack's change sets.
1. Choose the name of the change set that you want to view.

The CloudFormation console directs you to the change set's details page, where you can see the time the change set was created, its status, the input used to generate the change set, and a summary of the changes. Executing the change sets:

1. On the change set's details page, choose Execute.

CloudFormation immediately starts updating the stack. The CloudFormation console directs you to the Events tab, where you can monitor the progress of the stack update.

### Clean up

Follow these steps to clean up created resources:

1. In the **[CloudFormation console](https://console.aws.amazon.com/cloudformation)**, select the stack you have created in this lab. For example `cfn-workshop-003`.
1. In the top right corner, click on **Delete**.
1. In the pop up window click on **Delete stack**.
1. You can click the **refresh** button a few times until you see in the status **DELETE_COMPLETE**.

### Conclusion

Use change sets when you want to ensure that AWS CloudFormation doesn't make unintentional changes or when you want to consider several options. It's also the best practice to use change sets to update resources to avoid the unintentional changes for your infrastructure.


```
{
  "Statement" : [
    {
      "Effect" : "Allow",
      "Action" : "Update:*",
      "Principal": "*",
      "Resource" : "*"
    },
    {
      "Effect" : "Deny",
      "Action" : "Update:*",
      "Principal": "*",
      "Resource" : "LogicalResourceId/CFNBucket"
    }
  ]
}
```
