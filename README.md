# Smart Bookmarks App

A modern bookmark manager built with Next.js, Supabase, and Tailwind CSS. Users can sign in with Google OAuth, create private bookmarks, and see real-time updates across multiple tabs/devices.

## Features

✅ **Google OAuth Authentication** - Secure login with Google (no email/password)
✅ **Private Bookmarks** - Each user's bookmarks are private and isolated
✅ **Real-time Updates** - Changes appear instantly across all open tabs
✅ **Add Bookmarks** - Simple form to add URL + title
✅ **Delete Bookmarks** - Remove bookmarks with one click
✅ **Responsive Design** - Works on desktop and mobile with Tailwind CSS

## Tech Stack

- **Frontend**: Next.js 15 with TypeScript
- **Styling**: Tailwind CSS
- **Authentication**: Supabase Auth (Google OAuth)
- **Database**: Supabase PostgreSQL
- **Realtime**: Supabase Realtime subscriptions
- **Deployment**: Vercel

## Prerequisites

Before getting started, you'll need:

1. **Node.js** (v18 or higher)
2. **npm** or **yarn**
3. **Supabase Account** - Free at [supabase.com](https://supabase.com)
4. **Google OAuth Credentials** - Setup at [Google Cloud Console](https://console.cloud.google.com)

## Setup Instructions

### 1. Setup Supabase Project

1. Go to [supabase.com](https://supabase.com) and create a new project
2. Create a new table called `bookmarks` with the following schema:

```sql
CREATE TABLE bookmarks (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID NOT NULL REFERENCES auth.users(id) ON DELETE CASCADE,
  url TEXT NOT NULL,
  title TEXT NOT NULL,
  created_at TIMESTAMP WITH TIME ZONE DEFAULT TIMEZONE('utc', NOW()),
  UNIQUE(id)
);

-- Create index for faster queries
CREATE INDEX idx_bookmarks_user_id ON bookmarks(user_id);

-- Enable Realtime
ALTER TABLE bookmarks REPLICA IDENTITY FULL;
```

4. Enable Realtime:
   - Go to Replication in the Supabase dashboard
   - Turn on replication for the `bookmarks` table

5. Set up Google OAuth:
   - Go to Authentication > Providers > Google
   - Add your Google OAuth credentials (get them from Google Cloud Console)

### 4. Configure Environment Variables

Create a `.env.local` file in the project root:

```env
NEXT_PUBLIC_SUPABASE_URL=your_supabase_url
NEXT_PUBLIC_SUPABASE_ANON_KEY=your_supabase_anon_key
```

Get these values from your Supabase project settings (API section).

### 5. Run the Development Server

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

## How to Use

1. **Sign In**: Click "Sign in with Google" and authenticate with your Google account
2. **Add Bookmark**: Enter a title and URL, then click "Add Bookmark"
3. **View Bookmarks**: Your bookmarks appear in the list below
4. **Delete**: Click the "Delete" button on any bookmark to remove it
5. **Real-time Sync**: Open the app in multiple tabs to see real-time synchronization

## Deployment on Vercel

### Prerequisites
- A GitHub account with your repository pushed
- A Vercel account

### Steps

1. **Push to GitHub**:
```bash
git push origin main
```

2. **Deploy to Vercel**:
   - Go to [Vercel](https://vercel.com)
   - Click "Import Project"
   - Select your GitHub repository
   - Add environment variables:
     - `NEXT_PUBLIC_SUPABASE_URL`
     - `NEXT_PUBLIC_SUPABASE_ANON_KEY`
   - Click "Deploy"

3. **Update Google OAuth Redirect URL**:
   - In Supabase, go to Authentication > Providers > Google
   - Add your Vercel URL to the authorized redirect URIs (e.g., `https://yourdomain.vercel.app/auth/callback`)

## Problems Faced & Solutions

### 1. **Problem: Bookmarks not appearing in real-time**
**Solution**: 
- Enabled Realtime in Supabase for the bookmarks table
- Changed table replication identity to FULL
- Implemented proper subscription cleanup in React hooks

### 2. **Problem: Auth session not persisting after refresh**
**Solution**:
- Used Supabase's built-in session management
- Called `getSession()` on page mount to check authentication
- Set up auth state listener for proper redirect handling

### 3. **Problem: CORS errors with Supabase**
**Solution**:
- Used Supabase JavaScript client which handles CORS automatically
- Configured Supabase project to allow the Vercel domain

### 4. **Problem: Type errors with TypeScript**
**Solution**:
- Installed proper type definitions for Supabase
- Configured TypeScript strict mode for better type safety

### 5. **Problem: Real-time updates not working across tabs**
**Solution**:
- Used Supabase Realtime's built-in PostgreSQL Changes feature
- Implemented proper channel subscription with user_id filtering
- Added unsubscribe cleanup in useEffect

## Project Structure

```
smart-bookmarks/
├── app/
│   ├── layout.tsx              # Root layout
│   ├── page.tsx                # Login page
│   ├── globals.css             # Global styles
│   ├── bookmarks/
│   │   └── page.tsx            # Main bookmarks page
│   └── auth/
│       └── callback/
│           └── page.tsx        # Auth callback handler
├── components/
│   ├── GoogleSignInButton.tsx   # Google OAuth button
│   ├── AddBookmark.tsx          # Add bookmark form
│   └── BookmarksList.tsx        # Bookmarks list with real-time
├── lib/
│   └── supabase.ts             # Supabase client
├── public/                      # Static assets
├── package.json
├── tsconfig.json
├── tailwind.config.ts
├── postcss.config.js
├── next.config.js
└── .env.example
```

## Development

### Run Tests
```bash
npm run lint
```

### Build for Production
```bash
npm run build
npm start
```

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit changes (`git commit -m 'Add amazing feature'`)
4. Push to branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is open source and available under the MIT License.

## Support

For issues, questions, or suggestions, please open an issue on GitHub or contact the maintainer.

---

**Live Demo**: [Add your Vercel URL here]  
**GitHub Repository**: [Add your GitHub URL here]
