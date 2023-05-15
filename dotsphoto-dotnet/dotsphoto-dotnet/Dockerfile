FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["dotsphoto-dotnet/dotsphoto-dotnet.csproj", "dotsphoto-dotnet/"]
RUN dotnet restore "dotsphoto-dotnet/dotsphoto-dotnet.csproj"
COPY . .
WORKDIR "/src/dotsphoto-dotnet"
RUN dotnet build "dotsphoto-dotnet.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "dotsphoto-dotnet.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "dotsphoto-dotnet.dll"]
