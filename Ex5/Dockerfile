FROM mcr.microsoft.com/dotnet/nightly/aspnet:8.0-preview AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/nightly/sdk:8.0-preview AS build
WORKDIR /src
COPY ["ex5/ex5.csproj", "ex5/"]
RUN dotnet restore "ex5/ex5.csproj"
COPY . .
WORKDIR "/src/ex5"
RUN dotnet build "ex5.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ex5.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ex5.dll"]

