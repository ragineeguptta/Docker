# Stage 1: Build
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# Copy csproj and restore dependencies
COPY ./MnualDocker.csproj ./
RUN dotnet restore "MnualDocker.csproj"

# Copy everything else and build
COPY . .
RUN dotnet publish "MnualDocker.csproj" -c Release -o /app/publish

# Stage 2: Runtime (Lightweight)
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS final
WORKDIR /app

# Copy only published output
COPY --from=build /app/publish .

# Run application
ENTRYPOINT ["dotnet", "MnualDocker.dll"]