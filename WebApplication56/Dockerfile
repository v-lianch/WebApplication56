FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["WebApplication56/WebApplication56.csproj", "WebApplication56/"]

RUN dotnet restore "WebApplication56/WebApplication56.csproj"
COPY . .
WORKDIR "/src/WebApplication56"
RUN dotnet build "WebApplication56.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WebApplication56.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WebApplication56.dll"]