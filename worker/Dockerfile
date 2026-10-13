# Build stage
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /source
COPY *.csproj .
RUN dotnet restore -a amd64
COPY . .
RUN dotnet publish -c release -o /app -a amd64 --no-restore

# Development stage (matching docker-compose target)
FROM build AS dev
CMD ["dotnet", "watch", "run"]

# Final runtime stage
FROM mcr.microsoft.com/dotnet/runtime:8.0 AS final
WORKDIR /app
COPY --from=build /app .
USER app
ENTRYPOINT ["dotnet", "Worker.dll"]
