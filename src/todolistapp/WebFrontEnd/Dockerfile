FROM microsoft/dotnet:2.1-aspnetcore-runtime-nanoserver-sac2016 AS base
WORKDIR /app
EXPOSE 20006

FROM microsoft/dotnet:2.1-sdk-nanoserver-sac2016 AS build
WORKDIR /src
COPY WebFrontEnd/WebFrontEnd.csproj WebFrontEnd/
RUN dotnet restore WebFrontEnd/WebFrontEnd.csproj
COPY . .
WORKDIR /src/WebFrontEnd
RUN dotnet build WebFrontEnd.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish WebFrontEnd.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "WebFrontEnd.dll"]