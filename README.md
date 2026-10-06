# Canberra Student Favourite Places — deployment guide

## What this version does

- One shared Canberra map
- Students can search for a place
- Students can submit a place, category, recommendation and optional name
- All submissions are stored in a shared Supabase database
- New submissions appear on everyone’s map through Supabase Realtime
- Search/filter by place, category or recommendation
- Mobile-friendly
- Uses OpenStreetMap for the map and Nominatim for place search

## 1. Create the database

1. Go to https://supabase.com/
2. Create a new project.
3. Open **SQL Editor**.
4. Paste everything from `supabase.sql`.
5. Run it.
6. Open **Project Settings → API**.
7. Copy:
   - Project URL
   - anon / publishable key

## 2. Connect the website

Open `index.html`.

Find:

    const SUPABASE_URL = "PASTE_YOUR_SUPABASE_PROJECT_URL_HERE";
    const SUPABASE_ANON_KEY = "PASTE_YOUR_SUPABASE_ANON_KEY_HERE";

Replace the two values with your Supabase Project URL and anon/publishable key.

Do NOT put a Supabase service_role/secret key in the website.

## 3. Test locally

You can use VS Code + Live Server, or any static web server.

Do not open the file with file:// if the browser blocks requests. A local server is better.

## 4. Deploy with Vercel

Option A — easiest:

1. Go to https://vercel.com/
2. Sign in with GitHub.
3. Create a new GitHub repository.
4. Upload `index.html` and `supabase.sql`.
5. Import the repository into Vercel.
6. Deploy.

Because this is a static site, Vercel does not need a build command.

Your result will be a public URL such as:

    https://canberra-student-map.vercel.app

You can then put that link in an ANU/Lodge group chat, QR code or poster.

## 5. Important before public launch

This starter version allows anonymous submissions and immediately publishes them.

For a student community project, I recommend adding moderation before a large public launch:

- add an `approved` column
- public map only shows approved=true
- admin approves submissions in Supabase
- optionally add a simple admin login

The current database intentionally gives anonymous users INSERT but not UPDATE/DELETE permissions.

## 6. Map/geocoding note

The map uses OpenStreetMap tiles and Nominatim search. Keep reasonable usage limits and attribution. If the project becomes popular, move to a dedicated map/geocoding provider such as Mapbox or Google Maps Platform with an API key and usage limits.

## 7. Suggested next features

- ❤️ Like/upvote places
- ⭐ student rating
- “Cheap / under $20”
- “Good for studying”
- “Date spot”
- “Best at night”
- photo upload
- student login / ANU email verification
- moderation dashboard
- top 10 most recommended places
- QR code for posters around Lodge
