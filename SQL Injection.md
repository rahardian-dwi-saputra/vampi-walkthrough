# SQL Injection
Serangan SQL Injection adalah jenis serangan injeksi, di mana perintah SQL dimasukkan ke dalam input data untuk memengaruhi eksekusi perintah SQL yang telah ditentukan sebelumnya. Serangan SQL Injection yang berhasil dapat membaca data sensitif dari database, memodifikasi data database, atau menjalankan operasi administrasi pada database. Secara umum, cara aplikasi web membuat query SQL adalah dengan melibatkan sintaks SQL yang ditulis oleh programmer dicampur dengan data yang disediakan oleh pengguna. Celah keamanan ini berada di endpoint `/users/v1/{username}`

- Kita bisa menggunakan username apapun sebagai parameter kemudian menambahkan tanda petik tunggal dibagian akhir
```sh
curl "http://IP_Server:5000/users/v1/test'" --proxy http://127.0.0.1:8080 
```


- Selain tanda petik tunggal kita juga bisa menggunakan kode `%27` yang otomatis akan terdecode sebagai tanda petik tunggal
```sh
curl http://IP_Server:5000/users/v1/test%27 --proxy http://127.0.0.1:8080
```

