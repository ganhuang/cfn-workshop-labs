### Overview

When you create a stack, all update actions are allowed on all resources. By default, anyone with stack update permissions can update all of the resources in the stack. During an update, some resources might require an interruption or be completely replaced, resulting in new physical IDs or completely new storage. You can prevent stack resources from being unintentionally updated or deleted during a stack update by using a stack policy. A stack policy is a JSON document that defines the update actions that can be performed on designated resources.

### Topics Covered

By the end of this lab, you will be able to:

+ Prevent updates to stack resources using stack policy

### Start Lab

#### 1. Apply a stack policy while creating S3 bucket stack (dev)

1. Open the **[AWS CloudFormation](https://console.aws.amazon.com/cloudformation)** link in a new tab and log in to your AWS account.
1. Click on **Create stack** (_With new resources (Standard)_ if you have clicked in the top right corner).
1. In **Prepare template**, choose **Template is ready**.
1. In **Template source**, choose **Upload a template file**.
1. Click on **Choose file** button and navigate to your workshop directory.
1. Select the file `lab04-stack.yaml`.
1. Click **Next**.
1. Provide a **Stack name**: **cfn-workshop-004**.
    + The _Stack name_ identifies the stack. Use a name to help you distinguish the purpose of this stack.
    + Click **Next**.
1. Choose a **EnvironmentType**: **dev**.
1. In the Create Stack wizard, on the **Configure stack options** page, expand the **Advanced** section and then choose **Stack policy**.
1. Specify the stack policy:
   - To write a policy directly in the console, choose Enter stack policy and then type the stack policy directly in the text field.
   ```json
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
1. You can leave other **Configure stack options** default, click **Next**.
1. On the **Review <stack_name>** page, scroll down to the bottom and click on **Create stack**.
1. You can click the **refresh** button a few times until you see in the status **CREATE_COMPLETE**.
1. You can navigate to **Outputs** tab, you can see the **BucketName** which contains **dev** string.

#### 2. Trying to update the protected resource in the stack (test)

1. Navigate to Cloudformation service in the AWS console.
1. Select the **cfn-workshop-004** stack.
1. In the top right corner click on **Update**.
1. In **Prepare template**, choose **Use current template**, click **Next**.
1. Choose the **EnvironmentType** parameter to **test**, click **Next**.
1. You can leave **Configure stack options** default, click **Next**.
1. On the **Review <stack_name>** page, scroll down to the bottom and click on **Update stack**.
1. You can click the **refresh** button a few times until you see in the status **UPDATE_ROLLBACK_COMPLETE**.
1. You can navigate to **Outputs** tab, you can see the **BucketName** which is unchanged.

### Clean up

Follow these steps to clean up created resources:

1. In the **[CloudFormation console](https://console.aws.amazon.com/cloudformation)**, select the stack you have created in this lab. For example `cfn-workshop-004`.
1. In the top right corner, click on **Delete**.
1. In the pop up window click on **Delete stack**.
1. You can click the **refresh** button a few times until you see in the status **DELETE_COMPLETE**.

### Conclusion

Stack policies help protect critical stack resources from unintentional updates that could cause resources to be interrupted or even replaced. A stack policy is a JSON document that describes what update actions can be performed on designated resources. Specify a stack policy whenever you create a stack that has critical resources.
