FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["dncoreapi.csproj", "./"]
RUN dotnet restore "dncoreapi.csproj"
COPY . .
WORKDIR "/src/dncoreapi"
RUN dotnet build "../dncoreapi.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "../dncoreapi.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "dncoreapi.dll", "--environment=Development"]
