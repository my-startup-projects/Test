FROM mcr.microsoft.com/dotnet/sdk:9.0 AS build
WORKDIR /src

COPY ["WebAppTest.sln", "./"]
COPY ["WebAppTest/WebAppTest.csproj", "WebAppTest/"]

RUN dotnet restore "WebAppTest/WebAppTest.csproj"

COPY . .
RUN dotnet publish "WebAppTest/WebAppTest.csproj" -c Release -o /app/publish --no-restore

FROM mcr.microsoft.com/dotnet/aspnet:9.0 AS runtime
WORKDIR /app

COPY --from=build /app/publish .

EXPOSE 80
ENTRYPOINT ["dotnet", "WebAppTest.dll"]
