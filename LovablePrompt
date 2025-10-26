# 🧠 Vibe Coding Project: URL Shortener SaaS (n8n + Lovable)

This project demonstrates how to build a **Bitly-like SaaS** using **Vibe Coding tools** — powered by **n8n** for backend automation and **Lovable.dev** for the frontend UI.

---

## 🚀 Project Overview

We'll create a simple **URL Shortener SaaS** that allows users to enter a long URL and receive a shortened one in return — all without writing traditional backend code.

### 🛠️ Tools Used
- **Lovable.dev** — No-code frontend builder (UI)
- **n8n.io** — Automation backend for generating and redirecting URLs

---

## ⚙️ Workflow Steps (n8n)

### **1. Create a Workflow for Short URL Generation**

1. Add a **Webhook Trigger** node — this will receive requests from your frontend (Lovable app).
   - Method: **POST**
   - Example URL: `/webhook/shorten-url`

2. Add a **Function** node to generate a shortcode for each new URL.

```javascript
// Generate a random 6-character shortcode
function generateShortCode() {
  const chars = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789';
  let code = '';
  for (let i = 0; i < 6; i++) {
    code += chars.charAt(Math.floor(Math.random() * chars.length));
  }
  return code;
}

return items.map(item => {
  const originalUrl = item.json.url;
  const shortCode = generateShortCode();
  return {
    json: {
      originalUrl,
      shortCode,
      shortUrl: `https://n8n.yourdomain.com/webhook/redirect/${shortCode}`
    }
  };
});
```

3. Store the mapping (shortCode → originalUrl) using a **Database node** (like SQLite, PostgreSQL, or even Google Sheets).

4. Add a **Respond to Webhook** node to send the shortened URL back to the frontend.

---

### **2. Create a Second Workflow for Redirection**

1. Add another **Webhook Trigger** node:
   - Method: **GET**
   - Example URL: `/webhook/redirect/:code`

2. Add a **Database Query** node to fetch the original URL using the `code` parameter.

3. Use a **Respond to Webhook** node:
   - Set HTTP Status: **302 (Redirect)**
   - Add header: `Location: {{originalUrl}}`

This ensures that when a user visits the shortened link, they’re automatically redirected to the original website.

---

## 💻 Frontend (Lovable.dev)

> 🧩 **Add your Lovable prompt and configuration steps here:**  
---
Create a shortn url wesbite with a input box to provide the original url and then provide the response with short url.
I will give you to apis
1. To create the short url : Post with Json Body 
    Url : http://localhost:5678/webhook-test/shorten
    Body : { "url": To Fetch from input box }
2. To Redirect to actual url : Get Call
    url : http://localhost:5678/webhook-test/b3d31330-e3cf-4ad5-85f7-32e17ebe796e/r/:code
     :code is the short code that we will recive from url, It will redirect to the actual url that we will get from db. 
---

## 🧩 Example API Flow

**POST /webhook/shorten-url**
```json
{
  "url": "https://example.com/my-long-page"
}
```
**Response:**
```json
{
  "shortUrl": "https://n8n.yourdomain.com/webhook/redirect/aB12xZ"
}
```

---

## 🧠 Notes
- You can host n8n on your own server or use n8n.cloud.
- Use a custom domain (like `short.yourdomain.com`) for professional branding.
- Add analytics or user authentication later to turn this into a full SaaS.

---

## 🪄 Credits
Built with ❤️ using **Vibe Coding**, **n8n**, and **Lovable.dev**
