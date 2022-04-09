#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/runtime:6.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["NetCoreHelloWorldDocker/NetCoreHelloWorldDocker.csproj", "NetCoreHelloWorldDocker/"]
RUN dotnet restore "NetCoreHelloWorldDocker/NetCoreHelloWorldDocker.csproj"
COPY . .
WORKDIR "/src/NetCoreHelloWorldDocker"
RUN dotnet build "NetCoreHelloWorldDocker.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "NetCoreHelloWorldDocker.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "NetCoreHelloWorldDocker.dll"]