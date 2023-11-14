FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["WebProject.api/WebProject.api.csproj", "WebProject.api/"]
RUN dotnet restore "WebProject.api/WebProject.api.csproj"
COPY . .
WORKDIR "/src/WebProject.api"
RUN dotnet build "WebProject.api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WebProject.api.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WebProject.api.dll"]