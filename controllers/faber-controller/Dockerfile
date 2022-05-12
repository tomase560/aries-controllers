FROM mcr.microsoft.com/dotnet/core/sdk:3.1 as build
WORKDIR /app

# Copy csproj and restore distinct layers
COPY *.sln .
COPY TestCenterController/*.csproj ./TestCenterController/
RUN dotnet restore

# Copy and build app
COPY TestCenterController/. ./TestCenterController/
WORKDIR /app/TestCenterController
RUN dotnet publish -c Release -o out

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1 as runtime
WORKDIR /app
COPY --from=build /app/TestCenterController/out ./
ENTRYPOINT ["dotnet", "TestCenterController.dll"]