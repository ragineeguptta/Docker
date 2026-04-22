# Stage 1: Build
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# Copy csproj and restore dependencies
COPY ./DockerSample.csproj ./
RUN dotnet restore "DockerSample.csproj"

# Copy everything else and build
COPY . .
RUN dotnet publish "DockerSample.csproj" -c Release -o /app/publish

# Stage 2: Runtime (Lightweight)
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS final
WORKDIR /app
ENV DOTNET_URLS=http://+:5000 
# Copy only published output
COPY --from=build /app/publish .

# Run application
ENTRYPOINT ["dotnet", "DockerSample.dll"]