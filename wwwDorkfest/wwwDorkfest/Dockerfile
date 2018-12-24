FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 65238
EXPOSE 44317

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["wwwDorkfest/wwwDorkfest.csproj", "wwwDorkfest/"]
RUN dotnet restore "wwwDorkfest/wwwDorkfest.csproj"
COPY . .
WORKDIR "/src/wwwDorkfest"
RUN dotnet build "wwwDorkfest.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "wwwDorkfest.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "wwwDorkfest.dll"]