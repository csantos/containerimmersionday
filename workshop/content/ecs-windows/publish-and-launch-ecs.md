---
title: "Deploy the ASP.Net Framework Application to ECS"
chapter: false
weight: 13
---





Navigate to the ‘ECS-ASPNET’ project and right click and click ‘Publish’
![publish-image](/images/ecs-windows/publish-image.png)

Under Publish Target select ‘Container Registry’ and choose the Custom radio button and click ‘Create Profile’. If prompted for a registry URL simply put localhost
![publish-container-registry](/images/ecs-windows/publish-container-registry.png)
![publish-localhost](/images/ecs-windows/publish-localhost.png)

Click 'Publish'
![publish-localhost](/images/ecs-windows/publish-localhost.png)

Navigate to the Amazon Elastic Container Registry service in the console. Create a new Amazon ECR repository for your image:

![publish-ecr](/images/ecs-windows/publish-ecr.png)

![publish-ecr-listing](/images/ecs-windows/publish-ecr-listing.png)

Click the ‘View push commands’ button at the top of the screen. If you don’t see that button, click your repository name (ex: ecsaspnet) then ‘View push commands’ (We will only use commands 3 and 4 from this pop-up)
![publish-ecr-push-commands](/images/ecs-windows/publish-ecr-push-commands.png)

Open a Command Prompt or PowerShell **as an Administrator** and login to ECR (Modify the region if necessary) 

```
aws ecr get-login --no-include-email --region us-east-2
```

![publish-docker-login](/images/ecs-windows/publish-docker-login.png)

Enter the Docker log-in command from the last step

![publish-docker-login-succeed](/images/ecs-windows/publish-docker-login-succeed.png)

You should see a similar output when the login is successful.

Now we have to tag the container image was built in the local development environment with the ECR repository. Use the syntax from item #3 in the push commands pop-up window. For this example, we’ll use the :latest tag.

---
**NOTE**

In production, it is strongly recommended to use a tagging strategy based on SemVer or repo commit hashes to avoid confusion

---

**Example**
```
docker tag ecsaspnetframework:latest 505753271373.dkr.ecr.us-east-2.amazonaws.com/ecsaspnetframework:latest
```

Now we need to run the docker push command to push the newly created image to the ECR repository (item #4 in the push commands pop-up window).

**Example**
```
docker push 505753271373.dkr.ecr.us-east-2.amazonaws.com/ecsaspnetframework:latest
```
![publish-push](/images/ecs-windows/publish-push.png)

Record the image name and tag for the CloudFormation in the final step below

Let's deploy the ASP.Net application to the ECS Cluster with the CloudFormation template that we downloaded earlier

The required CloudFormation Parameters include the following:

| Parameter               | Value                                        |
| ----------------------- | -------------------------------------------- |
| AppName	              | ecswinservice (or any name of your choosing) |
| ECSCluster              | **retrieve from recorded values**            |
| ECSImageName            | **retrieve from recorded values**            |
| EcsClusterSecurityGroup | **retrieve from recorded values**            |
| SubnetID                | **retrieve from recorded values**            |
| VpcId	                  | **retrieve from recorded values**            |

