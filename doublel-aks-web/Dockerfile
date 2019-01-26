FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ./doublel-aks-web/doublel-aks-web.csproj doublel-aks-web/
RUN dotnet restore doublel-aks-web/doublel-aks-web.csproj
COPY . .
WORKDIR /src/doublel-aks-web
RUN dotnet build doublel-aks-web.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish doublel-aks-web.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "doublel-aks-web.dll"]
