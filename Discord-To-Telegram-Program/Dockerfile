# Dockerfile
FROM mcr.microsoft.com/dotnet/runtime:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY "Discord-To-Telegram-Program.csproj" .
RUN dotnet restore "Discord-To-Telegram-Program.csproj"
COPY . .
RUN dotnet build "Discord-To-Telegram-Program.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Discord-To-Telegram-Program.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Discord-To-Telegram-Program.dll"]