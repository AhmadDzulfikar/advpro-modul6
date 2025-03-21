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

### Milestone 3
> Add additional reflection notes, put the title clearly such as Commit 3 Reflection notes.
Pada milestone ini, saya menambahkan validasi request agar server dapat merespon secara selektif berdasarkan apa yang diminta oleh browser. Sebelumnya, server selalu mengembalikan halaman hello.html tanpa memperhatikan isi request.
Poin-Poin Utama
1. Validasi Request
a. Server membaca baris pertama dari request menggunakan `BufReader::lines().next().` Baris ini merupakan request line (misalnya, `"GET / HTTP/1.1"`).
b. Dengan melakukan pengecekan terhadap request line, saya bisa menentukan respons yang tepat. Jika request line sama dengan `"GET / HTTP/1.1"`, maka server mengirimkan halaman hello.html dengan status 200 OK. Jika tidak, maka server mengirimkan halaman 404.html dengan status `404 NOT FOUND`.
   
2. Pemisahan Logika Response
a. Penggunaan conditional expression (`if ... else ...`) untuk mengatur tuple (`status_line`, `filename`) memungkinkan pemisahan logika respons. Hal ini memudahkan penambahan route baru atau penyesuaian validasi di masa mendatang.
b. Refactoring ini meningkatkan keterbacaan kode karena respons yang dikirim sudah terstruktur dengan jelas berdasarkan validasi request.

3. Penyusunan Response HTTP yang Benar
a. Response HTTP disusun dengan format yang tepat, yaitu:
  - Baris status (misalnya, `HTTP/1.1 200 OK` atau `HTTP/1.1 404 NOT FOUND`).
  - Header, seperti `Content-Length`, yang berisi panjang dari konten HTML.
  - Dua baris kosong (`\r\n\r\n`) yang memisahkan header dengan body.
  - Body yang berisi isi file HTML yang diambil dari file hello.html atau 404.html.
b. Langkah ini menunjukkan pentingnya mengikuti standar HTTP agar browser dapat menginterpretasikan response dengan benar.

Dokumentasi:
![image](https://github.com/user-attachments/assets/91509cb4-530e-4be4-8fcd-9e5f62185fe8)


### Milestone 4
> Add additional reflection notes, put the title clearly such as Commit 4 Reflection notes.
Pada milestone ini, saya menambahkan validasi request agar server dapat merespon berdasarkan apa yang diminta oleh browser. Sebelumnya, server selalu mengembalikan halaman hello.html tanpa memperhatikan isi request.
Poin-Poin Utama
Pada milestone ini, saya menambahkan simulasi respons lambat dengan menyisipkan delay menggunakan `thread::sleep(Duration::from_secs(10))` ketika menerima request dengan path `/sleep`. Maka, jika pengguna mengakses URL `http://127.0.0.1:7878/sleep`, server akan menunggu 10 detik sebelum mengembalikan response.

1. Sifat Single Threaded
- Karena web server yang kita buat berjalan dalam satu thread, setiap request yang masuk akan diproses secara berurutan. Artinya, jika ada satu request yang membutuhkan waktu lama (misalnya, /sleep dengan delay 10 detik), request lainnya harus menunggu hingga proses tersebut selesai.
- Hal ini mengakibatkan keterlambatan (latency) yang signifikan jika banyak pengguna mengakses server secara bersamaan. Contohnya, jika satu pengguna mengakses /sleep sementara pengguna lain mengakses root (/), maka pengguna yang mengakses / pun harus menunggu sampai delay selesai.
  
2. Simulasi Respons Lambat
- Penambahan kode thread::sleep(Duration::from_secs(10)) berguna untuk mensimulasikan situasi di mana server mengalami proses yang berat atau terjadi kemacetan. Dengan simulasi ini, kita dapat melihat secara langsung dampak dari arsitektur single threaded terhadap performa server.
- Penggunaan simulasi seperti ini sangat membantu dalam memahami kenapa server yang di-deploy di lingkungan produksi biasanya menggunakan multithreading atau asynchronous processing untuk menangani request secara paralel.

### Milestone 5
> Add additional reflection notes, put the title clearly such as Commit 5 Reflection notes.

Pada milestone ini, saya mengubah arsitektur web server dari single-threaded menjadi multithreaded dengan menggunakan ThreadPool. Perubahan ini sangat penting untuk meningkatkan performa server, karena memungkinkan server menangani beberapa request secara bersamaan. Berikut adalah beberapa poin pembelajaran yang saya dapatkan:
1. Pengenalan ThreadPool
- Sebelumnya, server berjalan dalam satu thread sehingga setiap request harus menunggu jika ada request lain yang sedang diproses (misalnya, request dengan delay).
- Dengan menggunakan ThreadPool, saya membuat sejumlah worker thread (dalam contoh ini 4 thread) yang akan mengeksekusi tugas-tugas (jobs) secara paralel. Hal ini membuat server mampu menangani lebih banyak request secara bersamaan dan meningkatkan skalabilitas.
  
2. Mekanisme Kerja ThreadPool
- Pengiriman Tugas:
Setiap request yang masuk diubah menjadi sebuah job (closure yang dikemas dalam Box<dyn FnOnce() + Send + 'static>) dan dikirim melalui channel (mpsc::Sender<Job>) ke para worker.
- Sinkronisasi:
Penerima (receiver) dari channel tersebut dibungkus dengan Arc<Mutex<Receiver<Job>>> agar dapat diakses secara aman oleh semua worker thread secara bersamaan.
- Worker Thread:
Setiap worker dalam ThreadPool menjalankan loop yang terus-menerus mencoba menerima job dari channel. Jika berhasil, worker mencetak pesan log (misalnya, “Worker {id} got a job; executing.”) dan mengeksekusi job tersebut.

3. Keunggulan Pendekatan Multithreaded
- Concurrency:
Dengan adanya thread pool, beberapa request dapat diproses secara simultan, sehingga respons server menjadi lebih cepat meskipun ada satu atau lebih request yang memerlukan waktu lama (contohnya request /sleep).
- Efisiensi Sumber Daya:
Dibandingkan dengan membuat thread baru untuk setiap request, penggunaan thread pool mengurangi overhead dengan membatasi jumlah thread aktif pada waktu tertentu.
- Skalabilitas:
Model ini merupakan dasar yang baik untuk membangun web server yang scalable. Di aplikasi nyata, biasanya akan ditambahkan mekanisme untuk mengatur jumlah thread secara dinamis sesuai beban.
