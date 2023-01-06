#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["learnDocker/learnDocker.csproj", "learnDocker/"]
RUN dotnet restore "learnDocker/learnDocker.csproj"
COPY . .
WORKDIR "/src/learnDocker"
RUN dotnet build "learnDocker.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "learnDocker.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "learnDocker.dll"]