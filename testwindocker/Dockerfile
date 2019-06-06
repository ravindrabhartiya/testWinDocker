FROM microsoft/aspnetcore:2.0-nanoserver-1709 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0-nanoserver-1709 AS build
WORKDIR /src
COPY testwindocker/testwindocker.csproj testwindocker/
RUN dotnet restore testwindocker/testwindocker.csproj
COPY . .
WORKDIR /src/testwindocker
RUN dotnet build testwindocker.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish testwindocker.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "testwindocker.dll"]
