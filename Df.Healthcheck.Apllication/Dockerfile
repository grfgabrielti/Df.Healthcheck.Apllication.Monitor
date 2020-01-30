FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["Df.Healthcheck.Apllication.UI/Df.Healthcheck.Apllication.UI.csproj", "Df.Healthcheck.Apllication.UI/"]
RUN dotnet restore "Df.Healthcheck.Apllication.UI/Df.Healthcheck.Apllication.UI.csproj"
COPY . .
WORKDIR "/src/Df.Healthcheck.Apllication.UI"
RUN dotnet build "Df.Healthcheck.Apllication.UI.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Df.Healthcheck.Apllication.UI.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Df.Healthcheck.Apllication.UI.dll"]