#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["Voter.Api.csproj", ""]
RUN dotnet restore "./Voter.Api.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "Voter.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Voter.Api.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENV ALLOWED_ORIGIN http://localhost:4200
ENTRYPOINT ["dotnet", "Voter.Api.dll"]