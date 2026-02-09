# Veridia Hiring Platform

A complete full-stack hiring platform with React frontend and Node.js backend, replacing traditional Google Forms with a professional recruitment system.

## Features

### Complete Full-Stack Implementation

**Frontend (React + TypeScript + Vite):**
- Beautiful, modern UI with 3D animations
- Responsive design for all devices
- Real-time status updates
- Professional form validation
- Smooth user experience

**Backend (Node.js + Express + MongoDB):**
- RESTful API architecture
- JWT authentication
- MongoDB database
- Automated email notifications
- Role-based access control
- Secure password hashing

###  Core Features

1. **Candidate Registration & Login**
   - Email-based authentication
   - JWT token management
   - Secure password hashing

2. **Application Form**
   - Comprehensive form (replaces Google Forms)
   - Personal, professional, and educational details
   - Resume upload support
   - Location and availability tracking

3. **Candidate Dashboard**
   - View all applications
   - Track application status
   - Withdraw applications
   - Update profile

4. **Admin Dashboard**
   - View all applications
   - Filter and search functionality
   - Update application status
   - View detailed candidate profiles
   - Application statistics

5. **Automated Email Notifications**
   - Application submission confirmation
   - Status update notifications
   - Professional HTML email templates

## Quick Start

### Prerequisites
- Node.js (v18+)
- MongoDB (local or Atlas)

### Installation

```bash
# Clone the repository
git clone <your-repo-url>
cd Veridia

# Install frontend dependencies
npm install

# Install backend dependencies
cd backend
npm install
cd ..

# Setup environment variables
# Copy .env.example to .env in both root and backend directories
# Update with your MongoDB URI and other settings

# Start MongoDB (if using local)
# Windows: net start MongoDB
# Mac/Linux: sudo systemctl start mongod

# Start backend server (in one terminal)
cd backend
npm run dev

# Start frontend (in another terminal)
npm run dev
```

The application will be available at:
- **Frontend:** http://localhost:5173
- **Backend API:** http://localhost:5000

## Project Structure

```
Veridia/
├── backend/              # Node.js + Express backend
│   ├── models/          # MongoDB models
│   ├── routes/          # API routes
│   ├── middleware/      # Auth middleware
│   ├── utils/           # Email service
│   └── server.js        # Main server file
├── src/                 # React frontend
│   ├── components/      # React components
│   ├── api-backend.ts   # Backend API client
│   └── App.tsx          # Main app
└── SETUP_GUIDE.md       # Detailed setup instructions
```

##  Configuration

### Backend (.env)
```env
MONGODB_URI=mongodb://localhost:27017/veridia-hiring
JWT_SECRET=your-secret-key
EMAIL_HOST=smtp.gmail.com
EMAIL_USER=your-email@gmail.com
EMAIL_PASSWORD=your-app-password
```

### Frontend (.env)
```env
VITE_API_URL=http://localhost:5000/api
```

##  Documentation

- **[SETUP_GUIDE.md](SETUP_GUIDE.md)** - Complete setup instructions
- **[PROJECT_FEATURES.md](PROJECT_FEATURES.md)** - Feature documentation
- **[backend/README.md](backend/README.md)** - Backend API documentation

##  Tech Stack

### Frontend
- React 19.2.0
- TypeScript
- Vite
- React Router
- Three.js (3D graphics)
- Lucide React (icons)

### Backend
- Node.js
- Express.js
- MongoDB + Mongoose
- JWT Authentication
- Bcrypt (password hashing)
- Nodemailer (email service)

##  Testing

### Register Test Users

**Candidate:**
```
Email: john@example.com
Password: password123
```

**Admin:**
```
Email: hr@veridia.com
Password: admin123
```

*Note: Any email with @veridia.com is automatically assigned admin role*

##  Deployment

### Backend (Render/Railway/Heroku)
1. Push to GitHub
2. Connect repository
3. Set environment variables
4. Deploy

### Frontend (Vercel/Netlify)
1. Push to GitHub
2. Connect repository
3. Set `VITE_API_URL` to your backend URL
4. Deploy

See [SETUP_GUIDE.md](SETUP_GUIDE.md) for detailed deployment instructions.

##  API Endpoints

### Authentication
- `POST /api/auth/register` - Register user
- `POST /api/auth/login` - Login user
- `GET /api/auth/me` - Get current user

### Applications
- `POST /api/applications` - Submit application
- `GET /api/applications` - Get applications
- `PUT /api/applications/:id/status` - Update status (admin)
- `PUT /api/applications/:id/withdraw` - Withdraw application

##  Submission Options

This project fulfills **Option B: Full-Stack Working Hiring Platform**

 All required features implemented:
- Candidate registration and login
- Application form (Google Forms replacement)
- Candidate dashboard
- Admin dashboard
- Automated email notifications

**Plus:** Professional UI/UX design with modern aesthetics!

##  License

MIT License - feel free to use this project for your needs.

##  Support

For setup help, see [SETUP_GUIDE.md](SETUP_GUIDE.md)

For issues:
1. Check MongoDB is running
2. Verify environment variables
3. Check console for errors



