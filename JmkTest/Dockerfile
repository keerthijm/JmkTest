FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY JmkTest/JmkTest.csproj JmkTest/
RUN dotnet restore JmkTest/JmkTest.csproj
COPY . .
WORKDIR /src/JmkTest
RUN dotnet build JmkTest.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish JmkTest.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "JmkTest.dll"]
