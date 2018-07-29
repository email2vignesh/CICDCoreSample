FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY CoreApp.Web/CoreApp.Web.csproj CoreApp.Web/
RUN dotnet restore CoreApp.Web/CoreApp.Web.csproj
COPY . .
WORKDIR /src/CoreApp.Web
RUN dotnet build CoreApp.Web.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish CoreApp.Web.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "CoreApp.Web.dll"]
