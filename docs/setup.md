# Heart Track - Setup Guide

## Prerequisites

Before setting up the Heart Track project, ensure you have the following installed:

- **Node.js** (version 16 or higher)
- **npm** (comes with Node.js)
- **MongoDB** (local installation or MongoDB Atlas account)
- **Git** (for version control)
- **Particle CLI** (for IoT device programming)

## Installation Steps

### 1. Clone the Repository

```bash
git clone <your-repository-url>
cd ece_513_project_demo
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Environment Configuration

Copy the example environment file and configure your settings:

```bash
cp .env.example .env
```

Edit the `.env` file with your specific configuration:

```env
NODE_ENV=development
PORT=3000
MONGODB_URI=mongodb://localhost:27017/hearttrack
JWT_SECRET=your-super-secret-jwt-key-change-this-in-production
FRONTEND_URL=http://localhost:3000
IOT_API_KEY=your-iot-device-api-key
```

### 4. Database Setup

#### Option A: Local MongoDB

1. Install MongoDB locally
2. Start MongoDB service
3. Create a database named `hearttrack`

#### Option B: MongoDB Atlas (Recommended)

1. Create a MongoDB Atlas account
2. Create a new cluster
3. Get your connection string
4. Update `MONGODB_URI` in your `.env` file

### 5. Start the Development Server

```bash
npm run dev
```

The server will start on `http://localhost:3000`

## Hardware Setup

### Required Components

- Particle Photon development board
- MAX30102 heart rate and oxygen sensor
- Micro USB cable
- Mini breadboard
- Jumper wires (male-to-male and male-to-female)

### Wiring Diagram

```
Particle Photon    MAX30102 Sensor
3.3V          →    VCC
GND           →    GND
D0 (SDA)      →    SDA
D1 (SCL)      →    SCL
```

### Firmware Setup

1. Install Particle CLI:
   ```bash
   npm install -g particle-cli
   ```

2. Login to your Particle account:
   ```bash
   particle login
   ```

3. Upload firmware:
   ```bash
   cd iot/firmware
   particle flash <device-name> heart_track.ino
   ```

4. Configure WiFi credentials in the firmware code

## Project Structure

```
ece_513_project_demo/
├── public/                 # Frontend files
│   ├── css/               # Stylesheets
│   ├── js/                # JavaScript modules
│   ├── images/            # Static images
│   └── *.html             # HTML pages
├── server/                # Backend files
│   ├── routes/            # API routes
│   ├── models/            # Database models
│   ├── middleware/        # Custom middleware
│   └── *.js              # Server files
├── iot/                   # IoT device code
│   └── firmware/          # Particle Photon firmware
├── docs/                  # Documentation
└── package.json           # Dependencies
```

## Development Workflow

### Frontend Development

1. Edit HTML files in `public/`
2. Modify CSS in `public/css/`
3. Update JavaScript in `public/js/`
4. Test changes in browser

### Backend Development

1. Modify server files in `server/`
2. Update API routes in `server/routes/`
3. Modify database models in `server/models/`
4. Test API endpoints

### IoT Development

1. Edit firmware in `iot/firmware/`
2. Flash device with Particle CLI
3. Test device connectivity

## Testing

### Run Tests

```bash
npm test
```

### Manual Testing

1. **User Registration/Login**: Test account creation and authentication
2. **Device Management**: Add, update, and remove devices
3. **Data Visualization**: Verify charts display correctly
4. **IoT Integration**: Test device data transmission

## Troubleshooting

### Common Issues

1. **MongoDB Connection Error**
   - Verify MongoDB is running
   - Check connection string in `.env`
   - Ensure database exists

2. **Port Already in Use**
   - Change PORT in `.env` file
   - Kill existing process: `lsof -ti:3000 | xargs kill`

3. **IoT Device Not Connecting**
   - Check WiFi credentials in firmware
   - Verify device is online in Particle Console
   - Check API key configuration

4. **Charts Not Displaying**
   - Verify Chart.js CDN is loaded
   - Check browser console for errors
   - Ensure data is being fetched correctly

### Debug Mode

Enable debug logging by setting in `.env`:

```env
DEBUG=true
VERBOSE_LOGGING=true
```

## Production Deployment

### Environment Variables

Update `.env` for production:

```env
NODE_ENV=production
PORT=3000
MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/hearttrack
JWT_SECRET=your-production-secret-key
FRONTEND_URL=https://your-domain.com
```

### Security Considerations

1. Use strong JWT secrets
2. Enable HTTPS
3. Set up proper CORS policies
4. Implement rate limiting
5. Use environment variables for sensitive data

## Support

For technical support or questions:

1. Check this documentation
2. Review the API documentation
3. Contact course instructors
4. Check GitHub issues (if applicable)

## License

This project is created for educational purposes in ECE 413/513 courses at the University of Arizona.
