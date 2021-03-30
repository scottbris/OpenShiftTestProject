FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["OpenShiftTestProject/OpenShiftTestProject.csproj", "OpenShiftTestProject/"]

RUN dotnet restore "OpenShiftTestProject/OpenShiftTestProject.csproj"
COPY . .
WORKDIR "/src/OpenShiftTestProject"
RUN dotnet build "OpenShiftTestProject.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "OpenShiftTestProject.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "OpenShiftTestProject.dll"]