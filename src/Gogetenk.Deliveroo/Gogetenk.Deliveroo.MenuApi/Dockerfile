#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["Gogetenk.Deliveroo.MenuApi/Gogetenk.Deliveroo.MenuApi.csproj", "Gogetenk.Deliveroo.MenuApi/"]
RUN dotnet restore "Gogetenk.Deliveroo.MenuApi/Gogetenk.Deliveroo.MenuApi.csproj"
COPY . .
WORKDIR "/src/Gogetenk.Deliveroo.MenuApi"
RUN dotnet build "Gogetenk.Deliveroo.MenuApi.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Gogetenk.Deliveroo.MenuApi.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Gogetenk.Deliveroo.MenuApi.dll"]