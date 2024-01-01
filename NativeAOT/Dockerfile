FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["NativeAOT/NativeAOT.csproj", "NativeAOT/"]
RUN dotnet restore "NativeAOT/NativeAOT.csproj"
COPY . .
WORKDIR "/src/NativeAOT"
RUN dotnet build "NativeAOT.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "NativeAOT.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "NativeAOT.dll"]
