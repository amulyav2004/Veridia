# Veridia Hiring Platform - Full-Stack Setup Guide

## Architecture Overview

This is a complete full-stack application with:
- **Frontend:** React + TypeScript + Vite
- **Backend:** Node.js + Express + MongoDB
- **Authentication:** JWT (JSON Web Tokens)
- **Email:** Nodemailer
- **Database:** MongoDB

---

## Prerequisites

Before you begin, ensure you have installed:
- **Node.js** (v18 or higher) - [Download](https://nodejs.org/)
- **MongoDB** (v6 or higher) - [Download](https://www.mongodb.com/try/download/community)
  - OR use **MongoDB Atlas** (cloud) - [Sign up free](https://www.mongodb.com/cloud/atlas/register)
- **Git** - [Download](https://git-scm.com/)

---

## Quick Start

### 1. Install MongoDB (Local Setup)

**Windows:**
```bash
# Download and install MongoDB Community Server
# Start MongoDB service
net start MongoDB
```

**OR use MongoDB Atlas (Cloud - Recommended for deployment):**
1. Create free account at https://www.mongodb.com/cloud/atlas/register
2. Create a new cluster
3. Get your connection string (looks like: `mongodb+srv://username:password@cluster.mongodb.net/`)

### 2. Backend Setup

```bash
# Navigate to backend directory
cd backend

# Install dependencies
npm install

# Create .env file from example
copy .env.example .env

# Edit .env file with your settings:
# - Set MONGODB_URI (local or Atlas)
# - Set JWT_SECRET (any random string)
# - Set email credentials (optional for testing)

# Start backend server
npm run dev
```

Backend will run on: **http://localhost:5000**

### 3. Frontend Setup

```bash
# Navigate to frontend directory (root)
cd ..

# Install dependencies (if not already done)
npm install

# Create .env file
copy .env.example .env

# Start frontend development server
npm run dev
```

Frontend will run on: **http://localhost:5173**

---

## 🔧 Configuration

### Backend (.env)

```env
# MongoDB
MONGODB_URI=mongodb://localhost:27017/veridia-hiring
# OR for MongoDB Atlas:
# MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/veridia-hiring

# JWT
JWT_SECRET=your-super-secret-key-change-this
JWT_EXPIRE=7d

# Email (Gmail example)
EMAIL_HOST=smtp.gmail.com
EMAIL_PORT=587
EMAIL_USER=your-email@gmail.com
EMAIL_PASSWORD=your-app-specific-password
EMAIL_FROM=Veridia Hiring <noreply@veridia.com>

# Frontend URL
FRONTEND_URL=http://localhost:5173
```

### Frontend (.env)

```env
VITE_API_URL=http://localhost:5000/api
```

---

## Email Setup (Optional but Recommended)

### Using Gmail:

1. **Enable 2-Factor Authentication** on your Google account
2. **Generate App Password:**
   - Go to: https://myaccount.google.com/apppasswords
   - Select "Mail" and "Other (Custom name)"
   - Copy the 16-character password
3. **Update backend .env:**
   ```env
   EMAIL_USER=your-email@gmail.com
   EMAIL_PASSWORD=your-16-char-app-password
   ```

### Alternative Email Services:
- **SendGrid** (recommended for production)
- **AWS SES**
- **Mailgun**
- **Postmark**

---

## Testing the Application

### 1. Register a Candidate
1. Go to http://localhost:5173
2. Click "Get Started"
3. Register with any email (e.g., `john@example.com`)
4. You'll be logged in as a **Candidate**

### 2. Register an Admin
1. Logout
2. Register with `@veridia.com` email (e.g., `hr@veridia.com`)
3. You'll be logged in as an **Admin**

### 3. Test Application Flow
1. As **Candidate:**
   - Submit a job application
   - View your applications in dashboard
   - Check email for confirmation (if configured)

2. As **Admin:**
   - View all applications
   - Filter and search applications
   - Update application status
   - View statistics

---

## Project Structure

```
Veridia/
├── backend/                    # Backend API
│   ├── models/                # MongoDB models
│   │   ├── User.js           # User schema
│   │   └── Application.js    # Application schema
│   ├── routes/               # API routes
│   │   ├── auth.js          # Authentication routes
│   │   └── applications.js  # Application routes
│   ├── middleware/          # Express middleware
│   │   └── auth.js         # JWT authentication
│   ├── utils/              # Utility functions
│   │   └── email.js       # Email service
│   ├── server.js          # Main server file
│   ├── package.json       # Backend dependencies
│   └── .env              # Backend configuration
│
├── src/                      # Frontend source
│   ├── components/          # React components
│   ├── api-backend.ts      # Backend API client
│   ├── api.ts             # LocalStorage API (legacy)
│   ├── types.ts           # TypeScript types
│   └── App.tsx           # Main app component
│
├── package.json            # Frontend dependencies
└── .env                   # Frontend configuration
```

---

## API Endpoints

### Authentication
- `POST /api/auth/register` - Register new user
- `POST /api/auth/login` - Login user
- `GET /api/auth/me` - Get current user

### Applications
- `POST /api/applications` - Submit application
- `GET /api/applications` - Get all applications (filtered by role)
- `GET /api/applications/:id` - Get single application
- `PUT /api/applications/:id/status` - Update status (admin only)
- `PUT /api/applications/:id/withdraw` - Withdraw application
- `GET /api/applications/stats/overview` - Get statistics (admin only)

---

## Switching Between LocalStorage and Backend

The project includes both implementations:

**Use Backend API (Recommended):**
```typescript
// In src/App.tsx, change import:
import { api } from './api-backend';
```

**Use LocalStorage (Demo/Offline):**
```typescript
// In src/App.tsx, change import:
import { api } from './api';
```

---

## Deployment

### Backend Deployment (Render/Railway/Heroku)

1. **Push code to GitHub**
2. **Create new Web Service** on Render/Railway
3. **Set environment variables:**
   - `MONGODB_URI` (use MongoDB Atlas)
   - `JWT_SECRET`
   - `EMAIL_*` variables
   - `FRONTEND_URL` (your deployed frontend URL)
4. **Build command:** `npm install`
5. **Start command:** `npm start`

### Frontend Deployment (Vercel/Netlify)

1. **Push code to GitHub**
2. **Connect repository** to Vercel/Netlify
3. **Set environment variable:**
   - `VITE_API_URL=https://your-backend-url.com/api`
4. **Build command:** `npm run build`
5. **Publish directory:** `dist`

---

## Troubleshooting

### MongoDB Connection Error
```
Error: connect ECONNREFUSED 127.0.0.1:27017
```
**Solution:** Make sure MongoDB is running
```bash
# Windows
net start MongoDB

# Mac/Linux
sudo systemctl start mongod
```

### CORS Error
```
Access to fetch has been blocked by CORS policy
```
**Solution:** Check `FRONTEND_URL` in backend `.env` matches your frontend URL

### Email Not Sending
**Solution:** 
- Check email credentials in `.env`
- For Gmail, use App Password (not regular password)
- Check spam folder

### Port Already in Use
```
Error: listen EADDRINUSE: address already in use :::5000
```
**Solution:** Change `PORT` in backend `.env` or kill the process using that port

---

## Database Schema

### User Collection
```javascript
{
  _id: ObjectId,
  name: String,
  email: String (unique),
  password: String (hashed),
  role: String (candidate/admin),
  createdAt: Date
}
```

### Application Collection
```javascript
{
  _id: ObjectId,
  userId: ObjectId (ref: User),
  fullName: String,
  email: String,
  phone: String,
  role: String,
  experience: String,
  skills: String,
  educationType: String,
  course: String,
  collegeName: String,
  score: String,
  country: String,
  state: String,
  city: String,
  noticePeriod: String,
  workMode: String,
  resumeUrl: String,
  portfolioUrl: String,
  notes: String,
  status: String (pending/accepted/rejected/interview/withdrawn),
  submittedAt: Date,
  updatedAt: Date
}
```

---

## Features Checklist

✅ **Backend:**
- [x] RESTful API with Express
- [x] MongoDB database integration
- [x] JWT authentication
- [x] Password hashing (bcrypt)
- [x] Email notifications (Nodemailer)
- [x] Role-based access control
- [x] Input validation
- [x] Error handling
- [x] CORS configuration

✅ **Frontend:**
- [x] React + TypeScript
- [x] API integration
- [x] Authentication flow
- [x] Protected routes
- [x] Form validation
- [x] Real-time updates
- [x] Responsive design

---

## Notes

- **Default Admin:** Any email with `@veridia.com` is automatically assigned admin role
- **Password Requirements:** Minimum 6 characters
- **File Uploads:** Resume upload feature is ready for integration (use Multer middleware)
- **Email Templates:** Professional HTML templates included in `backend/utils/email.js`

---

## Support

For issues or questions:
1. Check this README
2. Review error logs in console
3. Check MongoDB connection
4. Verify environment variables

---

## You're All Set!

Your full-stack Veridia Hiring Platform is now ready to use!

**Test the complete flow:**
1. Start MongoDB
2. Start backend (`cd backend && npm run dev`)
3. Start frontend (`npm run dev`)
4. Register as candidate and admin
5. Submit applications
6. Manage applications as admin
7. Check email notifications



