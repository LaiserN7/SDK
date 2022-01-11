FROM mcr.microsoft.com/dotnet/runtime:6.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["SDKConsole/SDKConsole.csproj", "SDKConsole/"]
RUN dotnet restore "SDKConsole/SDKConsole.csproj"
COPY . .
WORKDIR "/src/SDKConsole"
RUN dotnet build "SDKConsole.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "SDKConsole.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "SDKConsole.dll"]
