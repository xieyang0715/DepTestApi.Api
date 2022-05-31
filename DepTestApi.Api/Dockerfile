#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["DepTestApi.Api.csproj", "DepTestApi.Api/"]
RUN dotnet restore "DepTestApi.Api/DepTestApi.Api.csproj"
COPY .  "DepTestApi.Api/"
WORKDIR "/src/DepTestApi.Api"
RUN dotnet build "DepTestApi.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "DepTestApi.Api.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DepTestApi.Api.dll"]