# 🚀 Deploy-Webiste

> Tutorial deploy website di Debian Linux menggunakan Apache2, MariaDB, PHP-FPM, SSL, dan Webmin.

---

# 👤 Tahap 1 — SSH ke Server Debian

## 🔐 Login SSH via CMD Windows

```bash
ssh user@ip_debian
```

## 🔑 Masuk Root

```bash
su -
```

---

## 📸 Screenshot

![SSH](img/ssh.png)

---

# 🌐 Tahap 2 — Setup Apache2 + PHP-FPM

## 📦 Install Package

```bash
apt install apache2 mariadb-server php-fpm -y
```

---

## ⚙️ Aktifkan Proxy Module

```bash
a2enmod proxy_fcgi
```

---

## ⚙️ Aktifkan PHP-FPM

```bash
a2enconf php8.4-fpm
```

---

## 🔄 Reload Apache

```bash
systemctl reload apache2
```

---

## 📸 Screenshot

![Apache Setup](img/setup-apcahe2.png)

---

# 🔒 Tahap 3 — Setup SSL HTTPS Apache

## ⚙️ Aktifkan SSL Module

```bash
a2enmod ssl
```

---

## 📁 Buat Folder SSL

```bash
mkdir ssl
cd ssl
```

---

## 🔐 Generate SSL Certificate

```bash
openssl req -x509 -nodes -days 90 -newkey rsa:2048 \
-keyout self.key \
-out self.crt
```

---

## 📂 Cek File SSL

```bash
ls
```

Pastikan muncul:

```txt
self.key
self.crt
```

---

## 🛠️ Edit SSL Config Apache

```bash
nano /etc/apache2/sites-available/default-ssl.conf
```

Jika error atau file tidak ada:

```bash
nano /etc/apache2/sites-available/000-default-ssl.conf
```

---

## ✏️ Ubah Lokasi SSL

Cari:

```apache
SSLCertificateFile
SSLCertificateKeyFile
```

Contoh:

```apache
SSLCertificateFile /root/ssl/self.crt
SSLCertificateKeyFile /root/ssl/self.key
```

---

## ✅ Aktifkan SSL Site

```bash
a2ensite default-ssl.conf
```

---

## 🔄 Reload Apache

```bash
systemctl reload apache2
```

Jika reload error:

```bash
systemctl start apache2
```

---

## 📸 Screenshot

### 🔒 Setup SSL

![SSL](img/setup-ssl.png)

![SSL2](img/setup-ssl1.png)

---

### 📜 SSL Certificate

![SSL Rename](img/rename-ssl.png)

---

# 🖥️ Tahap 4 — Setup Webmin

## 📥 Download Webmin

```bash
wget http://IP_SERVER/webmin_2.630_all.deb
```

---

## 📦 Install Webmin

```bash
dpkg -i webmin_2.630_all.deb
```

---

## ⚠️ Jika Dependency Error

```bash
apt install -f
```

Lalu jalankan ulang:

```bash
dpkg -i webmin_2.630_all.deb
```

---

## 🌍 Akses Webmin

```txt
https://IP_DEBIAN:10000
```

Contoh:

```txt
https://192.168.1.9:10000
```

---

## 📸 Screenshot

![Webmin](img/wget.png)

---

# 📂 Tahap 5 — Upload Folder Website

Upload folder website ke:

```txt
/var/www/html
```

---

## 📋 Langkah

* Masuk Webmin
* Tools
* File Manager
* Buka `/var/www/html`
* Upload folder website

---

## 📸 Screenshot

### 📁 File Manager

![Upload Website](img/upload-website.png)

---

### 📤 Select Folder

![Upload Website 2](img/upload-webiste2.png)

---

### ✅ Hasil Upload

![Upload Website 3](img/upload-website3.png)

---

# 🔑 Tahap 6 — Buat Password Root MariaDB

## 📋 Langkah

* Masuk Webmin
* MariaDB Database Server
* Change Administration Password

---

## 📸 Screenshot

![Password MariaDB](img/setup-pwphp.png)

![Password MariaDB 2](img/setup-pwphp2.png)

---

# 🗄️ Tahap 7 — Buat Database

## 📋 Langkah

* Masuk MariaDB Database Server
* Klik `Create a new database`
* Isi nama database
* Klik `Create`

---

## 📸 Screenshot

![Create Database](img/create-database.png)

![Create Database 2](img/create-database2.png)

---

# 📥 Tahap 8 — Import SQL via Webmin

## 📋 Langkah

* Masuk database
* Execute SQL
* Import text file
* Upload file `.sql`
* Klik Execute

---

## 📸 Screenshot

![Import SQL](img/import-sql.png)

![Import SQL 2](img/import-sql2.png)

![Import SQL 3](img/import-sql3.png)

![Import SQL 4](img/import-sql4.png)

Jika berhasil import, langsung akses website kalian.

---

# ❌ Troubleshoot — Error Import SQL

Kadang Webmin error seperti:

```sql
Error 1146 Table doesn't exist
```

---

## 📸 Screenshot Error

![Import SQL Error](img/import-sql5.png)

---

# 💻 Tahap 9 — Import SQL via CLI Terminal

Jika Webmin gagal import SQL, gunakan terminal Debian.

---

## ⚙️ Command

```bash
mysql -u root -p nama_database < file.sql
```

---

## 🧪 Contoh

```bash
mysql -u root -p acelajg_db < /var/www/html/ecommerce/ecommerce.sql
```

---

## 📸 Screenshot

![Import CLI](img/import-sql6.png)

Setelah berhasil import, akses kembali website kalian.

---

# ⚠️ Troubleshoot — Error HTTP 500

Jika SQL berhasil diimport tetapi website menampilkan error HTTP 500.

---

## 🔧 Solusi

Ubah konfigurasi database pada file config website kalian:

* Username MySQL
* Password MySQL
* Nama Database

Sesuaikan dengan database yang dibuat pada Tahap 6 dan Tahap 7.

---

## 📸 Screenshot

![Config PHP](img/config.php.png)

---

# ✅ Hasil Deploy Website

Website berhasil dijalankan.

## 📸 Screenshot

![Hasil Website](img/hasil.png)

---

# 👨‍💻 Author

**Marcelino Kresna Pratama**
