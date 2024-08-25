FROM mcr.microsoft.com/dotnet/sdk:8.0-alpine AS build-env
WORKDIR /app

# Copy everything
COPY . ./

# Restore dependencies
RUN dotnet restore

# Build the project
RUN dotnet publish -c Release -o out

# Build runtime image
FROM mcr.microsoft.com/dotnet/aspnet:8.0-alpine as final
WORKDIR /app
COPY --from=build-env /app/out .

# Expose the port
EXPOSE 7109

# Run the application
ENTRYPOINT ["dotnet", "certAzureDev.dll"]
