# ⚡ QUICKSTART GUIDE

## 🚀 5-Minute Setup

### Step 1: Ensure MongoDB is Running
```bash
# Windows (PowerShell as Admin)
mongod

# Mac
brew services start mongodb-community

# Linux
sudo systemctl start mongod
```

### Step 2: Start Backend (Terminal 1)
```bash
cd backend/campus
npm run dev
# OR
node server.js
```

You should see:
```
🚀 Server started on http://localhost:5000
✅ MongoDB connected successfully
```

### Step 3: Start Frontend (Terminal 2)
```bash
cd frontend
npm start
```

Browser opens automatically on `http://localhost:3000`

---

## 📝 Quick Test Workflow

### 1. **Register as Student**
- Go to `/register`
- Enter: Name, Roll (e.g., 101), Password
- Select Role: **Student**
- Click Register

### 2. **Register as Guard** (Optional)
- Go to `/register`
- Enter: Name, Roll (e.g., guard001), Password
- Select Role: **Guard**
- Click Register

### 3. **Login as Student**
- Go to `/login`
- Enter Roll & Password from step 1
- Click Login → Redirects to **Student Dashboard**

### 4. **Student Dashboard**
- Click "Generate QR Code" → See dynamic QR
- QR refreshes every 60 seconds
- Click "My Profile" → View your information

### 5. **Login as Guard** (Skip if no guard account)
- Login with guard credentials from step 2
- Now on **Guard Dashboard**
- Click "Open Scanner" → Camera opens
- Position student QR in frame → Auto-scans and records

### 6. **Login as Admin**
- Register with admin role during signup
- Login → Redirects to **Admin Dashboard**
- View Students, Guards, Late Logs
- Delete users and manage system

---

## 🔗 Key URLs

| Role | URL | Purpose |
|------|-----|---------|
| Guest | http://localhost:3000 | Login page |
| Student | http://localhost:3000/dashboard | Student home |
| Guard | http://localhost:3000/guard | Guard scanner |
| Admin | http://localhost:3000/admin | Admin panel |
| QR Scanner | http://localhost:3000/scan | Scan attendance |

---

## 🔑 Test Credentials

Create these during registration:

**Student:**
```
Name: John Doe
Roll: 101
Password: student123
```

**Guard:**
```
Name: Guard Singh
Roll: guard001
Password: guard123
```

**Admin:**
```
Name: Admin User
Roll: admin001
Password: admin123
```

---

## ✅ Expected Features

✓ Student can register & login  
✓ Student dashboard shows profile + QR  
✓ Guard can scan QR codes  
✓ Attendance recorded in database  
✓ Admin sees all users & logs  
✓ JWT authentication working  
✓ Bootstrap UI styling applied  

---

## 🐛 Troubleshooting

### Backend won't start?
```bash
# Check if MongoDB is running
mongosh  # Should connect successfully

# Check port 5000 is free
netstat -ano | findstr :5000  # Windows
lsof -i :5000  # Mac/Linux
```

### Frontend shows "Connection refused"?
```bash
# Ensure backend is running on 5000
# Check API URL in src/api/api.js points to http://localhost:5000
```

### QR Scanner not working?
```bash
# Ensure browser has camera permissions
# Try a different browser (Chrome/Edge recommended)
# Check browser console for errors
```

### "Authentication failed"?
```bash
# Register a new account
# Or clear localStorage: localStorage.clear()
# Then login again
```

---

## 📂 Project Files Overview

**Key files modified/created:**

```
✅ backend/campus/
  ├── config/db.js (MongoDB connection)
  ├── routes/authRoutes.js (Login/Register/Delete)
  ├── routes/attendanceRoutes.js (Mark/Get attendance)
  └── server.js (Express setup)

✅ frontend/src/
  ├── components/
  │   ├── Register.js (Multi-role registration)
  │   ├── Login.js (Role-based redirect)
  │   └── Dashboard.js (Student home)
  ├── pages/
  │   ├── ScanQR.js (QR scanner)
  │   ├── GuardDashboard.js (Guard view)
  │   └── AdminDashboard.js (Admin panel)
  ├── api/api.js (Axios with auth)
  └── App.js (All routes)
```

---

## 🎯 Next Steps

1. **Customize branding:**
   - Edit header title in `App.js`
   - Change colors in `App.css`
   - Update alerts in components

2. **Add more features:**
   - Email notifications
   - SMS on late entry
   - Statistics dashboard
   - Export reports to CSV

3. **Deploy to production:**
   - Set up MongoDB Atlas (cloud)
   - Deploy backend to Heroku/Railway
   - Deploy frontend to Vercel/Netlify
   - Set environment variables

4. **Secure endpoints:**
   - Add role-based access control
   - Add rate limiting
   - Add input validation
   - Add logging

---

## 💡 Tips

- Use browser DevTools (F12) to debug
- Check Network tab for API responses
- Use MongoDB Compass to view database
- Keep terminal windows visible for logs
- Test on mobile for camera features

---

**Ready to go!** 🚀 Start with Step 1 above.
