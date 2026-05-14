# 🚀 Career AI - Vercel Deployment Guide

## 📋 **Prerequisites**
- [Vercel account](https://vercel.com/signup) (free)
- [Git](https://git-scm.com/) installed
- Your project pushed to GitHub/GitLab/Bitbucket

## 🔥 **Quick Deployment Steps**

### **Step 1: Prepare Your Repository**
```bash
# Ensure all changes are committed and pushed
git add .
git commit -m "Prepare for Vercel deployment"
git push origin main
```

### **Step 2: Deploy via Vercel Web Interface**

1. **Visit Vercel Dashboard**
   - Go to [vercel.com](https://vercel.com)
   - Sign in with your GitHub account

2. **Import Your Project**
   - Click "New Project"
   - Select your `Career -AI` repository
   - Click "Import"

3. **Configure Build Settings**
   Vercel will auto-detect Vite. Verify these settings:
   - **Framework Preset**: Vite
   - **Build Command**: `npm run build`
   - **Output Directory**: `dist`
   - **Install Command**: `npm install`

### **Step 3: Set Environment Variables**

In Vercel dashboard, go to your project → Settings → Environment Variables:

**Required Variables:**
```
VITE_FIREBASE_API_KEY=your_firebase_api_key
VITE_FIREBASE_AUTH_DOMAIN=your_project.firebaseapp.com
VITE_FIREBASE_PROJECT_ID=your_project_id
VITE_FIREBASE_STORAGE_BUCKET=your_project.appspot.com
VITE_FIREBASE_MESSAGING_SENDER_ID=your_sender_id
VITE_FIREBASE_APP_ID=your_app_id
```

**Optional:**
```
VITE_GEMINI_API_KEY=your_gemini_api_key
```

### **Step 4: Deploy**
- Click "Deploy"
- Wait for build to complete (2-3 minutes)
- Your app will be live at `https://your-project-name.vercel.app`

---

## 🔧 **Alternative: CLI Deployment**

### **Install Vercel CLI**
```bash
npm install -g vercel
```

### **Login and Deploy**
```bash
# Login to Vercel
vercel login

# Deploy (from project directory)
vercel

# Follow the prompts:
# Set up and deploy? [Y/n] Y
# Which scope? Select your account
# Link to existing project? [y/N] N
# What's your project's name? Career -ai
# In which directory is your code located? ./

# Production deployment
vercel --prod
```

---

## ⚙️ **Firebase Configuration for Production**

### **Update Firebase Rules for Production Domain**

1. **Firestore Security Rules** (firestore.rules):
```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    // Allow read/write for authenticated users
    match /{document=**} {
      allow read, write: if request.auth != null;
    }
    
    // Allow anonymous access for demo purposes (remove in production)
    match /users/{userId} {
      allow read, write: if true;
    }
  }
}
```

2. **Add Vercel Domain to Firebase**
   - Go to Firebase Console → Authentication → Settings
   - Add your Vercel domain to "Authorized domains"
   - Example: `https://Career -ai.vercel.app`

---

## 🎯 **Post-Deployment Steps**

### **1. Test Your Deployment**
- Visit your Vercel URL
- Test all features:
  - Landing page loads
  - Onboarding flow works
  - Dashboard displays
  - ChatBot functions
  - Navigation works

### **2. Custom Domain (Optional)**
- In Vercel dashboard → Domains
- Add your custom domain
- Configure DNS records as instructed

### **3. Performance Optimization**
- Vercel automatically handles:
  - CDN caching
  - Gzip compression
  - Image optimization
  - Edge functions

---

## 🔍 **Troubleshooting**

### **Common Issues & Solutions**

**Build Fails:**
```bash
# Check build locally first
npm run build
npm run preview
```

**Environment Variables Not Working:**
- Ensure all VITE_ prefixed variables are set
- Redeploy after adding variables

**Firebase Errors:**
- Check Firebase project is active
- Verify all credentials are correct
- Ensure domain is authorized in Firebase

**404 Errors:**
- Verify `vercel.json` rewrites are configured
- Check React Router setup

---

## 📊 **Monitoring & Analytics**

### **Vercel Analytics (Free)**
- Go to your project → Analytics
- Monitor performance metrics
- Track user interactions

### **Performance Tips**
- Use Vercel's built-in optimization
- Monitor Core Web Vitals
- Enable Edge Functions for better performance

---

## 🎉 **Success Checklist**

- [ ] Repository pushed to Git platform
- [ ] Vercel project created and configured
- [ ] Environment variables set correctly
- [ ] Firebase domains authorized
- [ ] Build completes successfully
- [ ] App loads and functions correctly
- [ ] ChatBot works properly
- [ ] All navigation routes functional

---

**🌟 Your Career AI platform is now live and ready to help users with their career journey!**

**Production URL**: `https://your-project-name.vercel.app`