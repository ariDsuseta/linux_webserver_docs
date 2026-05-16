# linux_webserver_docs
tabel perintah untuk webserver linux (debian server)

# 🐧 Cheat Sheet Perintah Linux Debian untuk Web Server

Repositori ini berisi daftar perintah Linux Debian yang paling sering digunakan untuk mengelola *web server* (Apache, Nginx, PHP, MySQL/MariaDB).

---

## ⚙️ 1. Manajemen Layanan (Systemd)
Digunakan untuk mengontrol status dan jalannya *web server* atau *database*.

| Perintah | Fungsi / Kegunaan | Contoh Penggunaan |
| :--- | :--- | :--- |
| `systemctl start <service>` | Menjalankan sebuah layanan | `sudo systemctl start nginx` |
| `systemctl stop <service>` | Menghentikan sebuah layanan | `sudo systemctl stop apache2` |
| `systemctl restart <service>` | Mematikan lalu menyalakan ulang layanan | `sudo systemctl restart mysql` |
| `systemctl reload <service>` | Memuat ulang konfigurasi (tanpa *downtime*) | `sudo systemctl reload nginx` |
| `systemctl status <service>` | Mengecek status aktif/tidaknya layanan | `sudo systemctl status php8.2-fpm` |
| `systemctl enable <service>` | Mengaktifkan layanan saat server *booting* | `sudo systemctl enable nginx` |
| `systemctl disable <service>` | Mematikan fitur otomatis berjalan saat *booting* | `sudo systemctl disable apache2` |

---

## 📁 2. Manajemen File & Hak Akses (Permissions)
Penting untuk mengelola *source code* website di direktori web (misal: `/var/www/html`).

| Perintah | Fungsi / Kegunaan | Contoh Penggunaan |
| :--- | :--- | :--- |
| `cd <direktori>` | Berpindah folder/direktori | `cd /var/www/html/` |
| `ls -la` | Melihat daftar file & folder secara detail | `ls -la` |
| `chown -R user:group <path>` | Mengubah kepemilikan file/folder | `sudo chown -R www-data:www-data /var/www/html` |
| `chmod <mode> <path>` | Mengubah hak akses (*read, write, execute*) | `sudo chmod 755 /var/www/html` |
| `nano <file>` | Mengedit file teks langsung di terminal | `sudo nano /etc/nginx/sites-available/default` |
| `mkdir <nama_folder>` | Membuat folder baru | `mkdir nama_folder` |
| `rm -rf <path>` | Menghapus file/folder secara paksa (*hati-hati!*) | `sudo rm -rf folder_lama/` |

---

## 📊 3. Pemantauan Server & Log (Monitoring)
Digunakan untuk mencari tahu penyebab web *error* (debugging) dan memantau resource server.

| Perintah | Fungsi / Kegunaan | Contoh Penggunaan |
| :--- | :--- | :--- |
| `tail -f <file_log>` | Memantau log secara *real-time* (live) | `tail -f /var/log/nginx/error.log` |
| `htop` | Memantau penggunaan CPU & RAM secara interaktif | `htop` |
| `df -h` | Mengecek sisa kapasitas penyimpanan harddisk | `df -h` |
| `free -m` | Mengecek sisa kapasitas RAM (dalam MB) | `free -m` |
| `du -sh <path>` | Melihat total ukuran suatu folder/file | `du -sh /var/www/html` |

---

## 🌐 4. Jaringan & Keamanan (Networking & Firewall)
Untuk memantau port yang terbuka dan mengamankan lalu lintas data server.

| Perintah | Fungsi / Kegunaan | Contoh Penggunaan |
| :--- | :--- | :--- |
| `ss -tunlp` | Melihat port yang sedang terbuka & aktif | `sudo ss -tunlp` |
| `ufw allow <port>` | Membuka port tertentu pada *firewall* | `sudo ufw allow 80/tcp` |
| `curl -I <url>` | Mengecek respon HTTP header dari suatu web | `curl -I http://localhost` |
| `netstat -an` | Melihat seluruh koneksi jaringan yang aktif | `netstat -an` |

---

## 📦 5. Manajemen Paket Aplikasi (APT)
Untuk menginstal, memperbarui, atau menghapus aplikasi di Debian.

| Perintah | Fungsi / Kegunaan | Contoh Penggunaan |
| :--- | :--- | :--- |
| `apt update` | Memperbarui daftar paket dari repositori | `sudo apt update` |
| `apt upgrade` | Memperbarui semua aplikasi ke versi terbaru | `sudo apt upgrade` |
| `apt install <paket>` | Menginstal aplikasi baru | `sudo apt install certbot python3-certbot-nginx` |
| `apt purge <paket>` | Menghapus aplikasi beserta konfigurasinya | `sudo apt purge apache2` |

---

## 💡 Tips Cepat Validasi Konfigurasi
Selalu cek sintaks konfigurasi Anda sebelum melakukan *restart* layanan untuk menghindari web mati (*down*):

*   **Nginx:** `sudo nginx -t`
*   **Apache:** `sudo apache2ctl configtest`