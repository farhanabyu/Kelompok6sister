skalabilitas horizontal


- Implementasi skalabilitas horizontal tergantung pada teknologi dan lingkungan yang digunakan. 
Di bawah ini adalah contoh sederhana dalam bahasa Python menggunakan Flask (framework web) dan Redis (basis data) untuk membuat aplikasi web yang dapat dijalankan dengan beberapa instance.

# Import library yang diperlukan
from flask import Flask
from redis import Redis

# Inisialisasi aplikasi Flask
app = Flask(_name_)
# Inisialisasi koneksi Redis
redis = Redis(host='redis', port=6379)

# Definisi route untuk menghitung jumlah kunjungan
@app.route('/')
def hit_counter():
    # Menginkremen counter di Redis setiap kali halaman ini diakses
    redis.incr('counter')
    # Membaca nilai counter dari Redis
    count = redis.get('counter').decode('utf-8')
    return 'Ini adalah kunjungan ke-{}.\n'.format(count)

if _name_ == '_main_':
    # Menjalankan aplikasi Flask pada port 5000
    app.run(host='0.0.0.0', port=5000)

Dalam contoh ini, kita memiliki aplikasi sederhana yang menghitung jumlah kunjungan dan menyimpannya di Redis. Untuk mencapai skalabilitas horizontal, Anda dapat menjalankan beberapa instance dari aplikasi ini di beberapa server atau kontainer yang sama atau berbeda. Setiap instance akan dapat mengakses Redis yang sama untuk menyimpan dan mengambil data kunjungan.

skalabilitas vertikal
Contoh kodingan yang menggambarkan skalabilitas vertikal mungkin tidak terlalu bermanfaat karena itu lebih berkaitan dengan konfigurasi dan manajemen infrastruktur daripada kode aplikasi. Namun, berikut adalah contoh konfigurasi Docker Compose yang dapat digunakan untuk meningkatkan kapasitas vertikal pada aplikasi sederhana yang menggunakan Node.js:
version: '3'
services:
  web:
    image: node:14
    command: node app.js
    ports:
      - "3000:3000"
    environment:
      NODE_ENV: production
    deploy:
      resources:
        reservations:
          memory: 1G # Meningkatkan alokasi RAM
          cpus: '1'  # Meningkatkan alokasi CPU

Dalam contoh ini, kita menggunakan Docker Compose untuk menjalankan aplikasi Node.js di dalam kontainer Docker. Di bagian deploy, Anda dapat melihat bahwa kami mengatur alokasi sumber daya untuk kontainer, seperti jumlah RAM dan CPU yang dialokasikan. Anda dapat meningkatkan nilai memory dan cpus sesuai dengan kebutuhan aplikasi Anda untuk mencapai skalabilitas vertikal.
