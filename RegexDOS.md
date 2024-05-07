# Regular expression Denial of Service - ReDoS
Regular expression Denial of Service (ReDoS) adalah serangan Denial of Service, yang mengeksploitasi sebagian besar implementasi Regular Expression yang dapat mencapai situasi ekstrem dan menyebabkannya bekerja sangat lambat (secara eksponensial terkait dengan ukuran input). Penyerang dapat menyebabkan program yang menggunakan Regular Expression (Regex) memasuki situasi ekstrem ini dan kemudian hang dalam waktu yang sangat lama. Celah keamanan ini berada di endpoint `/users/v1/{username}/email`. Untuk mengakses endpoint ini kita harus login tersebut dengan akun baru yang berhasil kita buat sebelumnya

```sh
curl http://IP_Server:5000/users/v1/login -d '{"username":"test","password":"test"}' -H 'Content-Type: application/json' --proxy http://127.0.0.1:8080
```

- Sekarang kita coba ubah email akun user `name1` dengan inputan string yang sangat panjang misalnya `aaaaaaaaaaaaaaaaaaaaaaaaaaaaabbbbb`
```sh
curl -X PUT http://IP_Server:5000/users/v1/name1/email -d '{"email":"aaaaaaaaaaaaaaaaaaaaaaaaaaaaabbbbb"}' -H 'Authorization: Bearer token' -H 'Content-Type: application/json' -H "Accept: application/json" --proxy http://127.0.0.1:8080 -v
```

- Dari percobaan diatas terlihat bahwa semakin panjang inputan string yang berikan, server akan semakin lama untuk memprosesnya. Hal ini dapat menyebabkan layanan API tidak dapat diakses dalam kurun waktu tertentu