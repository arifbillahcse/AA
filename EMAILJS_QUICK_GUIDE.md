# EmailJS - Quick Credential Finder Guide

## 🎯 Step-by-Step: Find Your Service ID

### Step 1: Go to Dashboard
```
👉 https://dashboard.emailjs.com/
   Login with your email
```

### Step 2: Find Service ID
```
Left Sidebar
    ↓
Click "Email Services"
    ↓
You'll see your email (Gmail/Outlook/etc)
    ↓
Click on it
    ↓
LOOK FOR BLUE TEXT: "service_xxxxxxxxx"
    ↓
👉 COPY THIS - IT'S YOUR SERVICE ID
```

**Example:**
```
Your Service ID: service_abc123xyz789
```

---

## 🔑 Step-by-Step: Find Your Public Key

### Step 1: Go to Dashboard
```
👉 https://dashboard.emailjs.com/
```

### Step 2: Find Public Key
```
Top Right Corner
    ↓
Click Your Profile Icon (Avatar/Picture)
    ↓
Click "Account" or "My Account"
    ↓
Scroll Down
    ↓
Find "API Keys" Section
    ↓
You'll see "Public Key"
    ↓
👉 COPY THIS - IT'S YOUR PUBLIC KEY
```

**Alternative Location:**
```
If you can't find it above:

Sidebar → "Admin" 
    ↓
Click "API Keys"
    ↓
Copy the "Public Key"
```

**Example:**
```
Your Public Key: 1a2b3c4d5e6f7g8h9i0j
```

---

## ✅ What You Should Have Now

Copy this information into `index.html`:

```javascript
const EMAIL_CONFIG = {
    emailJSServiceID: 'service_____PUT_YOUR_SERVICE_ID_HERE_____',
    emailJSTemplateID: 'template_asma_updates',  // Don't change this
    emailJSPublicKey: '___PUT_YOUR_PUBLIC_KEY_HERE___',
    recipientEmail: 'csearif2002@gmail.com'
};
```

**Filled Example:**
```javascript
const EMAIL_CONFIG = {
    emailJSServiceID: 'service_abc123xyz789',
    emailJSTemplateID: 'template_asma_updates',
    emailJSPublicKey: '1a2b3c4d5e6f7g8h',
    recipientEmail: 'csearif2002@gmail.com'
};
```

---

## 🧪 Test It

1. Open browser DevTools (F12)
2. Go to Console tab
3. Interact with website (click a button)
4. Look for green ✅ messages saying:
   ```
   ✅ EmailJS initialized
   ✅ Email sent successfully
   ```

If you see RED ❌ errors:
- Check Service ID has no spaces
- Check Public Key has no spaces
- Check Service ID starts with `service_`
- Check you're using correct credentials (copy-paste!)

---

## 🆘 Common Issues

### "Can't find Service ID"
```
Check these locations:
1. Dashboard → Email Services → Your Email → Blue Text
2. Dashboard → Admin → Services → Copy ID
3. Try different browser/clear cache
4. Make sure you're logged in
```

### "Can't find Public Key"
```
Check these locations:
1. Dashboard → Profile Icon → Account → API Keys
2. Dashboard → Admin → API Keys
3. Top Right Corner near your name
4. Check you're logged into correct account
```

### "Still stuck?"
```
1. Check you're on https://dashboard.emailjs.com (NOT emailjs.com)
2. Log out completely, log back in
3. Try incognito/private browser window
4. Check EmailJS email confirmation (may need to verify)
```

---

## 📋 Checklist

- [ ] I found my Service ID (looks like: `service_abc123xyz`)
- [ ] I found my Public Key (looks like: `1a2b3c4d5e6f`)
- [ ] I created email template named `template_asma_updates`
- [ ] I updated `EMAIL_CONFIG` in index.html
- [ ] I tested and see ✅ in console
- [ ] I received test email

**Once all checked ✅ → EmailJS is working!**

---

**Need more help?** 
- Check SETUP_GUIDE.md for detailed instructions
- Visit https://www.emailjs.com/docs/
