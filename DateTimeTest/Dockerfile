﻿FROM mcr.microsoft.com/dotnet/runtime:6.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["DateTimeTest/DateTimeTest.csproj", "DateTimeTest/"]
RUN dotnet restore "DateTimeTest/DateTimeTest.csproj"
COPY . .
WORKDIR "/src/DateTimeTest"
RUN dotnet build "DateTimeTest.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "DateTimeTest.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DateTimeTest.dll"]
