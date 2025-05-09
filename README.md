# 📦 Inventory Management API

A standalone ASP.NET Core Web API for managing inventory products. Suitable for CI/CD pipelines and ready for Docker deployment.

## ✅ Features

- RESTful API with CRUD for Products
- SQLite database using EF Core
- Swagger API docs
- Runs on .NET 8

## 🧰 Setup Instructions

### 1. Install Dependencies

```bash
# Install .NET 8 SDK
sudo apt update
sudo apt install -y dotnet-sdk-8.0

# Optional: Confirm .NET installation
dotnet --version

```

```bash

# Install EF Core & Create DB

export PATH="$PATH:$HOME/.dotnet/tools"

dotnet add package Microsoft.EntityFrameworkCore.Sqlite
dotnet add package Microsoft.EntityFrameworkCore.Tools

dotnet restore
dotnet tool install --global dotnet-ef

```

### 2. Run Migrations & Start App

```bash
cd InventoryApi

dotnet ef migrations add InitialCreate
dotnet ef database update
dotnet run
```

App will be available at: [http://<server-ip>:5000/swagger](http://<server-ip>:5000/swagger)

## 🐳 Docker (optional)

```dockerfile
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY . .
RUN dotnet publish -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=build /app/publish .
ENTRYPOINT ["dotnet", "InventoryApi.dll"]
```

To build and run:

```bash
docker build -t inventory-api .
docker run -d -p 5000:5000 inventory-api
```

## 📦 API Endpoints

- `GET /api/products`
- `POST /api/products`
- `PUT /api/products/{id}`
- `DELETE /api/products/{id}`

## ✅ Ready for: Azure VM, Docker, CI/CD

MIT License
