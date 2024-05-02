# VAmPI - Vulnerable REST API Walkthrough
Vampi adalah REST API yang rentan dengan kerentanan OWASP top 10 untuk pengujian keamanan
- Link: https://github.com/erev0s/VAmPI

## Instalasi di Ubuntu
- Cloning repositori
```sh
git clone https://github.com/erev0s/VAmPI.git
```
- Instalasi depedensi
```sh
cd VAmPI
pip3 install -r requirements.txt
```
- Install plugin untuk swagger ui
```sh
pip3 install connexion[swagger-ui]
```
- Menjalankan API
```sh
python3 app.py
```
- Untuk dokumentasi API bisa diakses di `http://<IP_Server>:5000/ui`



## Disclaimer
Semua materi yang disajikan disini hanya digunakan sebagai media pembelajaran. Penulis tidak bertanggung jawab atas penyalahgunaan dari materi tersebut