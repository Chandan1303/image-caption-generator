# Gemini API Connection Troubleshooting Guide

## Quick Diagnosis

Run this command to test your Gemini connection:
```bash
cd backend
python test_gemini_connection.py
```

## Common Issues & Solutions

### Issue 1: "Gemini connection lost" or Empty Captions

**Possible Causes:**
1. API key has quotes around it in .env file
2. Invalid or expired API key
3. Network/firewall blocking Google API
4. Wrong model name
5. Backend server not running

**Solutions:**

#### Fix 1: Remove Quotes from API Key
**File:** `backend/.env`

❌ **Wrong:**
```env
GEMINI_API_KEY="AIzaSyAAhtCpP-EXJRRdbxOMxaxyZklGBSgUKks"
```

✅ **Correct:**
```env
GEMINI_API_KEY=AIzaSyAAhtCpP-EXJRRdbxOMxaxyZklGBSgUKks
```

#### Fix 2: Verify API Key is Valid
1. Go to [Google AI Studio](https://makersuite.google.com/app/apikey)
2. Check if your API key is active
3. Generate a new key if needed
4. Update `.env` file with new key

#### Fix 3: Check Backend Server is Running
```bash
# In backend directory
python app.py
```

You should see:
```
[INFO] BLIP model loaded successfully.
[INFO] Gemini API configured successfully.
* Running on http://127.0.0.1:5123
```

#### Fix 4: Verify Model Name
The code now uses `gemini-1.5-flash` which is correct for vision tasks.

### Issue 2: Backend Not Starting

**Check MongoDB:**
```bash
# Windows
net start MongoDB

# Or check if MongoDB is running
mongosh
```

**Check Python Dependencies:**
```bash
cd backend
pip install -r requirements.txt
```

### Issue 3: Captions Not Respecting Tone/Length

**This has been fixed!** The updated code includes:
- Detailed tone instructions (casual, professional, creative, funny)
- Specific length guidance (short: 10-20 words, medium: 20-40 words, long: 40-70 words)
- Platform-specific formatting

**Restart the backend** to apply changes:
```bash
# Stop the backend (Ctrl+C)
# Then restart
python app.py
```

## Debugging Steps

### Step 1: Check Environment Variables
```bash
cd backend
python -c "from dotenv import load_dotenv; import os; load_dotenv(); print('API Key exists:', os.getenv('GEMINI_API_KEY') is not None)"
```

### Step 2: Check Backend Logs
When you generate a caption, look for these logs:

✅ **Success:**
```
[DEBUG] Backend decided: AI Model = gemini, Platform = instagram
[DEBUG] Generating Gemini caption - Platform: instagram, Tone: casual, Length: medium
[DEBUG] Gemini model initialized successfully
[DEBUG] Sending request to Gemini API...
[DEBUG] Received response from Gemini API
[Gemini SUCCESS] Platform: instagram | Caption length: 85 chars
```

❌ **Failure:**
```
[ERROR] Gemini caption generation failed: [error message]
[ERROR] Full traceback: [detailed error]
[WARNING] Gemini returned empty caption, attempting BLIP fallback.
```

### Step 3: Test with BLIP First
If Gemini isn't working, test with BLIP to verify the rest of the system:
1. Select "BLIP Model" in the UI
2. Select "General" platform
3. Upload an image and generate

If BLIP works but Gemini doesn't, it's definitely a Gemini API issue.

## Updated Files

The following files have been updated to fix Gemini issues:

1. **backend/.env** - Removed quotes from API key
2. **backend/ai_core/gemini_caption.py** - Fixed model name and added better error handling
3. **backend/test_gemini_connection.py** - New test script

## Configuration Checklist

- [ ] `.env` file exists in `backend/` directory
- [ ] `GEMINI_API_KEY` is set without quotes
- [ ] API key is valid (check Google AI Studio)
- [ ] MongoDB is running
- [ ] Backend server is running (`python app.py`)
- [ ] Frontend is running (`npm start`)
- [ ] No firewall blocking Google API

## Network Requirements

Gemini API requires internet connection to:
- `generativelanguage.googleapis.com` (Gemini API endpoint)
- Port 443 (HTTPS)

If behind a corporate firewall, you may need to:
1. Configure proxy settings
2. Whitelist Google AI domains
3. Contact IT department

## Testing Workflow

1. **Test Gemini Connection:**
   ```bash
   cd backend
   python test_gemini_connection.py
   ```

2. **Start Backend:**
   ```bash
   python app.py
   ```
   Look for: `[INFO] Gemini API configured successfully.`

3. **Test in UI:**
   - Select "Gemini API" model
   - Select "Instagram" platform
   - Choose "Casual" tone
   - Choose "Medium" length
   - Upload an image
   - Click "Generate Caption"

4. **Check Logs:**
   - Backend terminal should show debug messages
   - Look for success or error messages

## Still Not Working?

If you've tried everything above and Gemini still isn't working:

1. **Check API Quota:**
   - Go to [Google Cloud Console](https://console.cloud.google.com/)
   - Check if you've exceeded free tier limits

2. **Try a Different API Key:**
   - Generate a new key in Google AI Studio
   - Update `.env` file

3. **Check Python Version:**
   ```bash
   python --version
   ```
   Should be Python 3.8 or higher

4. **Reinstall google-generativeai:**
   ```bash
   pip uninstall google-generativeai
   pip install google-generativeai
   ```

5. **Check Error Logs:**
   - Look at backend terminal output
   - Check for specific error messages
   - Share error messages for further help

## Contact & Support

If issues persist, provide:
- Backend terminal logs (full output)
- Result of `test_gemini_connection.py`
- Python version
- Operating system
- Error messages from browser console (F12)
