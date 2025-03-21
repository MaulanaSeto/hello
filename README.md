# Releksi
### Commit 1
Fungsi `handle_connection` berguna untuk menangani koneksi TCP. Buffered Reader membaca data yang berasal dari TCP *stream* sebagai Vector hingga menerima baris kosong yang menandakan akhir dari *header* HTTP. Selanjutnya, fungsi ini mencetak permintaan HTTP ke konsol.
### Commit 2
![Commit 2](https://github.com/MaulanaSeto/hello/blob/master/images/commit2.png)
Fungsi `handle_connection` menerima kepemilikan TcpStream yang direpresentasi oleh *stream*. Selanjutnya, Buffered Reader dibuat untuk membaca data dari TCP *stream* lalu disimpan pada variabel `http_request`. Selanjutnya, fungsi ini mengirim respons HTTP ke klien yang berisi berkas `hello.html`.
### Commit 3
![Commit 3](https://github.com/MaulanaSeto/hello/blob/master/images/commit3.png)
Fungsi `handle_connection` memeriksa baris pertama permintaan HTTP. Jika baris tersebut adalah `GET / HTTP/1.1` yang berisi *root path*, maka fungsi ini mengembalikan respons HTTP berisi berkas `hello.html`. Namun, jika baris tersebut berisi permintaan akses terhadap *path* lain, maka fungsi ini mengembalikan respons HTTP berisi berkas `404.html`.
### Commit 4
Terdapat *path* tambahan `/sleep`. Setelah fungsi `handle_connection` menerima permintaan HTTP dengan *path* `/sleep`, fungsi ini akan diam selama lima detik sebelum mengirim respons HTTP yang berisi berkas `hello.html`.
### Commit 5
Implementasi server diubah menjadi *multithreaded* dengan menggunakan *thread pool*. Dengan pendekatan ini, server dapat menangani banyak koneksi secara bersamaan, sehingga tidak terhambat oleh satu permintaan yang lama. Penggunaan *thread pool* menghindari *overhead* yang muncul akibat pembuatan *thread* baru untuk setiap koneksi, sehingga pemanfaatan sumber daya menjadi lebih efisien dan kinerja server meningkat secara signifikan.
### Commit Bonus
Fungsi `build` dibuat sebagai alternatif fungsi `new` dengan menambah validasi ukuran *thread pool* agar lebih besar dari nol. Alih-alih menggunakan `assert` yang menyebabkan *panic*, `build` mengembalikan Result galat. Kedua fungsi ini tetap menginisialisasi *channel*, membungkus *receiver* dalam Arc dan Mutex, serta membuat *worker* dengan logika yang sama. Pendekatan `build` ini memberi fleksibilitas tambahan untuk menambah logika inisialisasi di masa depan sehingga desain *thread pool* menjadi lebih *robust*.
