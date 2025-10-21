# Heart Track - ECE 413/513 Final Project (2025)

## Project Overview

Heart Track is a low-cost IoT-enabled web application for monitoring heart rate and blood oxygen saturation levels throughout the day. The system consists of:

- **IoT Device**: Particle Photon with MAX30102 sensor for heart rate and blood oxygen monitoring
- **Web Application**: Responsive web app for data visualization and device management
- **Server**: Node.js/Express backend with MongoDB database
- **Real-time Monitoring**: Configurable measurement intervals and time ranges

## Project Structure

```
ece_513_project_demo/
├── README.md                           # This file
├── package.json                        # Node.js dependencies
├── .gitignore                         # Git ignore rules
├── public/                            # Frontend web application
│   ├── index.html                     # Main landing page
│   ├── login.html                     # User login page
│   ├── dashboard.html                 # Main dashboard
│   ├── weekly-summary.html            # Weekly summary view
│   ├── daily-detail.html              # Daily detailed view
│   ├── device-management.html         # Device management
│   ├── settings.html                  # User settings
│   ├── reference.html                 # Third-party references
│   ├── css/                          # Stylesheets
│   │   ├── main.css                  # Main styles
│   │   ├── responsive.css             # Responsive design
│   │   └── charts.css                # Chart-specific styles
│   ├── js/                           # JavaScript modules
│   │   ├── main.js                   # Main application logic
│   │   ├── auth.js                   # Authentication handling
│   │   ├── charts.js                 # Chart functionality
│   │   ├── api.js                    # API communication
│   │   └── utils.js                  # Utility functions
│   └── images/                       # Static images
├── server/                           # Backend server
│   ├── app.js                        # Express app setup
│   ├── server.js                     # Server entry point
│   ├── config/                       # Configuration
│   │   └── database.js               # MongoDB connection
│   ├── routes/                       # API routes
│   │   ├── auth.js                   # Authentication routes
│   │   ├── devices.js                # Device management routes
│   │   ├── measurements.js           # Measurement data routes
│   │   └── users.js                  # User management routes
│   ├── models/                       # Database models
│   │   ├── User.js                   # User model
│   │   ├── Device.js                 # Device model
│   │   └── Measurement.js            # Measurement model
│   └── middleware/                   # Custom middleware
│       ├── auth.js                   # Authentication middleware
│       └── validation.js            # Input validation
├── iot/                              # IoT device code
│   ├── firmware/                     # Particle Photon firmware
│   │   ├── heart_track.ino           # Main firmware file
│   │   ├── sensor_handler.cpp        # Sensor management
│   │   └── wifi_manager.cpp          # WiFi connectivity
│   └── README.md                     # IoT setup instructions
└── docs/                             # Documentation
    ├── api.md                        # API documentation
    ├── setup.md                      # Setup instructions
    ├── hardware.md                   # Hardware requirements
    └── deployment.md                 # Deployment guide
```

## Getting Started

### Prerequisites

- Node.js 16+ and npm
- MongoDB (local or cloud)
- Particle Photon development board
- MAX30102 sensor module
- Basic electronics components (breadboard, jumper wires)

### Installation

1. Clone this repository:
   ```bash
   git clone <your-repository-url>
   cd ece_513_project_demo
   ```

2. Install server dependencies:
   ```bash
   npm install
   ```

3. Set up environment variables:
   ```bash
   cp .env.example .env
   # Edit .env with your MongoDB URI and JWT secret
   ```

4. Start the development server:
   ```bash
   npm run dev
   ```

5. Open your browser and navigate to `http://localhost:3000`

### Hardware Setup

1. Connect the MAX30102 sensor to Particle Photon
2. Upload the firmware from `iot/firmware/`
3. Configure WiFi credentials in the firmware
4. Register the device through the web application

## Key Features

### Web Application
- **Responsive Design**: Works on desktop, tablet, and mobile
- **User Authentication**: Secure login with JWT tokens
- **Device Management**: Add/remove multiple devices
- **Data Visualization**: Interactive charts for heart rate and blood oxygen
- **Weekly Summary**: Average, min, max heart rate over 7 days
- **Daily Detail**: Hourly charts with min/max indicators
- **Configurable Settings**: Customizable measurement intervals and time ranges

### IoT Device
- **Real-time Monitoring**: Configurable measurement requests
- **LED Indicators**: Blue (request), Green (success), Yellow (offline)
- **Offline Storage**: 24-hour local data storage
- **WiFi Connectivity**: Automatic data sync when connected
- **State Machine**: Synchronous operation for reliability

### Server
- **RESTful API**: Well-documented endpoints
- **Token Authentication**: Secure API access
- **MongoDB Integration**: Scalable data storage
- **Error Handling**: Proper HTTP status codes
- **Data Validation**: Input sanitization and validation

## API Endpoints

### Authentication
- `POST /api/auth/register` - User registration
- `POST /api/auth/login` - User login
- `POST /api/auth/logout` - User logout

### Devices
- `GET /api/devices` - Get user devices
- `POST /api/devices` - Register new device
- `PUT /api/devices/:id` - Update device settings
- `DELETE /api/devices/:id` - Remove device

### Measurements
- `GET /api/measurements` - Get measurement data
- `POST /api/measurements` - Submit new measurement
- `GET /api/measurements/weekly` - Get weekly summary
- `GET /api/measurements/daily/:date` - Get daily details

## Project Requirements

This project fulfills the requirements outlined in:
- `ECE_413_513_Final_Project_Description (2025)_v1 (1).docx`

### Core Requirements Met
- ✅ Responsive web application with navigation
- ✅ User account creation and management
- ✅ Device registration and management
- ✅ Node.js/Express/MongoDB backend
- ✅ RESTful API with proper documentation
- ✅ Token-based authentication
- ✅ Weekly summary and daily detail views
- ✅ Interactive charts with time-based data
- ✅ Configurable measurement settings
- ✅ IoT device with LED indicators
- ✅ Offline data storage capability
- ✅ Synchronous state machine implementation

## Development

### Running Tests
```bash
npm test
```

### Building for Production
```bash
npm run build
```

### Linting
```bash
npm run lint
```

## Deployment

1. Set up MongoDB Atlas or local MongoDB instance
2. Configure environment variables for production
3. Deploy server to cloud platform (Heroku, AWS, etc.)
4. Update IoT device firmware with production server URL
5. Test end-to-end functionality

## Course Information

- **Course**: ECE 413/513
- **Project**: Heart Rate Monitoring System
- **Due Date**: December 15, 2025 (11:59 PM)
- **Late Submission**: December 17, 2025 (11:59 PM) with 10-point deduction
- **Instructor**: [Your Name]
- **TA**: [TA Name]
- **Office Hours**: [Schedule]

## Third-Party Libraries and APIs

See `public/reference.html` for a complete list of third-party libraries, APIs, and code used in this project.

## License

This project is created for educational purposes in ECE 413/513 courses at the University of Arizona.

---

**Note**: This is a template project structure. Please customize it according to your specific implementation and remove this note when submitting your final project.
