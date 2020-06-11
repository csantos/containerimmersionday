---
title: "Create the ASP.Net Framework Application"
chapter: false
weight: 12
---


Open Visual Studio and click ‘File’ and ‘New Project’

Select the C# language and type asp.net in the filter. Select ‘ASP.NET Web Application (.NET Framework)’ and click ‘Next’
![visual-studio-new-application](/images/ecs-windows/visual-studio-new-application.png)

Specify Project and Solutions names as ‘ECS-ASPNET’, and click ‘Create’.
![visual-studio-new-project](/images/ecs-windows/visual-studio-new-project.png)

Select the ‘MVC’ project template, make sure ‘Enable Docker support’ is checked. Then, click ‘Create’
![visual-studio-new-asp](/images/ecs-windows/visual-studio-new-asp.png)

Examine the automatically-generated Dockerfile. It may look like this

```docker
FROM microsoft/aspnet
ARG source
WORKDIR /inetpub/wwwroot
COPY ${source:-obj/Docker/publish} .
```



Build and run the project to ensure it starts up without error.

