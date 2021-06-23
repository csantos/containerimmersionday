---
title: "Create the ECS Cluster"
chapter: false
weight: 11
---


Open the AWS Management Console, and navigate to ‘Elastic Container Service’.

If this is the first time running the ‘Elastic Container Service’, you will see the following screen.

![ecs-welcome](/images/ecs-windows/ecs-welcome.png)

Click ‘Clusters’ on the Left-Hand menu and then ‘Create Cluster’.

Select ‘EC2 Windows + Networking’ and click ‘Next Step’

![ecs-windows](/images/ecs-windows/ecs-windows.png)

Provide the following details in the Create Cluster page:

| Field |
| -----               | ---- |
| Cluster Name        | ECS-ASPNET-Framework |
| EC2 Instance type   | m5.large |
| Number of instances | 3 |
| All other fields    | Keep defaults |

![ecs-create-cluster](/images/ecs-windows/ecs-create-cluster.png)

**Click ‘Create’**

Wait several minutes while the ECS Cluster is being created. 

When all three boxes are green, **record the following values for later use in Notepad or some other program**:

| Parameters                                                             |
| ---------------------------------------------------------------------- |
| Cluster Name (It should be ECS-ASPNET-Framework unless you changed it) |
| VPC                                                                    |
| Subnet 1                                                               |
| Subnet 2                                                               |
| Security group                                                         |

![ecs-cluster-complete](/images/ecs-windows/ecs-cluster-complete.png)
