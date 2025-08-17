# Doctor Consultation MVP

A simple full-stack doctor consultation application built with React (Next.js), Node.js, Express, and MongoDB.

## Features

- **Doctor Discovery**: Search doctors by specialization, availability, and mode (online/in-person)
- **Slot Booking**: Book appointments with 5-minute slot locking and OTP confirmation
- **Reschedule Flow**: Reschedule or cancel appointments (>24h before)
- **Appointment Dashboard**: View upcoming and past appointments with filtering
- **Authentication**: JWT-based user authentication

## Project Structure

```
AyuCare/
├── backend/                 # Node.js + Express + MongoDB
│   ├── models/             # Database schemas
│   ├── routes/             # API endpoints
│   ├── middleware/         # Authentication middleware
│   ├── scripts/            # Database seeding
│   └── server.js           # Main server file
├── frontend/               # Next.js + React + TypeScript
│   ├── app/                # App router pages
│   ├── components/         # Reusable UI components
│   ├── lib/                # API client and utilities
│   └── configuration files # Next.js, TypeScript, Tailwind
├── README.md               # This file
└── setup.md               # Quick setup guide
```

## Setup Instructions

### Prerequisites
- Node.js (v16 or higher)
- MongoDB (local or MongoDB Atlas)
- npm or yarn

### Backend Setup

1. Navigate to the backend directory:
   ```bash
   cd backend
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Create a `.env` file in the backend directory:
   ```env
   PORT=5000
   MONGODB_URI=mongodb://localhost:27017/doctor-consultation
   JWT_SECRET=your-super-secret-jwt-key
   OTP_SECRET=123456
   ```

4. Start the backend server:
   ```bash
   npm start
   ```

The backend will run on `http://localhost:5000`

### Frontend Setup

1. Navigate to the frontend directory:
   ```bash
   cd frontend
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Create a `.env.local` file in the frontend directory:
   ```env
   NEXT_PUBLIC_API_URL=http://localhost:5000
   ```

4. Start the frontend development server:
   ```bash
   npm run dev
   ```

The frontend will run on `http://localhost:3000`

## API Documentation

### Authentication

#### POST /api/auth/register
Register a new user
```json
{
  "name": "John Doe",
  "email": "john@example.com",
  "password": "password123"
}
```

#### POST /api/auth/login
Login user
```json
{
  "email": "john@example.com",
  "password": "password123"
}
```

### Doctors

#### GET /api/doctors
Get all doctors with optional filters
- Query params: `specialization`, `mode`, `date`, `sortBy`

#### GET /api/doctors/:id
Get doctor details by ID

### Appointments

#### GET /api/appointments
Get user's appointments (requires authentication)
- Query params: `status` (booked/completed/cancelled)

#### POST /api/appointments
Book a new appointment (requires authentication)
```json
{
  "doctorId": "doctor_id",
  "slotId": "slot_id",
  "date": "2024-01-15",
  "time": "10:00"
}
```

#### PUT /api/appointments/:id
Update appointment (reschedule/cancel)
```json
{
  "action": "reschedule",
  "newSlotId": "new_slot_id",
  "newDate": "2024-01-16",
  "newTime": "11:00"
}
```

#### POST /api/appointments/:id/confirm
Confirm appointment with OTP
```json
{
  "otp": "123456"
}
```

### Slots

#### GET /api/slots
Get available slots for a doctor
- Query params: `doctorId`, `date`

## Database Schema

### Users
```javascript
{
  _id: ObjectId,
  name: String,
  email: String,
  password: String (hashed),
  createdAt: Date
}
```

### Doctors
```javascript
{
  _id: ObjectId,
  name: String,
  specialization: String,
  experience: Number,
  mode: String (online/in-person/both),
  rating: Number,
  image: String
}
```

### Slots
```javascript
{
  _id: ObjectId,
  doctorId: ObjectId,
  date: Date,
  time: String,
  isBooked: Boolean,
  isLocked: Boolean,
  lockedUntil: Date,
  appointmentId: ObjectId
}
```

### Appointments
```javascript
{
  _id: ObjectId,
  userId: ObjectId,
  doctorId: ObjectId,
  slotId: ObjectId,
  date: Date,
  time: String,
  status: String (booked/completed/cancelled),
  otp: String,
  otpExpiry: Date,
  createdAt: Date
}
```

## Features Implementation

### Slot Booking Flow
1. User selects a slot
2. Slot is locked for 5 minutes
3. OTP is sent (mock implementation)
4. User confirms with OTP
5. Appointment is confirmed and slot is permanently booked

### Reschedule Flow
1. User can reschedule appointments >24h before
2. Original slot is released
3. New slot is booked
4. Confirmation sent

### Doctor Discovery
- Filter by specialization, mode, availability
- Sort by rating, experience, name
- Real-time availability checking

## Technologies Used

- **Frontend**: React, Next.js, Tailwind CSS
- **Backend**: Node.js, Express, MongoDB, Mongoose
- **Authentication**: JWT
- **Styling**: Tailwind CSS
- **Database**: MongoDB

## Running the Application

1. Start MongoDB service
2. Start backend: `cd backend && npm start`
3. Start frontend: `cd frontend && npm run dev`
4. Open `http://localhost:3000` in your browser

## Sample Data

The application comes with seeded data including:
- Sample doctors with different specializations
- Available slots for the next 7 days
- Mock user accounts for testing
