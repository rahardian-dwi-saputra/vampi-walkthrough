# Lack of Resources & Rate Limiting
Beberapa permintaan bersamaan dapat dilakukan dari satu komputer lokal atau dengan menggunakan sumber daya komputasi awan. Beberapa API tidak menerapkan pembatasan akses. Mengingat bahwa tidak ada pembatasan akses, maka serangan brute force menjadi pilihan yang sangat tepat. Disisi lain eksploitasi pada celah keamanan ini dapat menyebabkan DoS, membuat API tidak responsif atau bahkan tidak tersedia dengan mengirim spam ke API dengan ratusan atau ribuan permintaan per detik. Pada tahap ini kita akan melakukan brute force login ke akun `name1` melalui endpoint `/users/v1/login`
- Pertama-tama kita login menggunakan tool `curl` kemudian merekam request nya ke tool `Burp Suite`
```sh
curl http://192.168.100.12:5000/users/v1/login -d '{"username":"name1","password":"abc"}' -H 'Content-Type: application/json' --proxy http://127.0.0.1:8080
```

- Setelah itu buka tool `Burp Suite` dan kirim request ke tab Intruder


- Hilangkan semua tanda payload


- Block value parameter password kemudian tambahkan tanda payload

- Pindah ke tab Intruder > Payloads kemudian copy list password dibawah ini lalu tekan tombol paste di Burp Suite. Jika daftar payload sudah terisi tekan tombol **Start attack** 
```sh
test
12345
qwerty
admin
qwerty123
testing
pass
pass1
abc123
abcd1234
```

- Tunggu hingga proses serangan selesai. Setelah selesai, dari hasil serangan diketahui bahwa payload `pass1` mempunyai length yang paling berbeda. Pada bagian response menunjukkan bahwa payload tersebut adalah password yang valid untuk username `name1`