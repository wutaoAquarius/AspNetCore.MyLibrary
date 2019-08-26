FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["MyLibrary.WebApi/MyLibrary.WebApi.csproj", "MyLibrary.WebApi/"]
RUN dotnet restore "MyLibrary.WebApi/MyLibrary.WebApi.csproj"
COPY . .
WORKDIR "/src/MyLibrary.WebApi"
RUN dotnet build "MyLibrary.WebApi.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "MyLibrary.WebApi.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "MyLibrary.WebApi.dll"]