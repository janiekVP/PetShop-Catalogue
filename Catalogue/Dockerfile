FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Catalogue/Catalogue.csproj", "Catalogue/"]
RUN dotnet restore "Catalogue/Catalogue.csproj"
COPY . .
WORKDIR "/src/Catalogue"
RUN dotnet build "Catalogue.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Catalogue.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Catalogue.dll"]
