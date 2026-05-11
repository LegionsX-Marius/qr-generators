# QRCode-Generators 🟣

> Generator profesional de QR Coduri personalizabile — Gratuit, Open Source, Neon Purple Dark UI

[![Licență MIT](https://img.shields.io/badge/Licen%C8%9B%C4%83-MIT-a855f7.svg)](LICENSE)
[![PHP 8.2+](https://img.shields.io/badge/PHP-8.2+-7c3aed.svg)](https://php.net)
[![MariaDB](https://img.shields.io/badge/MariaDB-10.6+-a855f7.svg)](https://mariadb.org)
[![Open Source](https://img.shields.io/badge/Open%20Source-%E2%9D%A4-c084fc.svg)](https://github.com)

---

## ✨ Funcționalități

### 🔳 Tipuri de QR
| Tip | Descriere |
|-----|-----------|
| URL | Link web simplu sau dinamic |
| Text | Orice text liber |
| WiFi | Rețea wireless (SSID + parolă) |
| Email | Deschide client email cu destinatar, subiect și mesaj precompletate |
| Telefon | Număr de telefon direct apelabil |
| Discord | Link de invitație Discord |
| Instagram | Profil sau cont Instagram |
| TikTok | Profil TikTok |

### 🎨 Personalizare Design
- **Culori**: Culoare solidă sau gradient (linear / radial / conic)
- **Stiluri dots**: Pătrat · Rotunjit · Cerc · Diamant · Stea · Cruce
- **Logo centru**: PNG/JPG/SVG, formă pătrat / rotunjit / cerc, dimensiune reglabilă
- **Fundal transparent**: Export PNG fără fundal
- **Glow / Shadow**: Efect neon cu intensitate reglabilă
- **Frame**: Fără · Simple · Rounded · Neon · Corner + text personalizat
- **Nivel erori**: L (7%) · M (15%) · Q (25%) · H (30%)
- **Dimensiune export**: 200px → 1200px

### 📤 Export
| Format | Descriere |
|--------|-----------|
| **PNG** | Calitate maximă, suport transparență |
| **JPG** | Cu fundal, fișier mai mic |
| **SVG** | Vector scalabil, perfect pentru print |
| **PDF** | Print ready, dimensiune corespunzătoare |

### 🤖 AI Style Generator
Scrie în câmpul AI orice descriere și generează automat:
- Culorile (principale + gradient)
- Stilul dots-urilor
- Efecte glow și frame
- Exemple: `"Gaming Neon Blue"`, `"Minimalist negru"`, `"Fire Red Dragon"`, `"Ocean Wave Cyan"`

### 📡 QR Dinamic
- Crează QR cu link scurt (ex: `siteulmeu.ro/qr/abc123`)
- **Schimbă URL-ul destinație oricând** fără a reimprima QR-ul
- Statistici complete scanări

### 📊 Statistici Scanări
- Total scanări
- Scanări azi / săptămâna
- Grafic pe zile (ultimele 30 zile)
- Top țări
- Tipuri de dispozitive (Mobile / Tablet / Desktop)

### ⚡ Live Preview
QR-ul se actualizează **instant** pe măsură ce tastezi — zero delay.

---

## 🚀 Instalare

### Cerințe sistem
- PHP **8.2+** cu extensiile: `pdo`, `pdo_mysql`, `mbstring`
- **MariaDB 10.6+** sau MySQL 8+
- Apache cu `mod_rewrite` activat

### Pași instalare

**1. Clonează repository-ul**
```bash
git clone https://github.com/YOUR_USERNAME/qrcode-generators.git
cd qrcode-generators
```

**2. Configurează baza de date**
```bash
# Creează baza de date și tabelele
mysql -u root -p < database/schema.sql
```

**3. Editează configurarea**

Deschide `api/config.php` și modifică:
```php
define('DB_HOST', 'localhost');
define('DB_NAME', 'qrcode_generators');
define('DB_USER', 'qrcode_user');       // ← userul tău MariaDB
define('DB_PASS', 'PAROLA_TA_SIGURA'); // ← parola ta
define('SITE_URL', 'https://siteulmeu.ro'); // ← domeniul tău
```

**4. Upload pe server**

Copiază toate fișierele în directorul `public_html` (sau `www`) al serverului tău:
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

**5. Setează permisiunile**
```bash
chmod 644 .htaccess
chmod 644 api/config.php
chmod 755 api/
```

**6. Verificare**

Accesează `https://siteulmeu.ro` — site-ul trebuie să fie funcțional!

---

## 📁 Structura Proiectului

```
qrcode-generators/
├── index.html              # Pagina principală (SPA)
├── .htaccess               # Routing Apache + securitate
├── README.md               # Documentație (Română)
├── README-EN.md            # Documentation (English)
├── LICENSE                 # Licență MIT
│
├── assets/
│   ├── css/
│   │   └── style.css       # Stiluri Neon Purple Dark
│   └── js/
│       ├── app.js          # Logica aplicației
│       ├── qr-engine.js    # Motor randare QR pe Canvas
│       └── ai-style.js     # Generator stiluri AI
│
├── api/
│   ├── config.php          # Configurare DB + helpers
│   ├── create-dynamic.php  # API: Creare QR Dinamic
│   ├── redirect.php        # Handler redirect + log scanare
│   ├── stats.php           # API: Statistici
│   └── get-qrs.php         # API: CRUD QR-uri
│
└── database/
    └── schema.sql          # Schema MariaDB
```

---

## 🔧 Configurare Avansată

### Domeniu personalizat pentru QR scurt
Editează în `api/config.php`:
```php
define('SITE_URL',    'https://siteulmeu.ro');
define('QR_REDIRECT', SITE_URL . '/qr/');
```
QR-urile dinamice vor arăta astfel: `https://siteulmeu.ro/qr/abc123`

### Detectare țară (pentru statistici)
Implicit, codul țării este `XX` (nedetectat). Pentru detectare reală:
1. **ip-api.com** (gratuit, 45 req/min): Adaugă un apel HTTP în `redirect.php`
2. **MaxMind GeoLite2**: Descarcă baza de date și folosește extensia PHP `geoip2`

### Protejare API cu token (recomandat în producție)
În `api/config.php` adaugă:
```php
define('API_TOKEN', 'TOKEN_SECRET_AL_TAU');
```
Și verifică în fiecare fișier API:
```php
$token = $_SERVER['HTTP_AUTHORIZATION'] ?? '';
if ($token !== 'Bearer ' . API_TOKEN) {
    jsonResponse(['success' => false, 'error' => 'Neautorizat.'], 401);
}
```

---

## 🌐 Tehnologii Folosite

| Tehnologie | Scop |
|------------|------|
| **HTML5 Canvas** | Randare QR personalizabil |
| **qrcode-generator 1.4.4** | Generare matrice QR |
| **jsPDF 2.5.1** | Export PDF |
| **Font Awesome 6.5** | Iconițe |
| **Google Fonts** | Orbitron · Rajdhani · JetBrains Mono |
| **PHP 8.2** | Backend API |
| **MariaDB** | Bază de date |
| **PDO** | Conexiune securizată DB |

---

## 🤝 Contribuții

Contribuțiile sunt binevenite! Urmează acești pași:

1. **Fork** repository-ul
2. Creează un branch nou: `git checkout -b feature/NumeleFeaturii`
3. Fă modificările și commit: `git commit -m "Adaugă: funcție nouă"`
4. Push pe branch: `git push origin feature/NumeleFeaturii`
5. Deschide un **Pull Request**

### Idei pentru contribuții
- [ ] Autentificare utilizatori (cont personal)
- [ ] Dashboard admin complet
- [ ] Suport vCard / contact QR
- [ ] QR cu parolă de protecție
- [ ] Teme suplimentare UI
- [ ] API rate limiting
- [ ] Export batch QR-uri

---

## 📜 Licență

Distribuit sub licența **MIT**. Vezi fișierul [LICENSE](LICENSE) pentru detalii.

---

## 🌟 Dacă îți place proiectul

⭐ Dă un **Star** pe GitHub
🍴 Fă un **Fork** și personalizează
📢 Distribuie cu prietenii

---

> Creat cu 💜 · Open Source Forever
