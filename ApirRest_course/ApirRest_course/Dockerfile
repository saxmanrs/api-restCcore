#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["ApirRest_course/ApirRest_course.csproj", "ApirRest_course/"]
RUN dotnet restore "ApirRest_course/ApirRest_course.csproj"
COPY . .
WORKDIR "/src/ApirRest_course"
RUN dotnet build "ApirRest_course.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ApirRest_course.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ApirRest_course.dll"]