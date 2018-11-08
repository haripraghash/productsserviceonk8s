FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 6326
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["MVCApp.csproj", "MVCApp/"]
RUN dotnet restore "MVCApp/MVCApp.csproj"
COPY . ./MVCApp
WORKDIR "/src/MVCApp"
RUN dotnet build "MVCApp.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "MVCApp.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "MVCApp.dll"]