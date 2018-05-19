FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 56165
EXPOSE 44389

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY SGC.Web/SGC.Web.csproj SGC.Web/
RUN dotnet restore SGC.Web/SGC.Web.csproj
COPY . .
WORKDIR /src/SGC.Web
RUN dotnet build SGC.Web.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish SGC.Web.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "SGC.Web.dll"]
