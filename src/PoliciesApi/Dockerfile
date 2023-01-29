#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["src/PoliciesApi/PoliciesApi.csproj", "src/PoliciesApi/"]
RUN dotnet restore "src/PoliciesApi/PoliciesApi.csproj"
COPY . .
WORKDIR "/src/src/PoliciesApi"
RUN dotnet build "PoliciesApi.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "PoliciesApi.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "PoliciesApi.dll"]