# 🚀 Zumbara Math Challenge — Deployment Checklist

## Cloud Leaderboard Setup (Supabase + GitHub Pages)

### ✅ Phase 1: Supabase Project Setup (5 minutes)

- [ ] **Create Supabase Account**
  - Go to https://supabase.com
  - Sign up (GitHub login recommended)
  - Create a new organization

- [ ] **Create Project**
  - Click "New Project"
  - Name: `zumbara-math`
  - Set a strong database password
  - Choose region closest to your users
  - Wait 1-2 minutes for deployment

- [ ] **Create Scores Table**
  - Go to SQL Editor
  - Click "New Query"
  - Run the SQL from `SUPABASE_SETUP.md`
  - Verify: ✓ Success message appears

- [ ] **Get API Credentials**
  - Go to Project Settings → API
  - Copy: **Project URL** (https://xxxxx.supabase.co)
  - Copy: **anon/public key** (long JWT-like string)
  - ⚠️ Keep these safe; the anon key can go in your code

### ✅ Phase 2: Update Code with Credentials

- [ ] **Open `index.html`**
  - Find lines ~1010-1015
  - Locate:
    ```javascript
    const SUPABASE_URL = '';
    const SUPABASE_ANON_KEY = '';
    ```

- [ ] **Paste Your Credentials**
  ```javascript
  const SUPABASE_URL = 'https://your-xxxxx.supabase.co';
  const SUPABASE_ANON_KEY = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...';
  ```

- [ ] **Commit & Push to GitHub**
  ```bash
  git add index.html
  git commit -m "Configure Supabase credentials for cloud leaderboard"
  git push origin main
  ```

### ✅ Phase 3: Deploy & Verify

- [ ] **Wait for GitHub Pages Deployment**
  - Go to your repo → Settings → Pages
  - Check deployment status (usually ~30 seconds)
  - Visit your site URL

- [ ] **Test the App**
  1. Play a game and get a score
  2. Go to Leaderboard tab
  3. Verify your score appears
  4. **No "Local scores only" banner?** ✅ Success!

- [ ] **Test Cross-Device Sync**
  - Play from another browser/device
  - Visit same leaderboard
  - Scores from all devices sync? ✅ Done!

- [ ] **Verify in Supabase**
  - Go to Supabase → Table Editor
  - Click **scores** table
  - See your game data? ✅ All working!

---

## Live Leaderboard Features Now Available

✨ Your app can now:
- **Store scores in the cloud** (not just local storage)
- **Show live leaderboards** across all players
- **Sync across devices** (one player, multiple devices)
- **Track by age group** (if implemented)
- **Handle unlimited players** (Supabase free tier: 500MB storage)

---

## Troubleshooting

| Problem | Solution |
|---------|----------|
| Still see "Local scores only" | Check `SUPABASE_URL` and `SUPABASE_ANON_KEY` are filled in `index.html` — no typos |
| Scores not saving | Check Supabase RLS policies exist — run the SQL again |
| CORS errors in console | Verify your `SUPABASE_URL` ends with `.supabase.co` |
| "Unauthorized" error | Make sure you copied the **anon key**, not **service_role key** |
| Leaderboard loads but shows "Error" | Check browser console (F12) for error messages |

---

## GitHub Pages Deployment Status

- ✅ Repository is public
- ✅ GitHub Pages enabled (automatic with `index.html`)
- ✅ Default branch: `main`
- 🔗 **Your app will be at:** `https://digrassilucas-source.github.io/zumbaramath/`

---

## Next Steps (Optional)

1. **Enable live updates** — Add polling (refetch leaderboard every 2 seconds)
2. **Add animations** — Highlight new scores as they appear
3. **Track players** — Add persistent user ID (localStorage)
4. **Add filters** — Filter by age, date range, or game mode
5. **Add auth** — Make players create accounts

---

## Questions?

Check the comments in `index.html` around the `SUPABASE CONFIG` section — they have detailed code notes!
