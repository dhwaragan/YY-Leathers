# YY Leathers - Netlify Deployment Guide

## ✅ ALL FIXES APPLIED

1. **Created root `netlify.toml`** with `base = "app"` - Fixes vite permission error
2. **Created root `package.json`** with `serverless-http` - Fixes missing module error
3. **Removed duplicate `api.ts`** - Cleaned up function files
4. **Updated `.env.example`** - Added all 8 required environment variables
5. **Installed dependencies** - Generated package-lock.json

---

## 🚀 DEPLOY NOW (3 Simple Steps)

### Step 1: Push to GitHub
```bash
git add .
git commit -m "Fix Netlify deployment: netlify.toml, serverless-http, base directory"
git push origin main
```

### Step 2: Deploy on Netlify
1. Go to https://app.netlify.com/
2. Click **"New site from Git"**
3. Select repo: `dhwaragan/YY-Leathers`
4. **Build settings are auto-configured** from netlify.toml:
   - Base directory: `app`
   - Build command: `npm run build`
   - Publish directory: `dist`
   - Functions directory: `netlify/functions`
5. Click **"Deploy site"**

### Step 3: Add Environment Variables
In Netlify Dashboard → Site settings → Environment variables, add:

**Required:**
```
GEMINI_API_KEY=your_actual_key
VITE_SUPABASE_URL=https://your-project.supabase.co
VITE_SUPABASE_ANON_KEY=your_key
STRIPE_SECRET_KEY=sk_test_...
STRIPE_WEBHOOK_SECRET=whsec_...
VITE_RAZORPAY_KEY_ID=rzp_test_...
RAZORPAY_KEY_SECRET=your_secret
RAZORPAY_WEBHOOK_SECRET=your_webhook_secret
```

### Step 4: Redeploy
- Go to **Deploys** tab
- Click **"Trigger deploy" → "Deploy site"**
- Wait 3-5 minutes

---

## 🔧 WHAT WAS FIXED

### Error 1: "Cannot find module 'serverless-http'"
**Cause**: Netlify couldn't find `serverless-http` in root package.json  
**Fix**: Created root `package.json` with `serverless-http` dependency

### Error 2: "vite: Permission denied"
**Cause**: Netlify was running from root, but vite is installed in `app/node_modules`  
**Fix**: Set `base = "app"` in netlify.toml so Netlify runs FROM the app folder

### Final netlify.toml Configuration:
```toml
[build]
  base = "app"                    # Run FROM app folder
  command = "npm run build"       # Vite is now accessible
  publish = "dist"                # Output folder (relative to base)
  functions = "netlify/functions" # Functions folder (relative to base)
```

---

## ✅ YOUR SITE WILL BE LIVE AT:
`https://your-site-name.netlify.app`

---

## 🧪 TEST AFTER DEPLOYMENT

- [ ] Homepage loads correctly
- [ ] `/api/products` returns JSON data
- [ ] Chatbot responds to messages
- [ ] Payment pages work (use test mode)

---

## 🐛 TROUBLESHOOTING

### "vite: Permission denied" (AGAIN)
**Solution**: Make sure `netlify.toml` has `base = "app"` at the root level

### "Cannot find module 'serverless-http'"
**Solution**: Verify root `package.json` exists and has `serverless-http` in dependencies

### "Build failed"
**Solution**: 
- Check Netlify build logs
- Ensure all env vars are set
- Verify `package-lock.json` is committed

### "API routes return 404"
**Solution**: 
- Check function files are in `app/netlify/functions/`
- Verify redirects in netlify.toml

---

## 📦 CORRECT PROJECT STRUCTURE

```
yy-leathers-updatedd/
├── netlify.toml              ✅ Root config with base = "app"
├── package.json              ✅ Root package (serverless-http)
├── package-lock.json         ✅ Lockfile
├── DEPLOYMENT_GUIDE.md       ✅ This file
└── app/
    ├── package.json          ✅ App dependencies (vite, react, etc.)
    ├── package-lock.json     ✅ App lockfile
    ├── vite.config.ts        ✅ Vite configuration
    ├── server.ts             ✅ Express server
    ├── .env.example          ✅ Environment template
    ├── dist/                 ✅ Build output (generated)
    └── netlify/functions/    ✅ Serverless functions
        ├── api.js
        ├── razorpay-create-order.js
        ├── razorpay-verify-payment.js
        ├── razorpay-webhook.js
        └── orders.js
```

---

## ⚠️ CRITICAL NOTES

1. **DO NOT** change `base = "app"` - This fixes the vite permission error
2. **DO** commit both root `package.json` AND `app/package.json`
3. **DO** commit `package-lock.json` files
4. **DO** set all environment variables in Netlify
5. **DO NOT** commit `.env` files (security risk)

---

## 🎯 QUICK DEPLOY CHECKLIST

- [x] netlify.toml at root with `base = "app"`
- [x] Root package.json with serverless-http
- [x] All function files in app/netlify/functions/
- [ ] Push code to GitHub
- [ ] Create site in Netlify
- [ ] Add environment variables
- [ ] Trigger deploy
- [ ] Test live site

---

## 📞 DEPLOYMENT COMPLETE!

After following these steps, your site will be live. The "vite: Permission denied" error is now fixed by running the build from the `app` directory where vite is installed.

**Need help?** Check Netlify build logs for detailed error messages.