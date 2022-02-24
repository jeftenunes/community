FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["Community.MVP.WebApp/Community.MVP.WebApp.csproj", "Community.MVP.WebApp/"]
RUN dotnet restore "Community.MVP.WebApp/Community.MVP.WebApp.csproj"
COPY . .
WORKDIR "/src/Community.MVP.WebApp"
RUN dotnet build "Community.MVP.WebApp.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Community.MVP.WebApp.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Community.MVP.WebApp.dll"]
