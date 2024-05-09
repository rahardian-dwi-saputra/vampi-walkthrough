# VAmPI - Vulnerable REST API Walkthrough
Vampi adalah REST API yang rentan dengan kerentanan OWASP top 10 untuk pengujian keamanan
- Link: https://github.com/erev0s/VAmPI

## Instalasi di Ubuntu
- Cloning repositori
```sh
git clone https://github.com/erev0s/VAmPI.git
```

![alt text](https://github.com/rahardian-dwi-saputra/vampi-walkthrough/blob/main/assets/instalasi/1.JPG)

- Instalasi depedensi
```sh
cd VAmPI
pip3 install -r requirements.txt
```

![alt text](https://github.com/rahardian-dwi-saputra/vampi-walkthrough/blob/main/assets/instalasi/2.JPG)

- Install plugin untuk swagger ui
```sh
pip3 install connexion[swagger-ui]
```

![alt text](https://github.com/rahardian-dwi-saputra/vampi-walkthrough/blob/main/assets/instalasi/3.JPG)

- Menjalankan API
```sh
python3 app.py
```

![alt text](https://github.com/rahardian-dwi-saputra/vampi-walkthrough/blob/main/assets/instalasi/4.JPG)

- Untuk dokumentasi API bisa diakses di `http://<IP_Server>:5000/ui`

![alt text](https://github.com/rahardian-dwi-saputra/vampi-walkthrough/blob/main/assets/instalasi/5.JPG)

- Uji coba API di kali linux
```sh
curl http://<IP_Server>:5000
```

![alt text](https://github.com/rahardian-dwi-saputra/vampi-walkthrough/blob/main/assets/instalasi/6.JPG)

## Lesson
- [SQLi Injection](SQL%20Injection.md)
- [Unauthorized Password Change](Unathorized%20Password%20Change.md)
- [Broken Object Level Authorization](Broken%20Object%20Level%20Authorization.md)
- [Mass Assignment](Mass%20Assigment.md)
- [Excessive Data Exposure](Excessive%20Data%20Exposure.md)
- [User and Password Enumeration](User%20and%20Password%20Enumeration.md)
- [RegexDOS (Denial of Service)](RegexDOS.md)
- [Lack of Resources & Rate Limiting](Lack%20of%20Resources%20and%20Rate%20Limiting.md)

## Disclaimer
Semua materi yang disajikan disini hanya digunakan sebagai media pembelajaran. Penulis tidak bertanggung jawab atas penyalahgunaan dari materi tersebut