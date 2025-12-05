# Quick Start Guide

## Prerequisites
- Python 3.8+
- Node.js 14+
- MongoDB running locally or connection string

## Setup Instructions

### 1. Backend Setup

```bash
# Navigate to backend directory
cd backend

# Create virtual environment (if not exists)
python -m venv venv

# Activate virtual environment
# Windows:
venv\Scripts\activate
# Mac/Linux:
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt

# Configure environment variables
# Create/edit .env file with:
# MONGO_URI=your_mongodb_connection_string
# GEMINI_API_KEY=your_gemini_api_key

# Start the backend server
python app.py
```

Backend will run on: http://localhost:5123

### 2. Frontend Setup

```bash
# Navigate to frontend directory
cd frontend

# Install dependencies (if not already done)
npm install

# Start the development server
npm start
```

Frontend will run on: http://localhost:3000

## Testing the Authentication

### Sign Up (New User)
1. Click on "Sign Up" tab
2. Fill in:
   - Username: testuser
   - Email: test@example.com
   - Password: Test123!
   - Confirm Password: Test123!
   - Security Question: (select one)
   - Security Answer: (your answer)
3. Click "Create Account"
4. Wait for success message
5. You'll be redirected to Sign In

### Sign In
1. Enter your username or email
2. Enter your password
3. Click "Sign In"
4. You'll be redirected to the home page

### Forgot Password
1. Click "Forgot Password?"
2. Enter your email
3. Click "Continue"
4. Answer your security question
5. Enter new password
6. Click "Reset Password"
7. Sign in with new password

## Features to Test

✅ Sign Up with validation
✅ Sign In with username or email
✅ Password visibility toggle
✅ Forgot password flow
✅ Security question recovery
✅ Error handling
✅ Loading states
✅ Responsive design (resize browser)
✅ Form validation
✅ Success/error messages

## Troubleshooting

### Backend Issues
- **Port 5123 already in use**: Kill the process or change port in app.py
- **MongoDB connection error**: Check MONGO_URI in .env
- **Module not found**: Reinstall requirements.txt

### Frontend Issues
- **Port 3000 already in use**: Kill the process or use different port
- **API connection error**: Ensure backend is running on port 5123
- **Module not found**: Run `npm install`

## Project Structure

```
ai-captioning-project/
├── backend/
│   ├── app.py              # Flask application
│   ├── routes/
│   │   └── auth.py         # Authentication routes
│   └── requirements.txt
├── frontend/
│   ├── src/
│   │   ├── App.js          # Main app component
│   │   ├── components/
│   │   │   ├── AuthPage.jsx      # New auth component
│   │   │   ├── AuthPage.css      # Auth styles
│   │   │   ├── HomePage.jsx      # Home page
│   │   │   ├── DashboardPage.jsx # Dashboard
│   │   │   └── ImageUploaderPage.jsx
│   │   └── index.css
│   └── package.json
└── AUTHENTICATION_UPGRADE.md
```

## Next Steps

After successful authentication:
1. Explore the Home page
2. Click "Get Started" to access Dashboard
3. Upload images for AI caption generation
4. Test different caption styles

## Support

For issues or questions:
- Check the AUTHENTICATION_UPGRADE.md for detailed documentation
- Review backend logs in terminal
- Check browser console for frontend errors
- Ensure all dependencies are installed
