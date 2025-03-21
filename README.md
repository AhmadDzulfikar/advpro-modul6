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
