FROM mcr.microsoft.com/dotnet/aspnet:6.0-alpine AS base
WORKDIR /app
EXPOSE 80
EXPOSE 3000
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["microservice-demo1/microservice-demo1.csproj", "microservice-demo1/"]
RUN dotnet restore "microservice-demo1/microservice-demo1.csproj"
COPY . .
WORKDIR "/src/microservice-demo1"
RUN dotnet build "microservice-demo1.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "microservice-demo1.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "microservice-demo1.dll"]
