# Vercel Deployment Guide for EduXperience

This guide will help you deploy your EduXperience application to Vercel with the provided Supabase environment variables.

## Prerequisites

1. **Vercel Account**: Sign up at [vercel.com](https://vercel.com) if you don't have one
2. **GitHub Account**: Your code should be pushed to a GitHub repository
3. **Node.js**: Version 18 or higher (for local testing)

## Step 1: Prepare Your Repository

### 1.1 Push to GitHub
```bash
# Initialize git repository (if not already done)
git init

# Add all files
git add .

# Commit your changes
git commit -m "Initial commit for Vercel deployment"

# Add your GitHub repository as remote
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git

# Push to GitHub
git push -u origin main
```

### 1.2 Verify Project Structure
Ensure your project has these files:
- `package.json` ✅
- `vercel.json` ✅ (created for you)
- `src/` directory with your React app ✅
- `index.html` ✅

## Step 2: Deploy to Vercel

### 2.1 Import Project
1. Go to [vercel.com/dashboard](https://vercel.com/dashboard)
2. Click **"New Project"**
3. Click **"Import Git Repository"**
4. Select your GitHub repository
5. Click **"Import"**

### 2.2 Configure Build Settings
Vercel should automatically detect this as a Vite project. The settings should be:
- **Framework Preset**: Vite
- **Build Command**: `npm run build`
- **Output Directory**: `dist`
- **Install Command**: `npm install`

### 2.3 Set Environment Variables
In the Vercel dashboard, go to your project settings and add these environment variables:

#### Required Environment Variables:
```
VITE_SUPABASE_URL = https://mhukvyjukajzrcqisycs.supabase.co
VITE_SUPABASE_ANON_KEY = eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6Im1odWt2eWp1a2FqenJjcWlzeWNzIiwicm9sZSI6ImFub24iLCJpYXQiOjE3NTQ0NzA3MTgsImV4cCI6MjA3MDA0NjcxOH0.Tvp7AZUB00ZL_4yUJkgJ6SffJ4nQEeeyyv8wD2v1SEk
VITE_PROJECT_ID = mhukvyjukajzrcqisycs
```

#### Optional Environment Variables:
```
VITE_SUPABASE_SERVICE_ROLE_KEY = your_service_role_key_here
```

### 2.4 Deploy
1. Click **"Deploy"**
2. Wait for the build to complete (usually 2-3 minutes)
3. Your app will be available at `https://your-project-name.vercel.app`

## Step 3: Configure Vercel Settings

### 3.1 Domain Configuration (Optional)
1. Go to your project dashboard
2. Click **"Settings"** → **"Domains"**
3. Add your custom domain if you have one

### 3.2 Environment Variables Management
1. Go to **"Settings"** → **"Environment Variables"**
2. Add the same variables for different environments:
   - **Production**: For your live site
   - **Preview**: For pull request previews
   - **Development**: For local development

### 3.3 Build Settings
1. Go to **"Settings"** → **"General"**
2. Verify these settings:
   - **Build Command**: `npm run build`
   - **Output Directory**: `dist`
   - **Install Command**: `npm install`
   - **Development Command**: `npm run dev`

## Step 4: Post-Deployment Configuration

### 4.1 Supabase Configuration
Your Supabase client is already configured to use environment variables. The configuration will automatically use:
- `VITE_SUPABASE_URL` for the Supabase URL
- `VITE_SUPABASE_ANON_KEY` for the anonymous key

### 4.2 CORS Configuration
Make sure your Supabase project allows requests from your Vercel domain:
1. Go to your Supabase dashboard
2. Navigate to **"Settings"** → **"API"**
3. Add your Vercel domain to the allowed origins:
   - `https://your-project-name.vercel.app`
   - `https://your-custom-domain.com` (if applicable)

### 4.3 Database Policies
Ensure your Row Level Security (RLS) policies are properly configured for your production environment.

## Step 5: Testing Your Deployment

### 5.1 Basic Functionality Test
1. Visit your deployed URL
2. Test user registration/login
3. Test course creation (if you're an institution)
4. Test student enrollment
5. Test admin dashboard functionality

### 5.2 Environment Variables Test
Check the browser console to ensure no environment variable errors:
1. Open browser developer tools
2. Check the console for any Supabase configuration errors
3. Verify that the app connects to Supabase successfully

## Step 6: Continuous Deployment

### 6.1 Automatic Deployments
Vercel will automatically deploy when you push to your main branch:
```bash
# Make changes to your code
git add .
git commit -m "Update feature"
git push origin main
# Vercel will automatically deploy the changes
```

### 6.2 Preview Deployments
Every pull request will create a preview deployment:
1. Create a feature branch
2. Make your changes
3. Create a pull request
4. Vercel will create a preview URL for testing

## Troubleshooting

### Common Issues:

#### 1. Build Failures
- Check that all dependencies are in `package.json`
- Ensure TypeScript errors are resolved
- Check the build logs in Vercel dashboard

#### 2. Environment Variables Not Working
- Verify variable names start with `VITE_`
- Check that variables are set in the correct environment (Production/Preview)
- Redeploy after adding new variables

#### 3. Supabase Connection Issues
- Verify CORS settings in Supabase
- Check that RLS policies allow your operations
- Ensure the Supabase URL and keys are correct

#### 4. Routing Issues
- The `vercel.json` file includes a rewrite rule for SPA routing
- If you have custom routes, update the rewrite rules accordingly

### Getting Help:
- Check Vercel's [documentation](https://vercel.com/docs)
- Review build logs in the Vercel dashboard
- Check Supabase logs for database-related issues

## Environment Variables Summary

Here are the environment variables you need to set in Vercel:

| Variable Name | Value | Required |
|---------------|-------|----------|
| `VITE_SUPABASE_URL` | `https://mhukvyjukajzrcqisycs.supabase.co` | ✅ |
| `VITE_SUPABASE_ANON_KEY` | `eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6Im1odWt2eWp1a2FqenJjcWlzeWNzIiwicm9sZSI6ImFub24iLCJpYXQiOjE3NTQ0NzA3MTgsImV4cCI6MjA3MDA0NjcxOH0.Tvp7AZUB00ZL_4yUJkgJ6SffJ4nQEeeyyv8wD2v1SEk` | ✅ |
| `VITE_PROJECT_ID` | `mhukvyjukajzrcqisycs` | ✅ |
| `VITE_SUPABASE_SERVICE_ROLE_KEY` | `your_service_role_key_here` | ❌ |

## Next Steps

1. **Monitor Performance**: Use Vercel Analytics to monitor your app's performance
2. **Set up Monitoring**: Consider adding error tracking (Sentry, LogRocket, etc.)
3. **Backup Strategy**: Ensure your Supabase database is properly backed up
4. **Security**: Regularly rotate your Supabase keys and review RLS policies

Your EduXperience application should now be successfully deployed on Vercel! 🚀
