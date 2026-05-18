## Experiment 1.2: Understanding how it works

Pada eksperimen ini, saya menambahkan baris berikut setelah `spawner.spawn(...)`:

```rust
println!("Mirza's Komputer: hey hey");
```

Hasil Eksekusi

Output program:

![alt text](images/1.2.png)

Penjelasan

Output `Mirza's Komputer: hey hey` muncul terlebih dahulu karena baris tersebut berada di luar asynchronous task. Baris tersebut langsung dieksekusi oleh fungsi main sebelum `executor.run()` dipanggil.

Sementara itu, kode di dalam `spawner.spawn(...)` tidak langsung dijalankan ketika spawn dipanggil. Fungsi spawn hanya memasukkan task ke dalam antrean task. Task tersebut baru mulai dijalankan ketika `executor.run()` dipanggil.

Setelah executor mulai berjalan, task asynchronous akan dipoll. Karena itu, output `Mirza's Komputer: howdy!` muncul setelah hey hey.

Kemudian program menunggu TimerFuture selama dua detik. Setelah timer selesai, task dibangunkan kembali dan executor melanjutkan eksekusi task tersebut. Oleh karena itu, output `Mirza's Komputer: done!` muncul terakhir.