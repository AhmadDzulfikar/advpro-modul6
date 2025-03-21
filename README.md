# RUST Advanced Programming
### Ahmad Dzulfikar As Shavy - 2306152374
---
## MODULE 6
---
### Milestone 1
> You may need to check the Rust documentation to understand what is inside the handle_connection method. Write as reflection notes in the Readme.md. Write it nicely.
Setelah membaca dokumentasi Rust tentang handle_connection, yang saya dapatkan adalah saya lebih mengenal dan paham mendalam tentang cara kerja komunikasi antara browser dan server, saya belajar kalau:
- Penggunaan Buffer
Pemanfaatan `BufReader` sangat membantu dalam mengelola data yang masuk, terutama untuk operasi I/O yang berulang. Hal ini sejalan dengan dokumentasi Rust yang menekankan efisiensi penggunaan buffer dalam membaca data.

- Iterator dan Closure
Metode `lines()` bersama dengan `take_while()` menunjukkan betapa powerful-nya konsep iterator dan penggunaan closure dalam Rust. Dengan menggunakan iterator, saya dapat dengan mudah memproses data baris per baris dan menentukan kapan harus menghentikan iterasi (yaitu saat menemukan baris kosong).

- Pertimbangan Error Handling
Penggunaan `unwrap()` di sini merupakan langkah awal dalam belajar. Namun, saya menyadari bahwa untuk aplikasi produksi perlu dikembangkan penanganan error yang lebih robust agar aplikasi dapat menangani berbagai kondisi gagal baca data secara lebih aman. 

### Milestone 2
> Complete your reflection on the new handle_connection in the readme.md, put the title clearly such as Commit 2 Reflection notes. commit with message “(2) Returning HTML”, push it to your git repository server.

Pada milestone 2, saya telah memodifikasi fungsi handle_connection untuk mengembalikan halaman HTML ke browser. Perubahan utama terletak pada cara server menanggapi request HTTP, di mana sekarang server tidak hanya mencetak request ke console, tetapi juga mengirimkan response HTTP yang lengkap sehingga browser dapat menampilkan halaman web.

Poin-poin yang Dipelajari
- Pembuatan Response HTTP
Saya belajar bahwa response HTTP harus mengikuti format tertentu, dimulai dengan status line seperti `HTTP/1.1 200 OK`, diikuti oleh header (misalnya, Content-Length) dan diakhiri dengan dua baris kosong `(\r\n\r\n)` sebelum body (isi HTML) dikirimkan. Hal ini penting agar browser dapat memahami di mana header berakhir dan body dimulai.

Membaca File HTML
Dengan menggunakan `fs::read_to_string("hello.html")`, server membaca isi file HTML yang berisi markup sederhana. Pendekatan ini memungkinkan kita untuk dengan mudah mengubah tampilan halaman dengan hanya mengedit file HTML eksternal, tanpa perlu mengubah kode program.

Menghitung Panjang Konten
Sebelum mengirim response, saya menghitung panjang dari konten HTML yang dihasilkan. Nilai panjang ini dimasukkan ke header `Content-Length`. Header ini memastikan bahwa browser mengetahui jumlah byte yang harus dibaca sebagai isi (body) response.

Dokumentasi:
![image](https://github.com/user-attachments/assets/e0d7a9e0-083d-43f8-860d-6b4bf708cba5)
