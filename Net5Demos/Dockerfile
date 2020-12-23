#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0-buster-slim AS build
WORKDIR /src
COPY ["Net5Demos/Net5Demos.csproj", "Net5Demos/"]
RUN dotnet restore "Net5Demos/Net5Demos.csproj"
COPY . .
WORKDIR "/src/Net5Demos"
RUN dotnet build "Net5Demos.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Net5Demos.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Net5Demos.dll"]