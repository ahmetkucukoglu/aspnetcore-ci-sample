FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["CISample.App/CISample.App.csproj", "CISample.App/"]
RUN dotnet restore "CISample.App/CISample.App.csproj"
COPY . .
WORKDIR "/src/CISample.App"
RUN dotnet build "CISample.App.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "CISample.App.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "CISample.App.dll"]