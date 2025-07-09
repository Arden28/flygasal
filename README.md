# Flight Booking API - Developed by Arden for Flygasal

![Postman Screenshot](https://raw.githubusercontent.com/Arden28/flygasal/master/postman.png)

Hey Flygasal,

I'm Arden, and this is a clean, functional RESTful API I built for your flight booking system using the Laravel framework. It's simple, elegant, and gets the job done.

# Project Overview

This API handles flight bookings with 21 endpoints for managing **Bookings**, **Flights**, and **Reservations**. The code is straightforward and reusable, so you can consume or adapt it for other projects. I'm not building a full product here—just a solid API implementation for your needs.

The endpoints support creating, updating, partially updating, retrieving, and deleting data. The same concept can be applied to other systems needing clean API consumption.

# Tech Stack

Here's what I used to build this API:
- Migrations (`database/migrations/*`)
- Database Seeding/Factories (`database/factories/*`)
- Tinker
- Resources/Collections (`app/Http/Resources/*`)
- Controllers (`app/Http/Controllers/*`)
- Request Validation (`app/Http/Requests/*`)
- Dependency Injection
- Resource Routing (`routes/api.php`)
- Full Unit Test Coverage (`tests/Feature/*`)
- Eloquent ORM/Models (`app/Models/*`)
- Events/Listeners

Example: `factory(App\User::class)->create()` creates a new User, Booking, Reservation, and Flight. The `UserCreated` event (`app/Events/UserCreated.php`) triggers additional factory creations in `UserFactory` (`database/factories/UserFactory` via `afterCreating`).

# Setup Instructions

To get this running, you need a database and a few terminal commands.

1. Create a database and update `.env` with its details.
2. Copy `.env.example` to `.env` and fill in your database info:
   ```
   cp .env.example .env
   ```

3. Run these commands:
   ```
   git clone https://github.com/Arden28/flygasal.git api
   cd api
   composer install
   php artisan migrate
   php artisan db:seed
   php artisan key:generate
   php artisan serve
   ```

This populates the database with 50 flights, bookings, reservations, and users for testing. The app runs on `http://127.0.0.1:8000` (or your hosted domain).

The front page at `http://127.0.0.1:8000` shows `GET` methods. For `POST`, `PUT`, `PATCH`, or `DELETE`, use an API client like [Postman](https://www.getpostman.com/).

# Unit Testing

Tests use the same database as your `.env`. To use a separate test database, update `phpunit.xml`:
```xml
<env name="DB_DATABASE" value="laravel_test"/>
```

Run tests:
```
vendor/bin/phpunit
```

**Note**: Tests wipe the database. Restore data with:
```
php artisan db:seed
```

# Endpoints

Replace `127.0.0.1:8000` with your domain if hosted. Non-`GET` endpoints need an API client like Postman.

## GET Endpoints
- List items:
  ```
  GET http://127.0.0.1:8000/api/reservations
  GET http://127.0.0.1:8000/api/bookings
  GET http://127.0.0.1:8000/api/flights
  ```
- Get specific item (ID 1–50):
  ```
  GET http://127.0.0.1:8000/api/reservations/1
  GET http://127.0.0.1:8000/api/bookings/1
  GET http://127.0.0.1:8000/api/flights/1
  ```

## POST Endpoints
Create items (sample data):
- Flights:
  ```
  POST http://127.0.0.1:8000/api/flights
  ```
  ```json
  {
    "flight_number": 400,
    "airline": "SouthWest",
    "origin": "DFW",
    "destination": "STI",
    "boarding_time": "2020-01-16 17:30:15",
    "arrival_time": "2020-01-16 20:30:15"
  }
  ```
- Reservations:
  ```
  POST http://127.0.0.1:8000/api/reservations
  ```
  ```json
  {
    "user_id": 400,
    "booking_id": 10,
    "flight_id": 10,
    "passenger_name": "Arden Smith",
    "passenger_email": "test@test.com",
    "reservation_code": "",
    "origin": "DFW",
    "destination": "STI",
    "airline": "SouthWest",
    "status": "active",
    "seat": "20C",
    "price": 0.0,
    "tax": 0,
    "assigned_flight_id": 0
  }
  ```
- Bookings:
  ```
  POST http://127.0.0.1:8000/api/bookings
  ```
  ```json
  {
    "user_id": 20,
    "flight_number": 1500,
    "airline": "American",
    "origin": "LAX",
    "destination": "DFW",
    "boarding_time": "2020-01-16 17:30:15",
    "arrival_time": "2020-01-16 20:30:15",
    "name": "Arden Smith",
    "seat": "20C",
    "email": "test@test.com",
    "passengers": 1,
    "price": 340,
    "tax": 20
  }
  ```

## PUT Endpoints
Update items:
- Flights:
  ```
  PUT http://127.0.0.1:8000/api/flights/1
  ```
  ```json
  {
    "flight_number": 99993,
    "airline": "Frontier",
    "origin": "LAS",
    "destination": "ZVE",
    "boarding_time": "2020-03-08 13:28:44",
    "arrival_time": "2020-03-09 18:30:20"
  }
  ```
- Reservations:
  ```
  PUT http://127.0.0.1:8000/api/reservations/10
  ```
  ```json
  {
    "user_id": 3,
    "booking_id": 11,
    "flight_id": 11,
    "passenger_name": "Arden Smith",
    "passenger_email": "test@test.com",
    "reservation_code": "",
    "origin": "DFW",
    "destination": "STI",
    "airline": "SouthWest",
    "status": "active",
    "seat": "20C",
    "price": 0.0,
    "tax": 0,
    "assigned_flight_id": 0
  }
  ```
- Bookings:
  ```
  PUT http://127.0.0.1:8000/api/bookings/10
  ```
  ```json
  {
    "user_id": 7,
    "flight_number": 300,
    "airline": "Spirit",
    "origin": "LAX",
    "destination": "MIA",
    "boarding_time": "2020-01-16 17:30:15",
    "arrival_time": "2020-01-16 20:30:15",
    "name": "Arden Smith",
    "seat": "20C",
    "email": "test@test.com",
    "passengers": 1,
    "price": 340,
    "tax": 20
  }
  ```

## PATCH Endpoints
Partially update items:
- Flights:
  ```
  PATCH http://127.0.0.1:8000/api/flights/1
  ```
  ```json
  {
    "flight_number": 21
  }
  ```
- Reservations:
  ```
  PATCH http://127.0.0.1:8000/api/reservations/1
  ```
  ```json
  {
    "status": "cancelled"
  }
  ```
- Bookings:
  ```
  PATCH http://127.0.0.1:8000/api/bookings/1
  ```
  ```json
  {
    "email": "test@test.com"
  }
  ```

## DELETE Endpoints
- Delete items:
  ```
  DELETE http://127.0.0.1:8000/api/flights/1
  DELETE http://127.0.0.1:8000/api/reservations/1
  DELETE http://127.0.0.1:8000/api/bookings/1
  ```

## OPTIONS Endpoints
- Check available methods:
  ```
  OPTIONS http://127.0.0.1:8000/api/reservations
  OPTIONS http://127.0.0.1:8000/api/flights
  OPTIONS http://127.0.0.1:8000/api/bookings
  ```

# Notes
- Only `GET` endpoints work in browsers. Other methods (`POST`, `PUT`, `PATCH`, `DELETE`) require an API client like [Postman](https://www.getpostman.com/).
- The API is designed for programmatic consumption, ensuring flexibility for your applications.

Let me know if you need further tweaks or have questions!

Best,
Arden
