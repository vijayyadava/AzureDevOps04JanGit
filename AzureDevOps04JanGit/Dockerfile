#Depending on the operating system of the host machines(s) that will build or run the containers, the image specified in the FROM statement may need to be changed.
#For more information, please see https://aka.ms/containercompat

FROM microsoft/aspnetcore:2.0-nanoserver-1709 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0-nanoserver-1709 AS build
WORKDIR /src
COPY ["AzureDevOps04JanGit/AzureDevOps04JanGit.csproj", "AzureDevOps04JanGit/"]
RUN dotnet restore "AzureDevOps04JanGit/AzureDevOps04JanGit.csproj"
COPY . .
WORKDIR "/src/AzureDevOps04JanGit"
RUN dotnet build "AzureDevOps04JanGit.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "AzureDevOps04JanGit.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "AzureDevOps04JanGit.dll"]