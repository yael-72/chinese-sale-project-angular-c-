# Build stage
FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src

# Copy project file
COPY ["FinalProject.csproj", "./"]

# Restore dependencies
RUN dotnet restore "FinalProject.csproj"

# Copy source code
COPY . .

# Build the application
RUN dotnet build "FinalProject.csproj" -c Release -o /app/build

# Publish stage
FROM build AS publish
RUN dotnet publish "FinalProject.csproj" -c Release -o /app/publish

# Runtime stage
FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS final
WORKDIR /app
COPY --from=publish /app/publish .

# Expose port
EXPOSE 80

# Set environment variable for production
ENV ASPNETCORE_ENVIRONMENT=Production

# Run the application
ENTRYPOINT ["dotnet", "FinalProject.dll"]
