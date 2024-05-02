# Excessive Data Exposure
Terkadang developer API tidak memikirkan sensitivitas data yang diekspos. Alat otomatis biasanya tidak dapat mendeteksi kerentanan jenis ini karena sulit membedakan antara data sah yang dikembalikan oleh API dan data sensitif yang tidak boleh dikembalikan tanpa pemahaman mendalam tentang aplikasinya. Insecure endpoint API tidak memerlukan autentikasi apa pun untuk mengakses data sehingga penyerang dapat mengakses data pengguna lain atau data resmi. Jika kita lihat endpoint `/users/v1/_debug` akan menampilkan semua data pengguna secara detail termasuk username dan password
```sh
curl http://IP_Server:5000/users/v1/_debug --proxy http://127.0.0.1:8080
```

![alt text](https://github.com/rahardian-dwi-saputra/vampi-walkthrough/blob/main/assets/excessive%20data%20exposure/sensitive%201.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/vampi-walkthrough/blob/main/assets/excessive%20data%20exposure/sensitive%202.JPG)