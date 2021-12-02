#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["IdentityAuthExample/IdentityAuthExample.csproj", "IdentityAuthExample/"]
RUN dotnet restore "IdentityAuthExample/IdentityAuthExample.csproj"
COPY . .
WORKDIR "/src/IdentityAuthExample"
RUN dotnet build "IdentityAuthExample.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "IdentityAuthExample.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "IdentityAuthExample.dll"]