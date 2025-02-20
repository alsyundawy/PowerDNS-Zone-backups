# PowerDNS Zone Backups Bash Script

[![Latest Version](https://img.shields.io/github/v/release/alsyundawy/PowerDNS-Zone-Backups)](https://github.com/alsyundawy/PowerDNS-Zone-Backups/releases)
[![Maintenance Status](https://img.shields.io/maintenance/yes/9999)](https://github.com/alsyundawy/PowerDNS-Zone-Backups/)
[![License](https://img.shields.io/github/license/alsyundawy/PowerDNS-Zone-Backups)](https://github.com/alsyundawy/PowerDNS-Zone-Backups/blob/master/LICENSE)
[![GitHub Issues](https://img.shields.io/github/issues/alsyundawy/PowerDNS-Zone-Backups)](https://github.com/alsyundawy/PowerDNS-Zone-Backups/issues)
[![GitHub Pull Requests](https://img.shields.io/github/issues-pr/alsyundawy/PowerDNS-Zone-Backups)](https://github.com/alsyundawy/PowerDNS-Zone-Backups/pulls)
[![Donate with PayPal](https://img.shields.io/badge/PayPal-donate-orange)](https://www.paypal.me/alsyundawy)
[![Sponsor with GitHub](https://img.shields.io/badge/GitHub-sponsor-orange)](https://github.com/sponsors/alsyundawy)
[![GitHub Stars](https://img.shields.io/github/stars/alsyundawy/PowerDNS-Zone-Backups?style=social)](https://github.com/alsyundawy/PowerDNS-Zone-Backups/stargazers)
[![GitHub Forks](https://img.shields.io/github/forks/alsyundawy/PowerDNS-Zone-Backups?style=social)](https://github.com/alsyundawy/PowerDNS-Zone-Backups/network/members)
[![GitHub Contributors](https://img.shields.io/github/contributors/alsyundawy/PowerDNS-Zone-Backups?style=social)](https://github.com/alsyundawy/PowerDNS-Zone-Backups/graphs/contributors)

**If you find this project helpful and would like to support it, please consider donating via https://www.paypal.me/alsyundawy. Thank you for your support!**

**Jika Anda merasa terbantu dan ingin mendukung proyek ini, pertimbangkan untuk berdonasi melalui https://www.paypal.me/alsyundawy. Terima kasih atas dukungannya!**

PowerDNS menggunakan backend database secara default (mis. MySQL). Cukup lakukan dump database dari database yang dikonfigurasi dan Anda akan memiliki snapshot dari semua zona untuk pemulihan yang mudah. Disarankan untuk membuang database ke cadangan secara teratur sehingga Anda dapat memulihkan jika terjadi kerusakan server. Seberapa sering Anda harus mengambil cadangan sebagian bergantung pada seberapa aktif zona diperbarui, sekali sehari adalah aturan praktis yang baik.

Namun ini hanya baik untuk melakukan pengembalian penuh semua zona ke titik waktu pencadangan dibuat. Mengembalikan satu zona dari dump database penuh akan menjadi hal yang tidak sepele. PowerDNS menyertakan alat baris perintah pdnsutil yang dapat digunakan untuk membuang file zona individu. Anda kemudian dapat memulihkan masing-masing zona ke keadaan pada saat ekspor tertentu. Ini berguna jika satu zona secara tidak sengaja terhapus atau salah diperbarui dan Anda perlu memulihkan zona tertentu saja.

Berikut ini adalah skrip bash sederhana yang menggunakan alat baris perintah pdnsutil untuk membuang setiap zona dalam database ke file zona individual, dan untuk menyimpan salinan setiap file zona selama 28 hari sebelumnya.

wget -c https://raw.githubusercontent.com/alsyundawy/PowerDNS-Zone-Backups/main/export-zones-pds.sh

Simpan skrip sebagai /usr/local/bin/export-zones-pds.sh dan kemudian tambahkan tugas cron yang berjalan sekali sehari. Misalnya, untuk membuang zona pada pukul 3:01 setiap hari, tambahkan tugas cron ini: 1 3 * * * /usr/local/bin/export-zones-pds.sh

Untuk memulihkan zona, gunakan perintah pdnsutil seperti ini: /usr/bin/pdnsutil load-zone example.com /home/powerdns/zones/example.com-20230725.zone

Anda dapat dengan mudah menyesuaikan retensi (saat ini 28 hari) dengan menyesuaikan opsi -mtime pada perintah find di akhir skrip. Dengan sedikit lebih banyak pekerjaan, Anda dapat menyesuaikan var hari ini untuk memasukkan jam dan mungkin menit jika Anda ingin menyimpan zona beberapa kali sehari.

**Anda bebas untuk mengubah, mendistribusikan script ini untuk keperluan anda**


### Anda Memang Luar Biasa | Harry DS Alsyundawy | Kaum Rebahan Garis Keras & Militan
