# Heart Track - API Documentation

## Overview

The Heart Track API provides RESTful endpoints for managing users, devices, and health measurements. All API endpoints require authentication except for user registration and login.

## Base URL

```
http://localhost:3000/api
```

## Authentication

The API uses JWT (JSON Web Tokens) for authentication. Include the token in the Authorization header:

```
Authorization: Bearer <your-jwt-token>
```

## Response Format

All API responses follow this format:

### Success Response
```json
{
  "success": true,
  "data": { ... },
  "message": "Operation successful"
}
```

### Error Response
```json
{
  "success": false,
  "error": "Error message",
  "code": "ERROR_CODE"
}
```

## HTTP Status Codes

- `200` - OK (request succeeded)
- `201` - Created (resource created successfully)
- `400` - Bad Request (invalid request data)
- `401` - Unauthorized (authentication required)
- `404` - Not Found (resource not found)
- `500` - Internal Server Error (server error)

## Authentication Endpoints

### POST /auth/register

Register a new user account.

**Request Body:**
```json
{
  "email": "user@example.com",
  "password": "securePassword123!"
}
```

**Response:**
```json
{
  "success": true,
  "data": {
    "token": "jwt-token-here",
    "user": {
      "id": "user-id",
      "email": "user@example.com",
      "createdAt": "2025-01-01T00:00:00.000Z"
    }
  }
}
```

### POST /auth/login

Login with email and password.

**Request Body:**
```json
{
  "email": "user@example.com",
  "password": "securePassword123!",
  "rememberMe": false
}
```

**Response:**
```json
{
  "success": true,
  "data": {
    "token": "jwt-token-here",
    "user": {
      "id": "user-id",
      "email": "user@example.com"
    }
  }
}
```

### POST /auth/logout

Logout and invalidate token.

**Headers:** `Authorization: Bearer <token>`

**Response:**
```json
{
  "success": true,
  "message": "Logged out successfully"
}
```

## Device Endpoints

### GET /devices

Get all devices for the authenticated user.

**Headers:** `Authorization: Bearer <token>`

**Response:**
```json
{
  "success": true,
  "data": [
    {
      "id": "device-id",
      "name": "Heart Track Device #1",
      "status": "online",
      "batteryLevel": 85,
      "lastSeen": "2025-01-01T12:00:00.000Z",
      "settings": {
        "measurementInterval": 30,
        "timeRange": {
          "start": "06:00",
          "end": "22:00"
        }
      }
    }
  ]
}
```

### POST /devices

Register a new device.

**Headers:** `Authorization: Bearer <token>`

**Request Body:**
```json
{
  "name": "Heart Track Device #1",
  "deviceId": "particle-device-id",
  "apiKey": "device-api-key"
}
```

**Response:**
```json
{
  "success": true,
  "data": {
    "id": "device-id",
    "name": "Heart Track Device #1",
    "status": "offline",
    "createdAt": "2025-01-01T00:00:00.000Z"
  }
}
```

### PUT /devices/:id

Update device settings.

**Headers:** `Authorization: Bearer <token>`

**Request Body:**
```json
{
  "name": "Updated Device Name",
  "settings": {
    "measurementInterval": 60,
    "timeRange": {
      "start": "08:00",
      "end": "20:00"
    }
  }
}
```

**Response:**
```json
{
  "success": true,
  "data": {
    "id": "device-id",
    "name": "Updated Device Name",
    "settings": {
      "measurementInterval": 60,
      "timeRange": {
        "start": "08:00",
        "end": "20:00"
      }
    }
  }
}
```

### DELETE /devices/:id

Remove a device.

**Headers:** `Authorization: Bearer <token>`

**Response:**
```json
{
  "success": true,
  "message": "Device removed successfully"
}
```

## Measurement Endpoints

### GET /measurements

Get measurement data with optional filters.

**Headers:** `Authorization: Bearer <token>`

**Query Parameters:**
- `deviceId` (optional) - Filter by device ID
- `startDate` (optional) - Start date (ISO format)
- `endDate` (optional) - End date (ISO format)
- `limit` (optional) - Number of results (default: 100)
- `offset` (optional) - Number to skip (default: 0)

**Response:**
```json
{
  "success": true,
  "data": [
    {
      "id": "measurement-id",
      "deviceId": "device-id",
      "timestamp": "2025-01-01T12:00:00.000Z",
      "heartRate": 72,
      "bloodOxygen": 98
    }
  ],
  "pagination": {
    "total": 1000,
    "limit": 100,
    "offset": 0
  }
}
```

### POST /measurements

Submit a new measurement (typically from IoT device).

**Headers:** `Authorization: Bearer <token>` or `X-API-Key: <device-api-key>`

**Request Body:**
```json
{
  "deviceId": "device-id",
  "heartRate": 72,
  "bloodOxygen": 98,
  "timestamp": "2025-01-01T12:00:00.000Z"
}
```

**Response:**
```json
{
  "success": true,
  "data": {
    "id": "measurement-id",
    "deviceId": "device-id",
    "timestamp": "2025-01-01T12:00:00.000Z",
    "heartRate": 72,
    "bloodOxygen": 98
  }
}
```

### GET /measurements/weekly

Get weekly summary statistics.

**Headers:** `Authorization: Bearer <token>`

**Response:**
```json
{
  "success": true,
  "data": {
    "averageHeartRate": 72,
    "minHeartRate": 58,
    "maxHeartRate": 95,
    "averageOxygen": 98,
    "minOxygen": 94,
    "maxOxygen": 100,
    "totalMeasurements": 168,
    "period": {
      "start": "2025-01-01T00:00:00.000Z",
      "end": "2025-01-07T23:59:59.999Z"
    }
  }
}
```

### GET /measurements/daily/:date

Get detailed measurements for a specific date.

**Headers:** `Authorization: Bearer <token>`

**URL Parameters:**
- `date` - Date in YYYY-MM-DD format

**Response:**
```json
{
  "success": true,
  "data": {
    "date": "2025-01-01",
    "measurements": [
      {
        "id": "measurement-id",
        "timestamp": "2025-01-01T06:00:00.000Z",
        "heartRate": 68,
        "bloodOxygen": 97
      }
    ],
    "summary": {
      "averageHeartRate": 72,
      "minHeartRate": 58,
      "maxHeartRate": 95,
      "averageOxygen": 98,
      "minOxygen": 94,
      "maxOxygen": 100,
      "totalMeasurements": 24
    }
  }
}
```

## User Endpoints

### GET /users/profile

Get current user profile.

**Headers:** `Authorization: Bearer <token>`

**Response:**
```json
{
  "success": true,
  "data": {
    "id": "user-id",
    "email": "user@example.com",
    "createdAt": "2025-01-01T00:00:00.000Z",
    "settings": {
      "measurementInterval": 30,
      "timeRange": {
        "start": "06:00",
        "end": "22:00"
      },
      "notifications": true,
      "emailReports": true
    }
  }
}
```

### PUT /users/profile

Update user profile.

**Headers:** `Authorization: Bearer <token>`

**Request Body:**
```json
{
  "email": "newemail@example.com"
}
```

**Response:**
```json
{
  "success": true,
  "data": {
    "id": "user-id",
    "email": "newemail@example.com",
    "updatedAt": "2025-01-01T12:00:00.000Z"
  }
}
```

### PUT /users/settings

Update user settings.

**Headers:** `Authorization: Bearer <token>`

**Request Body:**
```json
{
  "measurementInterval": 60,
  "timeRange": {
    "start": "08:00",
    "end": "20:00"
  },
  "notifications": false,
  "emailReports": true
}
```

**Response:**
```json
{
  "success": true,
  "data": {
    "settings": {
      "measurementInterval": 60,
      "timeRange": {
        "start": "08:00",
        "end": "20:00"
      },
      "notifications": false,
      "emailReports": true
    }
  }
}
```

## IoT Device Integration

### Device Authentication

IoT devices authenticate using an API key in the `X-API-Key` header:

```
X-API-Key: your-device-api-key
```

### Webhook Endpoint

### POST /iot/webhook

Receive data from Particle Photon devices.

**Headers:** `X-API-Key: <device-api-key>`

**Request Body:**
```json
{
  "deviceId": "particle-device-id",
  "event": "heart-rate-measurement",
  "data": {
    "heartRate": 72,
    "bloodOxygen": 98,
    "timestamp": "2025-01-01T12:00:00.000Z"
  }
}
```

**Response:**
```json
{
  "success": true,
  "message": "Data received successfully"
}
```

## Error Codes

| Code | Description |
|------|-------------|
| `INVALID_CREDENTIALS` | Invalid email or password |
| `USER_NOT_FOUND` | User does not exist |
| `USER_ALREADY_EXISTS` | Email already registered |
| `INVALID_TOKEN` | JWT token is invalid or expired |
| `DEVICE_NOT_FOUND` | Device does not exist |
| `INVALID_API_KEY` | Device API key is invalid |
| `VALIDATION_ERROR` | Request data validation failed |
| `DATABASE_ERROR` | Database operation failed |

## Rate Limiting

API requests are rate limited to 100 requests per 15-minute window per IP address. Rate limit headers are included in responses:

```
X-RateLimit-Limit: 100
X-RateLimit-Remaining: 99
X-RateLimit-Reset: 1640995200
```

## Examples

### JavaScript/Fetch Example

```javascript
// Login
const loginResponse = await fetch('/api/auth/login', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    email: 'user@example.com',
    password: 'password123'
  })
});

const loginData = await loginResponse.json();
const token = loginData.data.token;

// Get devices
const devicesResponse = await fetch('/api/devices', {
  headers: {
    'Authorization': `Bearer ${token}`
  }
});

const devicesData = await devicesResponse.json();
console.log(devicesData.data);
```

### cURL Examples

```bash
# Login
curl -X POST http://localhost:3000/api/auth/login \
  -H "Content-Type: application/json" \
  -d '{"email":"user@example.com","password":"password123"}'

# Get devices
curl -X GET http://localhost:3000/api/devices \
  -H "Authorization: Bearer your-jwt-token"

# Submit measurement
curl -X POST http://localhost:3000/api/measurements \
  -H "Authorization: Bearer your-jwt-token" \
  -H "Content-Type: application/json" \
  -d '{"deviceId":"device-id","heartRate":72,"bloodOxygen":98}'
```
