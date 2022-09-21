FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["BookStor.API/BookStor.API.csproj", "BookStor.API/"]
RUN dotnet restore "BookStor.API/BookStor.API.csproj"
COPY . .
WORKDIR "/src/BookStor.API"
RUN dotnet build "BookStor.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "BookStor.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "BookStor.API.dll"]
