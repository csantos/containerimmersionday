---
title: "Install CLI Tools"
chapter: false
weight: 14
---

The following tools are useful for the lab exercises

#### Update awscli

Upgrade AWS CLI according to guidance in [AWS documentation](https://docs.aws.amazon.com/cli/latest/userguide/install-linux.html).

```
sudo pip install --upgrade awscli && hash -r
```
#### Install the ECS CLI
```
sudo curl -so /usr/local/bin/ecs-cli https://s3.amazonaws.com/amazon-ecs-cli/ecs-cli-linux-amd64-latest
sudo chmod +x /usr/local/bin/ecs-cli
```

#### Install jq, envsubst (from GNU gettext utilities) and bash-completion
```
sudo yum -y install jq gettext bash-completion
```

#### Verify the binaries are in the path and executable
```
for command in jq envsubst aws
  do
    which $command &>/dev/null && echo "$command in path" || echo "$command NOT FOUND"
  done
```
