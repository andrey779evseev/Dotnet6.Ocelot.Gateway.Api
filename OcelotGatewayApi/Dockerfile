FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 3000
EXPOSE 443

ENV ASPNETCORE_URLS=http://+:3000
ENV ASPNETCORE_ENVIRONMENT=Development

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["OcelotGatewayApi/OcelotGatewayApi.csproj", "OcelotGatewayApi/"]
RUN dotnet restore "OcelotGatewayApi/OcelotGatewayApi.csproj"
COPY . .
WORKDIR "/src/OcelotGatewayApi"
RUN dotnet build "OcelotGatewayApi.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "OcelotGatewayApi.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "OcelotGatewayApi.dll"]
