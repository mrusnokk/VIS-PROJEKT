# 🚲 Bikesharing

A bike-sharing system built with **C# and ASP.NET Core**. Customers can browse stations, rent a bike at one station and return it at another, while the app tracks every rental and every change of a bike's status. The same data is also exposed through a **REST API** with token authentication, so it can be used from a separate (e.g. desktop admin) client.

## ✨ Features

**Web app (MVC + Razor)**
- Registration and login with **BCrypt**-hashed passwords and session cookies
- List of stations with the number of available bikes, and a detail page for each station
- Renting and returning a bike (the return can happen at a different station)
- Personal profile with rental history
- Monthly statistics: rentals started and ended per station

**REST API** (`/api/...`)
- `auth`: obtain an access token
- `bikes`: list, detail, create, update, delete, change status, status history
- `stations`: full CRUD
- `rentals`: all rentals, my rentals, my active rental, start and return a rental
- `users`: list, detail, activate/deactivate, delete
- `docs`: API documentation generated automatically from the controllers via reflection

## 🧱 Architecture

```
Models/                  Domain models: Bike, BikeStatusHistory, Customer,
                         Rental, Station, StationDetail
Web/
├── Controllers/         MVC controllers (Home, Account, Stations, Rentals,
│   └── Api/             Profile, Statistics) and REST API controllers
├── Repositories/        Data access for bikes, stations, rentals, users, history
├── Services/            AuthService, TokenService
├── ViewModels/          Models for the Razor views
├── Views/               Razor views
└── Data/                Database initialization
```

The app follows a layered design: controllers talk to repositories and services, and views receive dedicated view models. The domain models live in a separate shared project so a different client can reuse them.

## 🛠️ Tech stack

- **C#**, **ASP.NET Core** (MVC, Razor views, REST API controllers)
- **SQLite** through **Dapper** and `Microsoft.Data.Sqlite`
- **BCrypt.Net** for password hashing
- Session-based auth for the web app, token auth for the API
