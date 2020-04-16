---
title: "Build the Environment"
chapter: false
weight: 11
---

In the Cloud9 workspace, run the following commands:

<!-- - Clone the demo repository:

```
cd ~/environment
git clone https://github.com/brentley/container-demo
```

- Ensure service linked roles exist for Load Balancers and ECS:

```
aws iam get-role --role-name "AWSServiceRoleForElasticLoadBalancing" || aws iam create-service-linked-role --aws-service-name "elasticloadbalancing.amazonaws.com"

aws iam get-role --role-name "AWSServiceRoleForECS" || aws iam create-service-linked-role --aws-service-name "ecs.amazonaws.com"
```
 -->

Build the VPC, ECS Cluster, and ALB:
 
```
cd ~/environment/

wget https://resources.containerimmersionday.com/ecs-ec2-spot-us-west-2.yaml

aws cloudformation deploy --stack-name container-demo --template-file ecs-ec2-spot-us-west-2.yaml --capabilities CAPABILITY_IAM
```

The CloudFormation script will utilize EC2 Spot Instances in the environment buildout.

When the [CloudFormation](https://us-west-2.console.aws.amazon.com/cloudformation/home?region=us-west-2#/stacks?filteringText=container-demo&filteringStatus=active&viewNested=true&hideStacks=false&stackId=) execution completes, you can view your Spot Requests in the [EC2 Console](https://us-west-2.console.aws.amazon.com/ec2sp/v1/spot/home?region=us-west-2#)
Monitor the progress of the CloudFormation

