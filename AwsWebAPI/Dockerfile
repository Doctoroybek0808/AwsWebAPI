FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
 WORKDIR /app
EXPOSE 80
EXPOSE 443
 
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["AwsWebAPI.csproj", "AwsWebAPI/"]
RUN dotnet restore "AwsWebAPI.csproj"
COPY . .
WORKDIR "/src/AwsWebAPI"
RUN dotnet build "AwsWebAPI.csproj" -c Release -o /app/build
 
FROM build AS publish
RUN dotnet publish "AwsWebAPI.csproj" -c Release -o /app/publish
 
FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "AwsWebAPI.dll"]