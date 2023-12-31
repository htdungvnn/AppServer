FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["WASM/WASM.csproj", "WASM/"]
RUN dotnet restore "WASM/WASM.csproj"
COPY . .
WORKDIR "/src/WASM"
RUN dotnet build "WASM.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WASM.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WASM.dll"]
