FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["Creative/Creative.csproj", "Creative/"]
RUN dotnet restore "Creative/Creative.csproj"
COPY . .
WORKDIR "/src/Creative"
RUN dotnet build "Creative.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Creative.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Creative.dll"]