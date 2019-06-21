FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["src.csproj", "./"]
RUN dotnet restore "./src.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "src.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "src.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "src.dll"]
