FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["WebProject.web/WebProject.web.csproj", "WebProject.web/"]
RUN dotnet restore "WebProject.web/WebProject.web.csproj"
COPY . .
WORKDIR "/src/WebProject.web"
RUN dotnet build "WebProject.web.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WebProject.web.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .  
ENTRYPOINT [ "dotnet", "WebProject.web.dll" ]
