# 🚀 Quick Start Guide

## Get the App Running in 5 Minutes

### Step 1: Install Dependencies (1 minute)
```bash
cd "c:\Users\dell\Documents\MI Docs\Assignment\Abstrabit"
npm install
```

### Step 2: Create Free Supabase Account (2 minutes)
1. Go to https://supabase.com
2. Click "Sign Up"
3. Create a new project
4. Wait for project to be ready
5. Go to Settings > API and copy your URL and `anon` key

### Step 3: Create Database Table
In Supabase, go to SQL Editor and run:

```sql
CREATE TABLE bookmarks (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID NOT NULL REFERENCES auth.users(id) ON DELETE CASCADE,
  url TEXT NOT NULL,
  title TEXT NOT NULL,
  created_at TIMESTAMP WITH TIME ZONE DEFAULT now(),
  UNIQUE(id)
);

CREATE INDEX bookmarks_user_id_idx ON bookmarks(user_id);
```

### Step 4: Setup Google OAuth (1 minute)
1. Go to https://console.cloud.google.com
2. Create a new project
3. Enable Google+ API
4. Create OAuth 2.0 credentials (Web application)
5. Add redirect URI: `http://localhost:3000/auth/callback`
6. Copy your Client ID

### Step 5: Configure Environment Variables (1 minute)
1. Open `.env.local` in your editor
2. Replace the values:

```env
NEXT_PUBLIC_SUPABASE_URL=https://your-project.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=eyJ...
NEXT_PUBLIC_GOOGLE_CLIENT_ID=xxx...
```

### Step 6: Run the App
```bash
npm run dev
```

Open http://localhost:3000 and click "Sign in with Google"

## 🎉 Done!

You now have a fully functional bookmark manager with:
- ✅ Real-time sync across tabs
- ✅ Private bookmarks per user
- ✅ Google login
- ✅ Beautiful UI

## 📚 What's Included

### Pages
- **/** - Login page
- **/bookmarks** - Main app (protected)
- **/auth/callback** - OAuth handler

### Components
- **GoogleSignInButton** - Login button
- **AddBookmark** - Add bookmark form
- **BookmarksList** - Bookmark list with real-time updates

### Features
- Add bookmarks (URL + title)
- Delete bookmarks
- Real-time updates across tabs
- Private bookmarks per user
- Responsive design

## 🆘 Troubleshooting

### "Cannot find module '@supabase/supabase-js'"
```bash
npm install
```

### "Missing environment variables"
- Check `.env.local` exists
- Verify all three NEXT_PUBLIC_* variables are set
- Restart `npm run dev`

### "Google login not working"
- Check redirect URI is `http://localhost:3000/auth/callback`
- Verify Google OAuth credentials in Supabase dashboard
- Check Google Cloud Console has redirect URI configured

### "Bookmarks not appearing"
- Ensure table `bookmarks` exists in Supabase
- Enable Realtime in Supabase for the bookmarks table
- Check browser console (F12) for errors

## 📖 Full Documentation

See `README.md` for:
- Detailed setup instructions
- Project structure explanation
- Deployment to Vercel guide
- Database security policies
- Common issues and solutions

## 🌐 Ready to Deploy?

1. Push to GitHub
2. Go to https://vercel.com
3. Import your GitHub repository
4. Add same environment variables
5. Click Deploy!

See README.md for detailed Vercel deployment steps.

---

Happy bookmarking! 🔖
