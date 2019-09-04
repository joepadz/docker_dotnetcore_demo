FROM microsoft/dotnet:2.2-aspnetcore-runtime-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk-stretch AS build
WORKDIR /src
COPY ["PMI.DevOps.Monitoring.csproj", ""]
RUN dotnet restore "PMI.DevOps.Monitoring.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "PMI.DevOps.Monitoring.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "PMI.DevOps.Monitoring.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "PMI.DevOps.Monitoring.dll"]