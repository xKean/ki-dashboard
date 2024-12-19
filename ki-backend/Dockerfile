# Verwende das .NET 8 SDK als Build-Umgebung
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build-env
WORKDIR /app

# Kopiere csproj und restore Abhängigkeiten
COPY *.csproj ./
RUN dotnet restore

# Kopiere den Rest der App und baue sie
COPY . ./
RUN dotnet publish -c Release -o out

# Verwende das .NET 8 Runtime-Basisimage
FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app
COPY --from=build-env /app/out .

# Setze Standard-Umgebungsvariablen
ENV ASPNETCORE_URLS="http://+:80;https://+:443"
ENV ASPNETCORE_ENVIRONMENT="Production"

# Expose Standard-Ports
EXPOSE 80
EXPOSE 443

# Startpunkt der Anwendung
ENTRYPOINT ["dotnet", "ki-backend.dll"]
