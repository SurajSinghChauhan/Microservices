FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build-env
WORKDIR /app

COPY *.csproj ./
RUN dotnet restore

COPY . ./
RUN dotnet publish -c Release -o out

FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app

# Make the app listen on port 80 inside the container
ENV ASPNETCORE_URLS=http://+:80

COPY --from=build-env /app/out ./
ENTRYPOINT ["dotnet", "PlatformService.dll"]
