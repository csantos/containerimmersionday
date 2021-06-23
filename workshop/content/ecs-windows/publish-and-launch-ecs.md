---
title: "Deploy the ASP.Net Framework Application to ECS"
chapter: false
weight: 13
---

Navigate to the Amazon Elastic Container Registry service in the console. Create a new Amazon ECR repository named `ecsaspnet` for your image:

![publish-ecr](/images/ecs-windows/publish-ecr.png)

![publish-ecr-listing](/images/ecs-windows/publish-ecr-listing.png)

Click the ‘View push commands’ button at the top of the screen. 
![publish-ecr-push-commands](/images/ecs-windows/publish-ecr-push-commands.png)

Open a PowerShell **as an Administrator** command prompt and *execute the commands listed in the above dialog* from the ECS-ASPNET project's folder. Unless changed, it should be C:\Users\Administrators\source\repos\ECS-ASPNET\ECS-ASPNET.

```
cd C:\Users\Administrator\source\repos\ECS-ASPNET\ECS-ASPNET

aws ecr get-login-password --region us-west-2 | docker login --username AWS --password-stdin <ACCOUNT ID>.dkr.ecr.us-west-2.amazonaws.com

docker build -t ecsaspnet .

docker tag ecsaspnet:latest <ACCOUNT ID>.dkr.ecr.us-west-2.amazonaws.com/ecsaspnet:latest

docker push <ACCOUNT ID>.dkr.ecr.us-west-2.amazonaws.com/ecsaspnet:latest

```

You should see output similar output to:

![publish-to-ecr-complete](/images/ecs-windows/publish-to-ecr-complete.png)

Record the ECR tag from the docker push command above (Similar to `<ACCOUNT ID>`.dkr.ecr.us-west-2.amazonaws.com/ecsaspnet:latest) so that you reference it when deploying the CloudFormation template below.

Let's deploy the ASP.Net application to the ECS Cluster with the CloudFormation template that we downloaded earlier

Navigate to the CloudFormation Console and create a new stack

![create-cloudformation-stack](/images/ecs-windows/create-cloudformation-stack.png)

Select the previously downloaded ecs.yaml file.

![create-cloudformation-stack-step1](/images/ecs-windows/create-cloudformation-stack-step1.png)

The required CloudFormation Parameters include the following:

| Parameter               | Value                                        |
| ----------------------- | -------------------------------------------- |
| AppName	              | ecswinservice (or any name of your choosing) |
| ECSCluster              | **retrieve from recorded values** (It should be ECS-ASPNET-Framework unless you changed it)           |
| ECSImageName            | **retrieve from recorded values** (Similar to `<ACCOUNT ID>`.dkr.ecr.us-west-2.amazonaws.com/ecsaspnet:latest) |
| EcsClusterSecurityGroup | **retrieve from recorded values**            |
| SubnetID                | **retrieve from recorded values**            |
| VpcId	                  | **retrieve from recorded values**            |

![create-cloudformation-stack-step2](/images/ecs-windows/create-cloudformation-stack-step2.png)

Click Next on Step 3 of the Create Stack Wizard

![create-cloudformation-stack-step3](/images/ecs-windows/create-cloudformation-stack-step3.png)

In Step 4, acknowledge that IAM resources will be created and click Create Stack

![create-cloudformation-stack-final-step](/images/ecs-windows/create-cloudformation-stack-final-step.png)

Once the Stack has successfully completed, switch the output tabs, and click on the URL for the ALB

![create-cloudformation-stack-outputs](/images/ecs-windows/create-cloudformation-stack-outputs.png)

Congratulations! You have successfully deployed the .NET Framework 4.8 application to ECS.

![ecs-running-app](/images/ecs-windows/ecs-running-app.png)