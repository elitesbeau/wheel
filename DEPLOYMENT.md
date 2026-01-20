# Market Elites - Test Deployment Guide

## Overview
This repository contains the Market Elites web application with both user-facing and admin interfaces for options trading education and portfolio management.

## Files
- `index.html` - Main user-facing application
- `admin.html` - Admin dashboard for managing signals, users, and analytics

## Test Deployment Options

### Option 1: GitHub Pages (Recommended for Testing)

1. **Enable GitHub Pages**
   - Go to your repository settings
   - Navigate to "Pages" section
   - Select source: Deploy from branch `claude/test-deploy-admin-AwPEf`
   - Select folder: `/` (root)
   - Click Save

2. **Access URLs**
   - User App: `https://elitesbeau.github.io/wheel/`
   - Admin Panel: `https://elitesbeau.github.io/wheel/admin.html`

### Option 2: Local Testing

1. **Using Python:**
   ```bash
   # Python 3
   python -m http.server 8000

   # Python 2
   python -m SimpleHTTPServer 8000
   ```

2. **Using Node.js (http-server):**
   ```bash
   npx http-server -p 8000
   ```

3. **Using PHP:**
   ```bash
   php -S localhost:8000
   ```

4. **Access URLs:**
   - User App: `http://localhost:8000/index.html`
   - Admin Panel: `http://localhost:8000/admin.html`

### Option 3: Netlify Drop

1. Go to [Netlify Drop](https://app.netlify.com/drop)
2. Drag and drop the entire folder
3. Get instant deployment URLs

### Option 4: Vercel

```bash
# Install Vercel CLI
npm i -g vercel

# Deploy
vercel --prod
```

## Admin Panel Features

The admin dashboard (`admin.html`) includes:

- **Dashboard Overview**
  - Total users and growth metrics
  - Premium member conversions
  - Active positions tracking
  - Monthly recurring revenue (MRR)

- **Signal Management**
  - Add, edit, and delete trading signals
  - Manage signal status (active/pending)
  - Track signal performance

- **User Management**
  - View all registered users
  - Manage user plans (Free/Premium)
  - Monitor user activity and positions

- **Analytics**
  - Platform-wide trading statistics
  - Win rate tracking
  - Total premium collected
  - Average position sizing

- **System Settings**
  - Platform mode control (Live/Maintenance/Read-only)
  - Premium pricing configuration
  - Free signal limits
  - System announcements
  - Database management tools

## Testing Checklist

### User App (`index.html`)
- [ ] Legal terms modal appears on first visit
- [ ] Theme toggle (Light/Dark) works
- [ ] Navigation between tabs (Home, Calc, Watch, Signals, Profile)
- [ ] Calculator functionality for CSP and CC
- [ ] Add position manually
- [ ] View positions and close them
- [ ] Profile settings save
- [ ] API key input (Alpaca integration ready)
- [ ] Wheely AI assistant modal
- [ ] Premium upgrade flow

### Admin Panel (`admin.html`)
- [ ] Dashboard loads with mock statistics
- [ ] Tab switching (Signals, Users, Analytics, Settings)
- [ ] Add new signal modal opens and saves
- [ ] Edit/Delete signal buttons work
- [ ] User table displays correctly
- [ ] Toggle user premium status
- [ ] Analytics displays platform metrics
- [ ] Settings can be modified and saved
- [ ] Dark theme UI consistency

## Configuration Notes

### API Integration (Alpaca)
The app is designed to integrate with Alpaca Markets API:
- Users can add API keys in Settings
- Paper trading endpoint: `https://paper-api.alpaca.markets/v2/`
- Live sync functionality available

### Data Storage
- Uses browser localStorage for data persistence
- Key: `meV6`
- Admin panel uses in-memory mock data (can be connected to backend)

### Security Considerations for Production
- [ ] Add authentication for admin panel
- [ ] Implement HTTPS only
- [ ] Secure API key storage (consider backend proxy)
- [ ] Add rate limiting
- [ ] Implement proper session management
- [ ] Add CORS policies
- [ ] Sanitize all user inputs

## Troubleshooting

### Issue: Blank page
- Check browser console for errors
- Ensure JavaScript is enabled
- Try hard refresh (Ctrl+F5)

### Issue: Legal modal won't close
- Click the checkbox and "Accept & Continue" button
- Clear localStorage and reload

### Issue: API connection fails
- Verify API keys are correct
- Check if using Paper trading keys
- Ensure network connectivity

## Next Steps for Production

1. **Backend Setup**
   - Set up database (PostgreSQL/MongoDB)
   - Create REST API for admin operations
   - Implement user authentication (JWT/OAuth)
   - Set up payment processing (Stripe)

2. **Security Hardening**
   - Add admin authentication
   - Implement rate limiting
   - Add input validation
   - Set up logging and monitoring

3. **Feature Enhancements**
   - Real-time data feeds
   - Advanced charting
   - Email notifications
   - Mobile app versions

4. **Analytics Integration**
   - Google Analytics
   - User behavior tracking
   - A/B testing framework

## Support

For issues or questions during testing:
- Check console logs for errors
- Review network tab for API failures
- Test in incognito mode to rule out cache issues

---

**Last Updated:** January 2026
**Version:** 6.0 (Test)
