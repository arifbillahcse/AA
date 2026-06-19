# Birthday Website - EmailJS & Google Sheets Setup Guide

## Overview
This guide helps you set up email notifications and activity logging for Asma's birthday website.

---

## ⚡ Quick Reference Card

### EmailJS Credentials Location
```
Dashboard (https://dashboard.emailjs.com/)
    ├─ Email Services → [Your Service] → Copy Service ID
    └─ Account (Profile Icon) → API Keys → Copy Public Key
```

### What You Need
```
SERVICE ID:   service_abc123xyz...
PUBLIC KEY:   1a2b3c4d5e6f7g8h...
TEMPLATE ID:  template_asma_updates
```

### Google Form Entry IDs Location
```
Google Form (https://forms.google.com)
    ├─ Right-click → Inspect (F12)
    ├─ Search for: entry.
    └─ Copy numbers: entry.1234567890
```

---

## 📧 EmailJS Setup (for Email Notifications)

### Step 1: Create EmailJS Account
1. Visit [emailjs.com](https://www.emailjs.com)
2. Click "Sign Up Free"
3. Create account with your email
4. Verify your email

### Step 2: Create Email Service
1. Go to "Email Services" in dashboard
2. Click "Connect new service"
3. Choose your email provider (Gmail, Outlook, etc.)
4. Authorize access and connect

### Step 3: Create Email Template
1. Go to "Email Templates"
2. Click "Create New Template"
3. Name: `template_asma_updates`
4. Use this template:

```
Subject: 🎁 Asma's Birthday Website - Activity Update

Hello!

Asma interacted with the birthday website:

Activity Type: {{activity_type}}
Details: {{activity_details}}
Time: {{timestamp}}
Source: {{website_url}}

---
This is an automated notification from the birthday website.
```

5. Save template

### Step 4: Get Your Credentials

#### Method 1: From Dashboard (Recommended)
1. Go to https://dashboard.emailjs.com/
2. Login with your EmailJS account
3. Look at the left sidebar
4. Click on **"Account"** or **"Settings"**
5. You'll see:
   - **Service ID** under "Email Services" section
   - **Public Key** under "API Keys" section (top right corner)

#### Method 2: From API Documentation
1. Go to https://dashboard.emailjs.com/
2. Click **"API Documentation"** tab
3. In the code example, you'll see:
   ```javascript
   emailjs.init("YOUR_PUBLIC_KEY");
   ```
   - The key shown here is your **Public Key**

#### Method 3: From Integration Page
1. Go to https://dashboard.emailjs.com/
2. Click **"Email Services"** 
3. Click on your connected email service (Gmail/Outlook)
4. The **Service ID** is shown in blue text
5. Go to **"Admin"** → **"API Keys"** for **Public Key**

#### Where to Find Them:
| Credential | Location |
|-----------|----------|
| **Service ID** | Dashboard → Email Services → Copy the ID in blue |
| **Public Key** | Dashboard → Account → API Keys (top right) OR Admin → API Keys |

#### Example of What They Look Like:
```
Service ID:  service_abc123xyz789def
Public Key:  1a2b3c4d5e6f7g8h9i0j
```

### Step 5: Update Code
Open `index.html` and find the `EMAIL_CONFIG` section (around line 1909):

```javascript
const EMAIL_CONFIG = {
    emailJSServiceID: 'service_asma_birthday', // ← Replace with your Service ID
    emailJSTemplateID: 'template_asma_updates', // ← Template name
    emailJSPublicKey: 'YOUR_EMAILJS_PUBLIC_KEY', // ← Replace with Public Key
    recipientEmail: 'csearif2002@gmail.com' // ← Can change to different email
};
```

**Example:**
```javascript
const EMAIL_CONFIG = {
    emailJSServiceID: 'service_abc123xyz789',
    emailJSTemplateID: 'template_asma_updates',
    emailJSPublicKey: '1234567890abcdefghij',
    recipientEmail: 'csearif2002@gmail.com'
};
```

---

## 📊 Google Sheets Setup (for Activity Logging)

### Step 1: Create Google Form
1. Visit [forms.google.com](https://forms.google.com)
2. Click "Create new form" (+ icon)
3. Name: "Birthday Website Activity Log"
4. Add 4 short answer questions:
   - **Question 1:** "Timestamp"
   - **Question 2:** "Activity Type"
   - **Question 3:** "Activity Details"
   - **Question 4:** "User Info"

### Step 2: Get Form Submission URL
1. Click "Send" button (top right)
2. Click "<>" (Embed code icon)
3. Copy the form action URL from the iframe src
   - It looks like: `https://docs.google.com/forms/u/0/d/e/YOUR_FORM_ID/formResponse`
4. Keep this URL, you'll need it

### Step 3: Get Field Entry IDs
1. Inspect the form with browser DevTools (F12)
2. Look for input fields with name patterns like `entry.1234567890`
3. Or use this method:
   - Right-click form → "Inspect"
   - Search for `entry.` in the HTML
   - Copy the numbers after `entry.`

**You need 4 entry IDs:**
- Entry ID 1: for Timestamp
- Entry ID 2: for Activity Type  
- Entry ID 3: for Activity Details
- Entry ID 4: for User Info

### Step 4: Update Code
Open `index.html` and find the `GOOGLE_SHEETS_CONFIG` section (around line 1923):

```javascript
const GOOGLE_SHEETS_CONFIG = {
    formURL: 'https://docs.google.com/forms/u/0/d/e/YOUR_FORM_ID/formResponse',
    entryMappings: {
        timestamp: '1234567890',    // ← Replace with actual entry ID
        activity: '1234567891',      // ← Replace with actual entry ID
        details: '1234567892',       // ← Replace with actual entry ID
        userInfo: '1234567893'       // ← Replace with actual entry ID
    }
};
```

**Example:**
```javascript
const GOOGLE_SHEETS_CONFIG = {
    formURL: 'https://docs.google.com/forms/u/0/d/e/1FAIpQLSd_abc123xyz/formResponse',
    entryMappings: {
        timestamp: '1234567890',
        activity: '1234567891',
        details: '1234567892',
        userInfo: '1234567893'
    }
};
```

### Step 5: View Responses
1. In Google Form, click "Responses" tab
2. Click the green Sheets icon to view in Google Sheets
3. A new spreadsheet will be created with all logged activities
4. Column A: Timestamps
5. Column B: Activity Types
6. Column C: Details (JSON format)
7. Column D: User Agent Info

---

## 🎯 Tracked Activities

The website automatically tracks:

| Activity | Details |
|----------|---------|
| **page_visit** | When someone visits the website |
| **gift_selected** | When Asma selects a gift (with gift name) |
| **gift_deselected** | When Asma deselects a gift |
| **aunty_gift_selected** | When Maa's gift is selected |
| **aunty_gift_deselected** | When Maa's gift is deselected |
| **quiz_answer_correct** | When quiz answer is correct |
| **quiz_answer_wrong** | When quiz answer is wrong |
| **bucket_item_completed** | When bucket list item is checked |
| **bucket_item_unchecked** | When bucket list item is unchecked |
| **mystery_guess_submitted** | When mystery gift guess is submitted |
| **open_when_card_opened** | When an open-when card is opened |

---

## 🧪 Testing

### Check Console Logs
1. Open website in browser
2. Press F12 to open DevTools
3. Go to "Console" tab
4. You should see logs like:
   ```
   ✅ EmailJS initialized
   📝 Activity tracked: {activity, timestamp, ...}
   ✅ Email sent successfully
   ✅ Data logged to Google Sheets
   ```

### Test Email Notification
1. Make sure EmailJS is configured
2. Interact with website (select a gift)
3. Check if email arrives at `recipientEmail`
4. Email contains activity details and timestamp

### Test Google Sheets
1. Make sure Google Sheets is configured
2. Interact with website (answer quiz, check bucket list)
3. Go to Google Sheets linked to form
4. Check if new rows appear in real-time

---

## ⚙️ Configuration Checklist

- [ ] EmailJS account created
- [ ] Email service connected
- [ ] Email template created (`template_asma_updates`)
- [ ] Service ID copied to `EMAIL_CONFIG`
- [ ] Public Key copied to `EMAIL_CONFIG`
- [ ] Recipient email set in `EMAIL_CONFIG`
- [ ] Google Form created
- [ ] Form submission URL copied
- [ ] 4 entry IDs found
- [ ] Entry IDs copied to `GOOGLE_SHEETS_CONFIG`
- [ ] Website tested in browser console
- [ ] Email notification tested
- [ ] Google Sheets data tested

---

## 🔒 Security Notes

- **Public Key**: Your EmailJS public key is visible in code (it's meant to be public)
- **Google Form**: Form URL and entry IDs are visible in code (they're meant to be public)
- **Email**: Recipient email is visible in code (you can change it)
- **No Secrets**: This setup doesn't store passwords or private keys in code

---

## 🐛 Troubleshooting

### Can't find Service ID or Public Key?
1. **Make sure you're logged in** to https://dashboard.emailjs.com/
2. **Service ID Location:**
   - Go to "Email Services"
   - Click on your email service (Gmail/Outlook/etc)
   - Service ID is shown in blue text
   - Example: `service_abc123xyz`

3. **Public Key Location:**
   - Click on your **profile icon** (top right)
   - Select **"Account"** 
   - Scroll down to **"API Keys"** section
   - Or: Go to **Admin** → **API Keys**
   - Example: `1a2b3c4d5e6f7g8h`

4. **Still can't find it?**
   - Try clearing browser cache
   - Log out and log back in
   - Try a different browser
   - Check spam/promotions folder for EmailJS setup email

### EmailJS not sending emails?
- Check Public Key is correct (no extra spaces)
- Check Service ID is correct (no extra spaces)
- Check Template ID is correct (`template_asma_updates`)
- Check email service is **connected** in EmailJS dashboard (green checkmark)
- Check Template **exists** (go to "Email Templates")
- Look at browser console (F12) for errors
- Wait 30 seconds after configuration before testing

### Google Sheets not receiving data?
- Check Form URL is correct
- Check entry IDs match your form fields
- Make sure form is published (not in edit mode)
- Check browser console for errors
- Google Forms may take 1-2 seconds to receive data

### No console logs appearing?
- Make sure DevTools console is open (F12)
- Refresh the page and interact again
- Check that code changes were saved

---

## 📚 Useful Links

- [EmailJS Documentation](https://www.emailjs.com/docs/)
- [EmailJS Dashboard](https://dashboard.emailjs.com/)
- [Google Forms](https://forms.google.com/)
- [Google Sheets](https://sheets.google.com/)

---

**Last Updated:** 2026-06-19
**Version:** 1.0
