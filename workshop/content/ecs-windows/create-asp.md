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
FROM mcr.microsoft.com/dotnet/framework/aspnet:4.8-windowsservercore-ltsc2019
ARG source
WORKDIR /inetpub/wwwroot
COPY ${source:-obj/Docker/publish} .
```

Replace it with the following content

```docker
#Depending on the operating system of the host machines(s) that will build or run the containers, the image specified in the FROM statement may need to be changed.
#For more information, please see https://aka.ms/containercompat 
FROM mcr.microsoft.com/dotnet/framework/aspnet:4.8-windowsservercore-ltsc2019 AS base
ARG source

FROM mcr.microsoft.com/dotnet/framework/sdk:4.8 AS build
WORKDIR /app
COPY . .
RUN nuget restore -PackagesDirectory ../packages; msbuild /p:Configuration=Release /p:publishUrl=/out /p:DeleteExistingFiles=True /p:DeployOnBuild=True /p:DeployDefaultTarget=WebPublish /p:WebPublishMethod=FileSystem 

# copy build artifacts into runtime image
FROM base as final
WORKDIR /inetpub/wwwroot
COPY --from=build /out .
```

Next edit the `.dockerignore` file, removing the first line containing the '*' character. The resulting file should look like the below.

![dockerignore-edited](/images/ecs-windows/dockerignore-edited.png)

Build and run the project to ensure it starts up without error. This make take some time as the base Docker images must be downloaded.

![visual-studio-new-asp](/images/ecs-windows/netfx-app-running.png)