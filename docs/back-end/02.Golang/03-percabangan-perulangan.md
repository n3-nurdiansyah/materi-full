# Pertemuan 3: Logika Percabangan & Perulangan (Real-World Patterns)

Aplikasi *backend* harus efisien dan aman. Di Golang, kita sangat mengutamakan penulisan kode yang ringkas dan *to-the-point*. Hari ini kita akan mempelajari pola logika yang paling sering digunakan oleh *Go Engineer* di proyek nyata.

## 1. Percabangan Dasar (If - Else)  
Digunakan untuk mengecek kondisi Benar atau Salah. Di Go, kondisi tidak perlu diapit tanda kurung `()`, membuat kode lebih bersih.

```go
package main

import "fmt"

func main() {
    statusServer := "Aktif"

    if statusServer == "Aktif" {
        fmt.Println("Server berjalan normal.")
    } else {
        fmt.Println("Peringatan: Server mati!")
    }
}
```

## 2. Percabangan "Satu Baris" (If with Short Statement)  
Ini adalah "Gaya Golang" sesungguhnya. Kita bisa membuat variabel, melakukan proses, sekaligus mengecek kondisinya dalam satu baris `if`. Sangat sering dipakai untuk mengecek *error* atau hasil kalkulasi agar variabelnya tidak mengotori memori utama.

```go
// Rumus: if [inisialisasi]; [kondisi] { ... }

if sisaStok := 10 - 8; sisaStok < 5 {
    // Variabel sisaStok HANYA BISA dipakai di dalam kurung kurawal ini
    fmt.Printf("Peringatan! Stok hampir habis. Sisa: %d\n", sisaStok)
}
// fmt.Println(sisaStok) // JIKA DITULIS DISINI AKAN ERROR, memori langsung dibersihkan.
```

## 3. Perulangan (The "Go" Way)  
Golang hanya punya satu kata kunci untuk perulangan: `for`. Tidak ada `while` atau `do-while`. Di proyek nyata, kita sering memakai 2 pola yang paling mudah ditulis ini:

**A. For sebagai "While" (Condition Only)**  
Hanya menggunakan satu kondisi. Selama kondisi terpenuhi, perulangan jalan terus. Sering dipakai untuk memonitor status.
```go
baterai := 3

for baterai > 0 {
    fmt.Println("Drone terbang. Sisa baterai:", baterai)
    baterai-- // Kurangi 1
}
fmt.Println("Drone mendarat.")
```

**B. For Tanpa Batas (Infinite Loop) + Break**  
Tidak ada kondisi yang ditulis di awal. Program akan berulang selamanya (`for {}`) sampai dipaksa berhenti dengan `break`. Ini pola wajib untuk membuat *server* atau aplikasi yang menunggu ketikan *user*.
```go
for {
    fmt.Println("Sistem memantau pergerakan...")
    // Bayangkan jika ada pergerakan terdeteksi:
    adaPergerakan := true 

    if adaPergerakan {
        fmt.Println("Penyusup terdeteksi! Menghentikan pemantauan.")
        break // Hentikan perulangan paksa
    }
}
```

### **Tugas Mandiri (Studi Kasus: Terminal ATM)**

**Tantangan: "Simulasi Mesin ATM Sederhana"**  
Buatlah sebuah program Go dengan ketentuan:  
1.  Buat folder dan inisialisasi module baru bernama `tugas-atm`.  
2.  Gunakan pola **Infinite Loop (`for {}`)** untuk membuat layar utama ATM yang terus menyala.  
3.  Di dalam perulangan, tampilkan menu:  
    `1. Cek Saldo`  
    `2. Tarik Tunai`  
    `3. Keluar (Ambil Kartu)`  
4.  Gunakan `fmt.Scanln` untuk meminta pilihan pengguna.  
5.  Gunakan **If-Else** dasar:  
    - Jika pilih 1: Tampilkan "Saldo Anda: Rp. 5.000.000".  
    - Jika pilih 2: Minta pengguna memasukkan nominal. (Tidak perlu dihitung pengurangannya dulu, cukup tampilkan "Anda menarik uang sebesar: [nominal]").  
    - Jika pilih 3: Tampilkan "Terima kasih telah bertransaksi", lalu gunakan **`break`** agar mesin ATM (perulangan) berhenti beroperasi.  

**Output yang Diharapkan:**
```text
=== ATM GOLANG ===
1. Cek Saldo
2. Tarik Tunai
3. Keluar
Pilih menu: 1
Saldo Anda: Rp. 5.000.000

=== ATM GOLANG ===
1. Cek Saldo
2. Tarik Tunai
3. Keluar
Pilih menu: 3
Terima kasih telah bertransaksi.
(Program Selesai)
```