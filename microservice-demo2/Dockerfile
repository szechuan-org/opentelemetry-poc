FROM mcr.microsoft.com/dotnet/aspnet:6.0-alpine AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443
EXPOSE 3000

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["microservice-demo2/microservice-demo2.csproj", "microservice-demo2/"]
RUN dotnet restore "microservice-demo2/microservice-demo2.csproj"
COPY . .
WORKDIR "/src/microservice-demo2"
RUN dotnet build "microservice-demo2.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "microservice-demo2.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "microservice-demo2.dll"]
