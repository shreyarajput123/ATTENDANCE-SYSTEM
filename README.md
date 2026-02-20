# 🎓 Campus Attendance System - Complete Setup Guide

## 📋 Project Structure

```
Attendance-system/
├── backend/
│   └── campus/
│       ├── config/
│       │   └── db.js (MongoDB connection)
│       ├── middleware/
│       │   └── authMiddleware.js (JWT verification)
│       ├── models/
│       │   ├── user.js
│       │   └── Attendance.js
│       ├── routes/
│       │   ├── authRoutes.js (Register, Login, Delete User)
│       │   └── attendanceRoutes.js (Mark attendance, fetch logs)
│       ├── server.js
│       ├── package.json
│       └── .env
│
└── frontend/
    ├── src/
    │   ├── components/
    │   │   ├── Register.js (Registration with role selection)
    │   │   ├── Login.js (Login with role-based navigation)
    │   │   └── Dashboard.js (Student dashboard)
    │   ├── pages/
    │   │   ├── ScanQR.js (QR scanning for attendance)
    │   │   ├── GuardDashboard.js (Guard view of attendance logs)
    │   │   └── AdminDashboard.js (Admin management panel)
    │   ├── api/
    │   │   └── api.js (Axios instance with token interceptor)
    │   ├── App.js (Main routing)
    │   ├── App.css (Bootstrap-based styling)
    │   └── package.json
```

## 🚀 Features

### 🎓 Student Features
- Create account with roll number
- View personal dashboard
- Generate dynamic QR codes for entry
- Track attendance history

### 👮 Guard Features
- Scan student QR codes
- Record attendance with timestamps
- View all attendance logs for the day
- Real-time entry tracking

### 🔑 Admin Features
- Manage student registrations
- Manage guard accounts
- View complete attendance logs
- Delete users from system
- Dashboard with statistics

## 🛠️ Tech Stack

**Backend:**
- Node.js + Express.js
- MongoDB + Mongoose
- JWT for authentication
- Bcryptjs for password hashing

**Frontend:**
- React.js
- Bootstrap 5 for styling
- Axios for API calls
- html5-qrcode for QR scanning

## 📦 Installation & Setup

### 1. Backend Setup

```bash
cd backend/campus
npm install
```

**Create .env file:**
```
PORT=5000
MONGO_URI=mongodb://127.0.0.1:27017/attendance_system
JWT_SECRET=mysecretkey
```

**Start Backend:**
```bash
npm run dev
# or
node server.js
```

Server runs on: `http://localhost:5000`

### 2. Frontend Setup

```bash
cd frontend
npm install
npm start
```

App runs on: `http://localhost:3000`

## 🔐 Authentication Flow

1. **Registration:**
   - User selects role (Student/Guard/Admin)
   - Fills in name, roll number, password
   - Password is hashed with bcryptjs
   - User saved to MongoDB

2. **Login:**
   - User enters roll number & password
   - Backend verifies credentials
   - JWT token generated and returned
   - Frontend stores token in localStorage
   - User redirected based on role

3. **Protected Routes:**
   - AuthMiddleware checks token validity
   - Only authenticated users can mark attendance
   - Token included in all API calls via interceptor

## 📱 API Endpoints

### Authentication
- `POST /api/auth/register` - Register new user
- `POST /api/auth/login` - Login user
- `GET /api/auth/check-users` - Fetch all users (admin)
- `DELETE /api/auth/user/:id` - Delete user (admin)

### Attendance
- `POST /api/attendance/mark` - Mark attendance with QR
- `GET /api/attendance/logs` - Get logs (authenticated)
- `GET /api/attendance/my-logs` - Get user's logs
- `GET /api/attendance/all-logs` - Get all logs (admin)

## 🎯 User Credentials (For Testing)

After registration, you can test with:

**Student Account:**
- Roll: 101
- Password: student123
- Role: Student

**Guard Account:**
- Name: Guard User
- Roll/Phone: guard001
- Password: guard123
- Role: Guard

**Admin Account:**
- Name: Admin User
- Roll: admin001
- Password: admin123
- Role: Admin

## 🔄 Attendance Workflow

### For Students:
1. Login with roll number
2. Go to Student Dashboard
3. Click "Generate QR Code"
4. Share/scan QR code for entry

### For Guards:
1. Login with guard credentials
2. Go to Guard Dashboard
3. Click "Open Scanner"
4. Scan student QR codes
5. Attendance auto-recorded with timestamp

### For Admins:
1. Login with admin credentials
2. Access Admin Dashboard
3. Manage students/guards
4. View real-time attendance logs
5. Delete or edit user records

## ⚙️ Environment Configuration

**Backend (.env):**
```
PORT=5000
MONGO_URI=mongodb://127.0.0.1:27017/attendance_system
JWT_SECRET=your-secret-key
```

**MongoDB Setup:**
- Ensure MongoDB is running locally
- Or update MONGO_URI to your cloud database (MongoDB Atlas)

```bash
# To start MongoDB locally (Windows)
mongod

# To start MongoDB locally (Mac)
brew services start mongodb-community

# To start MongoDB locally (Linux)
sudo systemctl start mongod
```

## 🐛 Common Issues & Solutions

### Issue: "MongoDB connection error"
**Solution:** Ensure MongoDB is running on localhost:27017 or update MONGO_URI in .env

### Issue: "Token expired - re-login required"
**Solution:** Tokens expire in 7 days. Login again to get new token.

### Issue: "QR Scanner not working"
**Solution:** Ensure camera permissions are granted in browser settings.

### Issue: "CORS errors"
**Solution:** Backend CORS is enabled. Clear browser cache and restart.

## 📊 Database Schema

**User Model:**
- name: String
- roll: String (unique)
- password: String (hashed)
- role: String (student/guard/admin)

**Attendance Model:**
- studentId: ObjectId (ref: User)
- date: String (YYYY-MM-DD)
- time: String (HH:MM:SS)
- qrData: String
- status: String (Present/Late)
- scannedBy: ObjectId (ref: Guard User - optional)
- Index: unique(studentId, date)

## 🚀 Deployment

### Backend (Heroku/Railway):
```bash
# Push to git and deploy
git push heroku main

# Set environment variables on platform
MONGO_URI=your-atlas-url
JWT_SECRET=your-secret
```

### Frontend (Vercel/Netlify):
```bash
npm run build
# Deploy the build folder
```

## 📞 Support

For issues or questions:
1. Check browser console for errors
2. Check backend logs in terminal
3. Verify MongoDB is running
4. Ensure all packages are installed
5. Clear localStorage if experiencing persistent issues

---

**Version:** 1.0.0  
**Last Updated:** February 2026  
**Status:** Production Ready ✅
