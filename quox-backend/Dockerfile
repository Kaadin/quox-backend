FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 5001

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["quox-backend.csproj", "./"]
RUN dotnet restore "quox-backend.csproj"
COPY . .
WORKDIR "/src/"
RUN dotnet build "quox-backend.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "quox-backend.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "quox-backend.dll"]
