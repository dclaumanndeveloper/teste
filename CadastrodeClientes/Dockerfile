#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["CadastrodeClientes/CadastrodeClientes.csproj", "CadastrodeClientes/"]
RUN dotnet restore "CadastrodeClientes/CadastrodeClientes.csproj"
COPY . .
WORKDIR "/src/CadastrodeClientes"
RUN dotnet build "CadastrodeClientes.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "CadastrodeClientes.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "CadastrodeClientes.dll"]