#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["ApnaGharV2/ApnaGharV2.csproj", "ApnaGharV2/"]
RUN dotnet restore "ApnaGharV2/ApnaGharV2.csproj"
COPY . .
WORKDIR "/src/ApnaGharV2"
RUN dotnet build "ApnaGharV2.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ApnaGharV2.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ApnaGharV2.dll"]
