# 🧟 Zumbara Math Challenge — Supabase Cloud Setup

This guide helps you set up Supabase for cloud-based leaderboard syncing.

## Quick Setup (3 minutes)

### 1️⃣ Create a Free Supabase Project

1. Go to **[supabase.com](https://supabase.com)**
2. Click **Sign Up** (use your GitHub account for easier auth)
3. Create a new organization (or use default)
4. Click **New Project**
5. Fill in:
   - **Name**: `zumbara-math`
   - **Database Password**: Create a strong password (you won't need it again)
   - **Region**: Choose closest to you
6. Wait ~1-2 minutes for deployment ✅

---

### 2️⃣ Create the Scores Table

Once your project is ready:

1. Go to **SQL Editor** (left sidebar)
2. Click **New Query**
3. Copy & paste this SQL:

```sql
create table scores (
  id        bigserial primary key,
  username  text    not null,
  age       integer,
  score     integer,
  wrong     integer,
  "runMs"   integer,
  ts        bigint
);

alter table scores enable row level security;

create policy "anon_select" on scores 
  for select using (true);

create policy "anon_insert" on scores 
  for insert with check (true);
```

4. Click **Run** (or press `Ctrl+Enter`)
5. You should see: `✓ Success. No rows returned` ✅

---

### 3️⃣ Get Your API Keys

1. Click **Project Settings** (bottom left gear icon)
2. Go to **API** tab
3. Copy these two values:
   - **Project URL** — looks like: `https://xxxxxxxxxxxxx.supabase.co`
   - **anon / public key** — long string starting with `eyJh...`

**Never share these publicly!** (Well, the `anon` key is meant to be public, but good practice)

---

### 4️⃣ Add Keys to index.html

Open `index.html` in your repo and find this section (around line 1010-1015):

```javascript
const SUPABASE_URL = '';
const SUPABASE_ANON_KEY = '';
```

Replace with your actual credentials:

```javascript
const SUPABASE_URL = 'https://your-project-xxxxx.supabase.co';
const SUPABASE_ANON_KEY = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...';
```

---

### 5️⃣ Deploy & Test

1. Commit and push your changes to GitHub
2. Wait ~30 seconds for GitHub Pages to redeploy
3. Open your Zumbara Math site
4. Play a game
5. Click **Leaderboard** → should show your score
6. **Play from another device** — your score syncs! ☁️

---

## Verify It's Working

### In Supabase:
1. Go to **Table Editor**
2. Click the **scores** table
3. You should see rows appearing as you play

### On Your Site:
1. Leaderboard should show **"⚠ Local scores only"** banner disappears
2. Scores persist across browser sessions
3. Different devices/browsers see same leaderboard

---

## Troubleshooting

| Issue | Fix |
|-------|-----|
| "Local scores only" banner still shows | Check `SUPABASE_URL` and `SUPABASE_ANON_KEY` are filled in `index.html` |
| Scores not saving | Check RLS policies in Supabase SQL Editor — run the policy creation SQL again |
| CORS error in console | Make sure you're using the correct Project URL (with `.supabase.co` domain) |
| "Unauthorized" error | Verify the `anon` key is in `SUPABASE_ANON_KEY`, not the `service_role` key |

---

## What's Happening?

- **Scores Table**: Stores username, age, score, wrong answers, run duration, timestamp
- **Row Level Security (RLS)**: Allows anyone to read all scores, anyone to submit new scores
- **anon Key**: Limited read/write access — safe to use in frontend code
- **GitHub Pages**: Your site stays fully static, Supabase handles the backend

---

## What's Next?

- 🏆 Add filtering by age/date ranges
- 📊 Add charts/analytics
- 🔐 Add authentication if you want user accounts
- 🎯 Add per-game leaderboards

Enjoy! 🧟‍♂️
