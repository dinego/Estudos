#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Estudos/Estudos.csproj", "Estudos/"]
RUN dotnet restore "Estudos/Estudos.csproj"
COPY . .
WORKDIR "/src/Estudos"
RUN dotnet build "Estudos.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Estudos.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Estudos.dll"]