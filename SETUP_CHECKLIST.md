# Setup Checklist

Complete these steps to get your Smart Bookmarks app running:

## Phase 1: Install & Configure (15 minutes)

- [ ] **Install Node Dependencies**
  ```bash
  cd "c:\Users\dell\Documents\MI Docs\Assignment\Abstrabit"
  npm install
  ```
  
- [ ] **Create Supabase Account**
  - [ ] Go to https://supabase.com
  - [ ] Sign up for free
  - [ ] Create a new project
  - [ ] Save your Project URL and Anon Key

- [ ] **Setup Database**
  - [ ] In Supabase SQL Editor, run the bookmarks table creation script
  - [ ] Script is provided in README.md

- [ ] **Setup Google OAuth**
  - [ ] Go to https://console.cloud.google.com
  - [ ] Create new project
  - [ ] Enable Google+ API
  - [ ] Create OAuth 2.0 credentials (Web application)
  - [ ] Add redirect URI: `http://localhost:3000/auth/callback`
  - [ ] Copy your Client ID

- [ ] **Configure .env.local**
  - [ ] Open `.env.local` in the project root
  - [ ] Fill in your Supabase URL (from Settings > API)
  - [ ] Fill in your Supabase Anon Key (from Settings > API)
  - [ ] Fill in your Google Client ID
  - [ ] Save the file

## Phase 2: Verify Setup (5 minutes)

- [ ] **Run Development Server**
  ```bash
  npm run dev
  ```
  
- [ ] **Test Login**
  - [ ] Open http://localhost:3000
  - [ ] Click "Sign in with Google"
  - [ ] Login with your Google account
  - [ ] Should redirect to /bookmarks

- [ ] **Test Adding Bookmark**
  - [ ] Enter a title (e.g., "Google")
  - [ ] Enter a URL (e.g., "https://google.com")
  - [ ] Click "Add Bookmark"
  - [ ] Bookmark should appear in the list

- [ ] **Test Deleting Bookmark**
  - [ ] Click "Delete" on the bookmark you just added
  - [ ] Bookmark should disappear

- [ ] **Test Real-time (Optional)**
  - [ ] Open the same URL in another browser tab/window
  - [ ] Add a bookmark in one tab
  - [ ] Check if it appears instantly in the other tab
  - [ ] No refresh needed!

## Phase 3: Prepare for Deployment (10 minutes)

- [ ] **Create GitHub Repository**
  - [ ] Go to https://github.com/new
  - [ ] Create public repository "smart-bookmarks"
  - [ ] Initialize with no template

- [ ] **Push Code to GitHub**
  ```bash
  cd "c:\Users\dell\Documents\MI Docs\Assignment\Abstrabit"
  git init
  git add .
  git commit -m "Initial commit: Smart Bookmarks App"
  git remote add origin https://github.com/YOUR_USERNAME/smart-bookmarks.git
  git branch -M main
  git push -u origin main
  ```

## Phase 4: Deploy to Vercel (10 minutes)

- [ ] **Create Vercel Account**
  - [ ] Go to https://vercel.com
  - [ ] Sign up (can use GitHub)

- [ ] **Deploy Project**
  - [ ] Click "Import Project"
  - [ ] Select your GitHub repository
  - [ ] Click "Import"

- [ ] **Configure Environment Variables**
  - [ ] In Vercel dashboard, go to Settings > Environment Variables
  - [ ] Add `NEXT_PUBLIC_SUPABASE_URL`
  - [ ] Add `NEXT_PUBLIC_SUPABASE_ANON_KEY`
  - [ ] Add `NEXT_PUBLIC_GOOGLE_CLIENT_ID`
  - [ ] Click "Deploy"

- [ ] **Update Google OAuth**
  - [ ] In Google Cloud Console, add your Vercel URL
  - [ ] Redirect URI: `https://your-vercel-url.vercel.app/auth/callback`

- [ ] **Update Supabase Settings**
  - [ ] In Supabase, go to Authentication > URL Configuration
  - [ ] Add your Vercel URL to Site URL

- [ ] **Test Live Deployment**
  - [ ] Open your Vercel URL
  - [ ] Test login with Google
  - [ ] Test adding/deleting bookmarks
  - [ ] Share your live URL!

## 🎉 You're Done!

Your Smart Bookmarks app is now:
- ✅ Running locally on http://localhost:3000
- ✅ Deployed live on Vercel
- ✅ Ready for users!

## 📝 What to Submit

According to the assignment, submit:
1. **Live Vercel URL** - Your deployed app
2. **GitHub Repository** - Your public repo with the code
3. **README.md** - Already included in the project

## 🆘 Need Help?

### Common Issues:

**"Cannot connect to Supabase"**
- Check `.env.local` has correct credentials
- Verify credentials from Supabase > Settings > API

**"Google login not working"**
- Check redirect URI is exactly: `http://localhost:3000/auth/callback`
- In Supabase, verify Google OAuth is enabled
- In Google Cloud, verify redirect URI is configured

**"Bookmarks not saving"**
- Check bookmarks table exists in Supabase
- Check RLS policies are disabled initially (or properly configured)
- Check browser console (F12) for errors

**"npm install fails"**
- Delete `node_modules` and `package-lock.json`
- Run `npm install` again
- Make sure Node.js 18+ is installed

## 📚 More Information

- See `README.md` for full documentation
- See `QUICK_START.md` for quick reference
- See `PROJECT_SETUP.md` for technical details

---

✨ Good luck with your deployment! 🚀
