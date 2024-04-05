FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["HelloAzure/HelloAzure.csproj", "HelloAzure/"]
RUN dotnet restore "HelloAzure/HelloAzure.csproj"
COPY . .
WORKDIR "/src/HelloAzure"
RUN dotnet build "HelloAzure.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "HelloAzure.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "HelloAzure.dll"]
