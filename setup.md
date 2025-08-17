# Quick Setup Guide

## Prerequisites
- Node.js (v16 or higher)
- MongoDB (local or MongoDB Atlas)
- npm or yarn

## Backend Setup

1. **Navigate to backend directory:**
   ```bash
   cd backend
   ```

2. **Install dependencies:**
   ```bash
   npm install
   ```

3. **Create environment file:**
   ```bash
   # Copy the example file
   cp env.example .env
   ```

4. **Update .env file with your configuration:**
   ```env
   PORT=5000
   MONGODB_URI=mongodb://localhost:27017/doctor-consultation
   JWT_SECRET=your-super-secret-jwt-key-change-in-production
   OTP_SECRET=123456
   NODE_ENV=development
   ```

5. **Seed the database:**
   ```bash
   npm run seed
   ```

6. **Start the backend server:**
   ```bash
   npm start
   ```

The backend will run on `http://localhost:5000`

## Frontend Setup

1. **Navigate to frontend directory:**
   ```bash
   cd frontend
   ```

2. **Install dependencies:**
   ```bash
   npm install
   ```

3. **Create environment file:**
   ```bash
   # Copy the example file
   cp env.example .env.local
   ```

4. **Update .env.local file:**
   ```env
   NEXT_PUBLIC_API_URL=http://localhost:5000
   ```

5. **Start the frontend development server:**
   ```bash
   npm run dev
   ```

The frontend will run on `http://localhost:3000`

## Test Credentials

After seeding the database, you can use these credentials:

- **Email:** john@example.com
- **Password:** password123

- **Email:** jane@example.com  
- **Password:** password123

## Demo OTP

For booking appointments, use the OTP: **123456**

## Features to Test

1. **User Registration/Login**
2. **Doctor Discovery** - Filter by specialization, mode, date
3. **Slot Booking** - Select date/time, lock slot, confirm with OTP
4. **Appointment Dashboard** - View and filter appointments
5. **Appointment Confirmation** - Enter OTP to confirm pending appointments

## API Endpoints

- `GET /api/health` - Health check
- `POST /api/auth/register` - User registration
- `POST /api/auth/login` - User login
- `GET /api/doctors` - Get doctors with filters
- `GET /api/slots` - Get available slots
- `POST /api/slots/:id/lock` - Lock a slot
- `POST /api/appointments` - Book appointment
- `POST /api/appointments/:id/confirm` - Confirm with OTP
- `GET /api/appointments` - Get user appointments

## Troubleshooting

1. **MongoDB Connection Error:**
   - Make sure MongoDB is running
   - Check the MONGODB_URI in your .env file

2. **Port Already in Use:**
   - Change the PORT in .env file
   - Update NEXT_PUBLIC_API_URL accordingly

3. **CORS Errors:**
   - Backend has CORS enabled for all origins in development
   - Check that the API URL is correct in frontend .env.local

4. **Build Errors:**
   - Make sure all dependencies are installed
   - Check Node.js version compatibility

