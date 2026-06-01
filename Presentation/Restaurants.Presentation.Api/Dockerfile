FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["Presentation/Restaurants.Presentation.Api/Restaurants.Presentation.Api.csproj", "Presentation/Restaurants.Presentation.Api/"]
COPY ["Application/Restaurants.Application.Bussiness/Restaurants.Application.Bussiness.csproj", "Application/Restaurants.Application.Bussiness/"]
COPY ["Application/Restaurant.Application.Ioc/Restaurant.Application.Ioc.csproj", "Application/Restaurant.Application.Ioc/"]
COPY ["Domain/Restaurants.Domain.Entities/Restaurants.Domain.Entities.csproj", "Domain/Restaurants.Domain.Entities/"]
COPY ["Domain/Restaurants.Domain.Repositories/Restaurants.Domain.Repositories.csproj", "Domain/Restaurants.Domain.Repositories/"]
COPY ["Domain/Restaurants.Domain.Exceptions/Restaurants.Domain.Exceptions.csproj", "Domain/Restaurants.Domain.Exceptions/"]
COPY ["Domain/Restaurants.Domain.Services/Restaurants.Domain.Services.csproj", "Domain/Restaurants.Domain.Services/"]
COPY ["Infrastructure/Restaurants.Infrastructure.Database/Restaurants.Infrastructure.Database.csproj", "Infrastructure/Restaurants.Infrastructure.Database/"]
COPY ["Infrastructure/Restaurants.Infrastructure.Ioc/Restaurants.Infrastructure.Ioc.csproj", "Infrastructure/Restaurants.Infrastructure.Ioc/"]
COPY ["Infrastructure/Restaurants.Infrastructure.Application/Restaurants.Infrastructure.Application.csproj", "Infrastructure/Restaurants.Infrastructure.Application/"]
COPY ["Infrastructure/Restaurants.Infrastructure.BlobStorage/Restaurants.Infrastructure.BlobStorage.csproj", "Infrastructure/Restaurants.Infrastructure.BlobStorage/"]
RUN dotnet restore "Presentation/Restaurants.Presentation.Api/Restaurants.Presentation.Api.csproj"
COPY . .
RUN dotnet build "Presentation/Restaurants.Presentation.Api/Restaurants.Presentation.Api.csproj" -c Release -o /app/build
FROM build AS publish
RUN dotnet publish "Presentation/Restaurants.Presentation.Api/Restaurants.Presentation.Api.csproj" -c Release -o /app/publish /p:UseAppHost=false
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS final
WORKDIR /app
EXPOSE 8080
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Restaurants.Presentation.Api.dll"]
