FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["HelloCSharp/HelloCSharp.csproj", "HelloCSharp/"]
RUN dotnet restore "HelloCSharp/HelloCSharp.csproj"
COPY . .
WORKDIR "/src/HelloCSharp"
RUN dotnet build "HelloCSharp.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "HelloCSharp.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /appK
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "HelloCSharp.dll"]
