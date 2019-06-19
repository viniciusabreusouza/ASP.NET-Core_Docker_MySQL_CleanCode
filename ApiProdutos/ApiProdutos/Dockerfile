FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 55122
EXPOSE 44358

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["ApiProdutos/ApiProdutos.csproj", "ApiProdutos/"]
RUN dotnet restore "ApiProdutos/ApiProdutos.csproj"
COPY . .
WORKDIR "/src/ApiProdutos"
RUN dotnet build "ApiProdutos.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "ApiProdutos.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "ApiProdutos.dll"]