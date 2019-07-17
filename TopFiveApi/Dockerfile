FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["TopFiveApi/TopFiveApi.csproj", "TopFiveApi/"]
RUN dotnet restore "TopFiveApi/TopFiveApi.csproj"
COPY . .
WORKDIR "/src/TopFiveApi"
RUN dotnet build "TopFiveApi.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "TopFiveApi.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "TopFiveApi.dll"]