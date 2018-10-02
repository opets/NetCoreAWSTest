FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY NetCoreWebAppTest/NetCoreWebAppTest.csproj NetCoreWebAppTest/
RUN dotnet restore NetCoreWebAppTest/NetCoreWebAppTest.csproj
COPY . .
WORKDIR /src/NetCoreWebAppTest
RUN dotnet build NetCoreWebAppTest.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish NetCoreWebAppTest.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "NetCoreWebAppTest.dll"]
