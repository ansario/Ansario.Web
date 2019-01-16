FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["Ansario.Web.csproj", "Ansario.Web/"]
RUN dotnet restore "Ansario.Web/Ansario.Web.csproj"
COPY . .
WORKDIR "/src/Ansario.Web"
RUN dotnet build "Ansario.Web.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Ansario.Web.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Ansario.Web.dll"]