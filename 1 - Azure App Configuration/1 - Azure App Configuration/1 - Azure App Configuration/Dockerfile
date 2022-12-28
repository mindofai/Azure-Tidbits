#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["1 - Azure App Configuration/1 - Azure App Configuration.csproj", "1 - Azure App Configuration/"]
RUN dotnet restore "1 - Azure App Configuration/1 - Azure App Configuration.csproj"
COPY . .
WORKDIR "/src/1 - Azure App Configuration"
RUN dotnet build "1 - Azure App Configuration.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "1 - Azure App Configuration.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "1 - Azure App Configuration.dll"]