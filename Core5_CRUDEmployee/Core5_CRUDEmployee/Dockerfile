#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Core5_CRUDEmployee/Core5_CRUDEmployee.csproj", "Core5_CRUDEmployee/"]
RUN dotnet restore "Core5_CRUDEmployee/Core5_CRUDEmployee.csproj"
COPY . .
WORKDIR "/src/Core5_CRUDEmployee"
RUN dotnet build "Core5_CRUDEmployee.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Core5_CRUDEmployee.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Core5_CRUDEmployee.dll"]