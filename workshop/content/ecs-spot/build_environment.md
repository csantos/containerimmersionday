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

