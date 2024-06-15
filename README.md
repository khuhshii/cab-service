# Taxi Service Backend Application

## Overview
This backend application provides an API for a taxi service. It includes functionalities for riders and drivers such as requesting a ride, starting a ride, canceling a ride, and rating each other. The application uses ASP.NET Core for the API and Entity Framework Core for database interactions.

## Features
- **User Management**: Add riders and drivers, and authenticate users.
- **Ride Management**: Request, start, end, and cancel rides.
- **Rating System**: Riders can rate drivers and vice versa.
- **Driver Availability**: Toggle driver availability.

## Technologies Used
- ASP.NET Core
- Entity Framework Core
- Microsoft SQL Server
- JWT for Authentication and Authorization

## Prerequisites
- [.NET SDK](https://dotnet.microsoft.com/download) (version 6.0 or later)
- [SQL Server](https://www.microsoft.com/en-us/sql-server/sql-server-downloads) or any other compatible database server.
- [Postman](https://www.postman.com/) or any other API testing tool.

## Setup Instructions

### 1. Clone the Repository
```bash
git clone https://github.com/yourusername/taxi-service-backend.git
cd taxi-service-backend
```

### 2. Configure the Database
Update the `appsettings.json` file with your database connection string:
```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Server=your_server;Database=your_database;User Id=your_user;Password=your_password;"
  },
  "Jwt": {
    "Key": "your_secret_key",
    "Issuer": "your_issuer"
  }
}
```

### 3. Apply Migrations and Seed Database
```bash
dotnet ef database update
```

### 4. Run the Application
```bash
dotnet run
```

## API Endpoints

### Authorization Controller

#### Add Rider
- **URL**: `POST /api/authorize/add-rider`
- **Request Body**:
```json
{
  "Name": "John Doe",
  "Email": "john@example.com",
  "Phone": "1234567890",
  "Password": "password123"
}
```

#### Add Driver
- **URL**: `POST /api/authorize/add-driver`
- **Request Body**:
```json
{
  "Name": "Jane Smith",
  "Email": "jane@example.com",
  "Phone": "0987654321",
  "Password": "password123",
  "VehicleDetails": {
    "VehicleNumber": "ABC123",
    "VehicleType": "Car"
  }
}
```

#### Login
- **URL**: `POST /api/authorize/login`
- **Request Body**:
```json
{
  "EmailOrPhone": "john@example.com",
  "Password": "password123",
  "UserType": "Rider"
}
```

### Rider Controller

#### Request Ride
- **URL**: `POST /api/rider/request-ride`
- **Request Body**:
```json
{
  "PickupLocation": "Location A",
  "DropLocation": "Location B",
  "TypeOfRide": "car"
}
```

#### Get Current Ride
- **URL**: `GET /api/rider/current-ride`

#### Rate Driver
- **URL**: `POST /api/rider/rate-driver`
- **Request Body**:
```json
{
  "RideId": "ride-id",
  "Rating": 5
}
```

### Driver Controller

#### Toggle Availability
- **URL**: `POST /api/driver/toggle-availability`

#### Get Current Ride
- **URL**: `GET /api/driver/current-ride`

#### Start Ride
- **URL**: `POST /api/driver/start-ride`
- **Request Body**:
```json
{
  "RideId": "ride-id",
  "OTP": "123456"
}
```

#### Rate Rider
- **URL**: `POST /api/driver/rate-rider`
- **Request Body**:
```json
{
  "RideId": "ride-id",
  "Rating": 5
}
```

### Ride Controller

#### Cancel Ride
- **URL**: `POST /api/ride/cancel-ride`
- **Request Body**:
```json
{
  "RideId": "ride-id"
}
```

#### End Ride
- **URL**: `POST /api/ride/end-ride`
- **Request Body**:
```json
{
  "RideId": "ride-id"
}
```

## Exception Handling

### Custom Exceptions
- `UserNotFoundException`
- `RideNotFoundException`
- `OngoingOrPendingRideException`
- `AlreadyRatedException`
- `InvalidOTPException`

### Error Messages
Custom error messages are defined in `Constants/ErrorMessages.cs`.

## Utilities
- **JwtUtils**: Utility for extracting email and role from JWT claims.
- **GenerateOTP**: Utility for generating OTP.

## Mappers
- `AddUserMapper`
- `AddDriverMapper`
- `RatingsMapper`

## Models
### Request Models
- `AddUser`
- `AddDriver`
- `UserLogin`
- `RideRequest`
- `RateRequest`
- `StartRideRequest`
- `CancelOrEndRideRequest`

### Response Models
- `RideResponseRider`
- `RideResponseDriver`
- `StartRideResponse`

## Enums
- `UserType`
- `VehicleType`
- `RideStatus`

## Running Tests
To be implemented.

## Contribution Guidelines
To be implemented.

## License
To be implemented.

## Contact
For further information or inquiries, please contact [khushi6452@gmail.com].

---

This README provides a comprehensive overview of the Taxi Service Backend application, covering setup, API endpoints, and other crucial information needed for development and usage.