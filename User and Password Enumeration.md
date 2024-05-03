# User and Password Enumeration
Seringkali, aplikasi web mengungkapkan keberadaan nama pengguna di sistem, baik karena kesalahan konfigurasi atau karena kesalahan desain. Misalnya, saat mengirimkan kredensial yang salah, kita menerima pesan yang menyatakan bahwa nama pengguna ada di sistem atau kata sandi yang diberikan salah. Informasi ini dapat digunakan untuk menyerang aplikasi web, misalnya melalui serangan brute force atau mengenumerasi username dan password. Celah keamanan ini ada di endpoint `/users/v1/login`

- Sekarang kita coba lakukan login dengan username yang ada tapi dengan password yang salah
```sh
curl http://IP_Server:5000/users/v1/login -d '{"username":"test","password":"abcd"}' -H 'Content-Type: application/json' --proxy http://127.0.0.1:8080
```

![alt text](https://github.com/rahardian-dwi-saputra/vampi-walkthrough/blob/main/assets/username%20and%20password%20enumeration/enum%201.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/vampi-walkthrough/blob/main/assets/username%20and%20password%20enumeration/enum%202.JPG)

- Pesan yang kita dapat menyatakan bahwa username tersebut valid tapi passwordnya salah. Sekarang kita coba login dengan username dan password yang salah
```sh
curl http://IP_Server:5000/users/v1/login -d '{"username":"abcd","password":"abcd"}' -H 'Content-Type: application/json' --proxy http://127.0.0.1:8080
```

![alt text](https://github.com/rahardian-dwi-saputra/vampi-walkthrough/blob/main/assets/username%20and%20password%20enumeration/enum%203.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/vampi-walkthrough/blob/main/assets/username%20and%20password%20enumeration/enum%204.JPG)

- Pesan yang kita dapat menyatakan bahwa username tersebut tidak valid. Celah ini bisa dimanfaatkan oleh penyerang untuk mengumpulkan daftar username kemudian melakukan brute force untuk menemukan password yang valid