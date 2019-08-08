FROM mcr.microsoft.com/dotnet/core/aspnet:2.2 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:2.2 AS build
WORKDIR /src
COPY ["DotnetForDocker/DotnetForDocker.csproj", "DotnetForDocker/"]
RUN dotnet restore "DotnetForDocker/DotnetForDocker.csproj"
COPY . .
WORKDIR "/src/DotnetForDocker"
RUN dotnet build "DotnetForDocker.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "DotnetForDocker.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "DotnetForDocker.dll"]
