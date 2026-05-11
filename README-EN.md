# QRCode-Generators 🟣

> Professional customizable QR Code generator — Free, Open Source, Neon Purple Dark UI

[![MIT License](https://img.shields.io/badge/License-MIT-a855f7.svg)](LICENSE)
[![PHP 8.2+](https://img.shields.io/badge/PHP-8.2+-7c3aed.svg)](https://php.net)
[![MariaDB](https://img.shields.io/badge/MariaDB-10.6+-a855f7.svg)](https://mariadb.org)
[![Open Source](https://img.shields.io/badge/Open%20Source-%E2%9D%A4-c084fc.svg)](https://github.com)

---

## ✨ Features

### 🔳 QR Types
| Type | Description |
|------|-------------|
| URL | Simple or dynamic web link |
| Text | Any free text |
| WiFi | Wireless network (SSID + password) |
| Email | Opens email client with pre-filled recipient, subject and body |
| Phone | Direct callable phone number |
| Discord | Discord invite link |
| Instagram | Instagram profile or account |
| TikTok | TikTok profile |

### 🎨 Design Customization
- **Colors**: Solid color or gradient (linear / radial / conic)
- **Dot Styles**: Square · Rounded · Circle · Diamond · Star · Cross
- **Center Logo**: PNG/JPG/SVG, shape square / rounded / circle, adjustable size
- **Transparent Background**: PNG export without background
- **Glow / Shadow**: Neon effect with adjustable intensity
- **Frame**: None · Simple · Rounded · Neon · Corner + custom text
- **Error Correction**: L (7%) · M (15%) · Q (25%) · H (30%)
- **Export Size**: 200px → 1200px

### 📤 Export
| Format | Description |
|--------|-------------|
| **PNG** | Maximum quality, transparency support |
| **JPG** | With background, smaller file size |
| **SVG** | Scalable vector, perfect for printing |
| **PDF** | Print ready, proper dimensions |

### 🤖 AI Style Generator
Type any description in the AI field and automatically generate:
- Colors (primary + gradient)
- Dot style
- Glow and frame effects
- Examples: `"Gaming Neon Blue"`, `"Minimalist Black"`, `"Fire Red Dragon"`, `"Ocean Wave Cyan"`

### 📡 Dynamic QR
- Create QR with short link (e.g. `yoursite.com/qr/abc123`)
- **Change destination URL anytime** without reprinting the QR
- Complete scan statistics

### 📊 Scan Statistics
- Total scans
- Scans today / this week
- Daily chart (last 30 days)
- Top countries
- Device types (Mobile / Tablet / Desktop)

### ⚡ Live Preview
QR updates **instantly** as you type — zero delay.

---

## 🚀 Installation

### System Requirements
- PHP **8.2+** with extensions: `pdo`, `pdo_mysql`, `mbstring`
- **MariaDB 10.6+** or MySQL 8+
- Apache with `mod_rewrite` enabled

### Installation Steps

**1. Clone the repository**
```bash
git clone https://github.com/YOUR_USERNAME/qrcode-generators.git
cd qrcode-generators
```

**2. Set up the database**
```bash
# Create database and tables
mysql -u root -p < database/schema.sql
```

**3. Edit configuration**

Open `api/config.php` and update:
```php
define('DB_HOST', 'localhost');
define('DB_NAME', 'qrcode_generators');
define('DB_USER', 'qrcode_user');       // ← your MariaDB user
define('DB_PASS', 'YOUR_SECURE_PASS'); // ← your password
define('SITE_URL', 'https://yoursite.com'); // ← your domain
```

**4. Upload to server**

Copy all files to your server's `public_html` (or `www`) directory:
```
public_html/
├── index.html
├── .htaccess
├── assets/
│   ├── css/style.css
│   └── js/
│       ├── app.js
│       ├── qr-engine.js
│       └── ai-style.js
├── api/
│   ├── config.php
│   ├── create-dynamic.php
│   ├── redirect.php
│   ├── stats.php
│   └── get-qrs.php
└── database/
    └── schema.sql
```

**5. Set permissions**
```bash
chmod 644 .htaccess
chmod 644 api/config.php
chmod 755 api/
```

**6. Verify**

Visit `https://yoursite.com` — the site should be fully functional!

---

## 📁 Project Structure

```
qrcode-generators/
├── index.html              # Main page (SPA)
├── .htaccess               # Apache routing + security
├── README.md               # Documentation (Romanian)
├── README-EN.md            # Documentation (English)
├── LICENSE                 # MIT License
│
├── assets/
│   ├── css/
│   │   └── style.css       # Neon Purple Dark styles
│   └── js/
│       ├── app.js          # Application logic
│       ├── qr-engine.js    # QR Canvas rendering engine
│       └── ai-style.js     # AI style generator
│
├── api/
│   ├── config.php          # DB config + helpers
│   ├── create-dynamic.php  # API: Create Dynamic QR
│   ├── redirect.php        # Redirect handler + scan logging
│   ├── stats.php           # API: Statistics
│   └── get-qrs.php         # API: CRUD QR codes
│
└── database/
    └── schema.sql          # MariaDB schema
```

---

## 🔧 Advanced Configuration

### Custom short domain for QR links
Edit in `api/config.php`:
```php
define('SITE_URL',    'https://yoursite.com');
define('QR_REDIRECT', SITE_URL . '/qr/');
```
Dynamic QR codes will look like: `https://yoursite.com/qr/abc123`

### Country detection (for statistics)
By default, country code is `XX` (undetected). For real detection:
1. **ip-api.com** (free, 45 req/min): Add an HTTP call in `redirect.php`
2. **MaxMind GeoLite2**: Download the database and use the PHP `geoip2` extension

### API protection with token (recommended for production)
In `api/config.php` add:
```php
define('API_TOKEN', 'YOUR_SECRET_TOKEN');
```
Then verify in each API file:
```php
$token = $_SERVER['HTTP_AUTHORIZATION'] ?? '';
if ($token !== 'Bearer ' . API_TOKEN) {
    jsonResponse(['success' => false, 'error' => 'Unauthorized.'], 401);
}
```

---

## 🌐 Technologies Used

| Technology | Purpose |
|------------|---------|
| **HTML5 Canvas** | Custom QR rendering |
| **qrcode-generator 1.4.4** | QR matrix generation |
| **jsPDF 2.5.1** | PDF export |
| **Font Awesome 6.5** | Icons |
| **Google Fonts** | Orbitron · Rajdhani · JetBrains Mono |
| **PHP 8.2** | Backend API |
| **MariaDB** | Database |
| **PDO** | Secure DB connection |

---

## 🤝 Contributing

Contributions are welcome! Follow these steps:

1. **Fork** the repository
2. Create a new branch: `git checkout -b feature/FeatureName`
3. Make your changes and commit: `git commit -m "Add: new feature"`
4. Push to branch: `git push origin feature/FeatureName`
5. Open a **Pull Request**

### Ideas for contributions
- [ ] User authentication (personal accounts)
- [ ] Full admin dashboard
- [ ] vCard / contact QR support
- [ ] Password-protected QR
- [ ] Additional UI themes
- [ ] API rate limiting
- [ ] Batch QR export

---

## 📜 License

Distributed under the **MIT License**. See [LICENSE](LICENSE) file for details.

---

## 🌟 If you like this project

⭐ Give it a **Star** on GitHub
🍴 **Fork** it and make it your own
📢 Share it with others

---

> Built with 💜 · Open Source Forever
