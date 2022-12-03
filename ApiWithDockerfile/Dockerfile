#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["ApiWithDockerfile/ApiWithDockerfile.csproj", "ApiWithDockerfile/"]
RUN dotnet restore "ApiWithDockerfile/ApiWithDockerfile.csproj"
COPY . .
WORKDIR "/src/ApiWithDockerfile"
RUN dotnet build "ApiWithDockerfile.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ApiWithDockerfile.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ApiWithDockerfile.dll"]
