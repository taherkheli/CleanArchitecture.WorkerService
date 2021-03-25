#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/runtime:5.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["src/CleanArchitecture.WorkerService/CleanArchitecture.WorkerService.csproj", "src/CleanArchitecture.WorkerService/"]
RUN dotnet restore "src/CleanArchitecture.WorkerService/CleanArchitecture.WorkerService.csproj"
COPY . .
WORKDIR "/src/src/CleanArchitecture.WorkerService"
RUN dotnet build "CleanArchitecture.WorkerService.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "CleanArchitecture.WorkerService.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "CleanArchitecture.WorkerService.dll"]