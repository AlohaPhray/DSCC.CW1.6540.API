FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY ["ProductApiWithRedis/ProductApiWithRedis.csproj", "ProductApiWithRedis/"]
RUN dotnet restore "ProductApiWithRedis/ProductApiWithRedis.csproj"
COPY . .
WORKDIR "/src/ProductApiWithRedis"
RUN dotnet build "ProductApiWithRedis.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "ProductApiWithRedis.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "ProductApiWithRedis.dll"]