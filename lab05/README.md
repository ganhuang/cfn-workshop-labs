### Overview

Even as you manage your resources through CloudFormation, users can change those resources outside of CloudFormation. Users can edit resources directly by using the underlying service that created the resource.

For example, you can use the Amazon EC2 console to update a server instance that was created as part of a CloudFormation stack. Some changes may be accidental, and some may be made intentionally to respond to time-sensitive operational events. Regardless, changes made outside of CloudFormation can complicate stack update or deletion operations. You can use drift detection to identify stack resources to which configuration changes have been made outside of CloudFormation management.

### Topics Covered

By the end of this lab, you will be able to:

+ Detecting unmanaged configuration changes to stacks and resources

### Start Lab

#### 1. Creating S3 bucket stack (dev)

1. Open the **[AWS CloudFormation](https://console.aws.amazon.com/cloudformation)** link in a new tab and log in to your AWS account.
1. Click on **Create stack** (_With new resources (Standard)_ if you have clicked in the top right corner).
1. In **Prepare template**, choose **Template is ready**.
1. In **Template source**, choose **Upload a template file**.
1. Click on **Choose file** button and navigate to your workshop directory.
1. Select the file `lab05-stack.yaml`.
1. Click **Next**.
1. Provide a **Stack name**: **cfn-workshop-005**.
    + The _Stack name_ identifies the stack. Use a name to help you distinguish the purpose of this stack.
    + Click **Next**.
1. Choose a **EnvironmentType**: **dev**.
1. You can leave other **Configure stack options** default, click **Next**.
1. On the **Review <stack_name>** page, scroll down to the bottom and click on **Create stack**.
1. You can click the **refresh** button a few times until you see in the status **CREATE_COMPLETE**.
1. You can navigate to **Outputs** tab, you can see the **BucketName** which contains **dev** string.

#### 2. Perform the unmanaged configuration changes on the S3 bucket

1. Navigate to S3 service in the AWS console.
1. In the Buckets list, choose the name of the bucket which was created above.
1. Choose **Properties**.
1. Under Bucket Versioning, choose Edit.
1. Choose **Enable**, and then choose Save changes.

#### 3. Detect drift on an entire CloudFormation stack

1. Open the **[AWS CloudFormation](https://console.aws.amazon.com/cloudformation)** link in a new tab and log in to your AWS account.
1. From the list of stacks, select the stack **cfn-workshop-005**. In the stack details pane, choose Stack actions, and then choose Detect drift.
1. Wait until CloudFormation completes the drift detection operation. When the drift detection operation completes, CloudFormation updates Drift status and Last drift check time for your stack. These fields are listed in the Overview section of the Stack info pane of the stack details page.
1. Review the drift detection results for the stack and its resources. With your stack selected, from the Stack actions menu select View drift results.

#### 4. Resolve drift by updating the template

1. Open and Edit the file `lab05-stack.yaml`.
1. Update the status of **Status** to **Enabled** for the file `lab05-stack.yaml`.
```
    Type: AWS::S3::Bucket
    Properties:
      BucketName: !Sub 'cfn-workshop-05-${AWS::Region}-${EnvironmentType}-${AWS::AccountId}'
      VersioningConfiguration:
        # https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-s3-bucket-versioningconfig.html
        # Allowed values: Enabled | Suspended
        Status: Enabled
```
1. Navigate to Cloudformation service in the AWS console.
1. Select the **cfn-workshop-005** stack.
1. In the top right corner click on **Update**.
1. In **Prepare template**, choose **Use current template**, click **Next**.
1. Keep **EnvironmentType** parameter unchanged, click **Next**.
1. You can leave **Configure stack options** default, click **Next**.
1. On the **Review <stack_name>** page, scroll down to the bottom and click on **Update stack**.
1. You can click the **refresh** button a few times until you see in the status **UPDATE_COMPLETE**.
1. You can navigate to **Outputs** tab, you can see the **BucketName** which is unchanged.

#### 5. Re-Detect drift on an entire CloudFormation stack

1. Open the **[AWS CloudFormation](https://console.aws.amazon.com/cloudformation)** link in a new tab and log in to your AWS account.
1. From the list of stacks, select the stack **cfn-workshop-005**. In the stack details pane, choose Stack actions, and then choose Detect drift.
1. Wait until CloudFormation completes the drift detection operation. When the drift detection operation completes, CloudFormation updates Drift status and Last drift check time for your stack. These fields are listed in the Overview section of the Stack info pane of the stack details page.
1. The **Drift Status** should be **IN_SYNC** for now.

### Clean up

Follow these steps to clean up created resources:

1. In the **[CloudFormation console](https://console.aws.amazon.com/cloudformation)**, select the stack you have created in this lab. For example `cfn-workshop-005`.
1. In the top right corner, click on **Delete**.
1. In the pop up window click on **Delete stack**.
1. You can click the **refresh** button a few times until you see in the status **DELETE_COMPLETE**.
