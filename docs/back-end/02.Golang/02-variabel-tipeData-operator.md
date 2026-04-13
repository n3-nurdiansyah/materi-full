# Pertemuan 2: Variabel, Tipe Data, dan Operator

## 1. Apa itu Variabel?  
Variabel adalah wadah atau tempat untuk menyimpan data sementara di dalam memori komputer. Di Golang, ada dua cara mendeklarasikan variabel:

**Cara Eksplisit (Menggunakan `var`):**
Digunakan jika kita ingin menyiapkan wadahnya dulu, tapi datanya diisi nanti.
```go
var namaSiswa string
namaSiswa = "Haidar"
```

**Cara Singkat (Type Inference `:=`):**
Sangat populer di Go. Kita tidak perlu menuliskan tipe datanya, Go otomatis menebak dari isinya.
```go
nilaiUjian := 85 // Go otomatis tahu ini Integer (Angka bulat)
```

## 2. Tipe Data Primitif
Setiap variabel harus punya tipe data yang jelas.  
- **String:** Untuk teks. Selalu diapit tanda kutip ganda. Contoh: `"Pemrograman Backend"`.  
- **Integer (`int`):** Untuk angka bilangan bulat. Contoh: `10`, `-50`, `2026`.  
- **Float (`float64`):** Untuk angka desimal. Gunakan titik. Contoh: `3.14`, `85.5`.  
- **Boolean (`bool`):** Hanya memiliki dua nilai, yaitu `true` (benar) atau `false` (salah).

## 3. Konstanta (`const`)
Konstanta mirip seperti variabel, tetapi **nilainya mutlak dan tidak bisa diubah** setelah dibuat. Sangat aman untuk menyimpan data yang sifatnya tetap.
```go
const tarifPajak = 11
const namaAplikasi = "My POS App"
```

## 4. Operator Aritmatika & Interaksi Pengguna
Untuk membuat kalkulator, kita butuh operator matematika dasar:  
- `+` (Penjumlahan)  
- `-` (Pengurangan)  
- `*` (Perkalian)  
- `/` (Pembagian)  
- `%` (Modulus / Sisa Hasil Bagi)  

Sedangkan untuk meminta input dari pengguna di terminal, kita menggunakan `fmt.Scan` atau `fmt.Scanln`.

**Contoh: Program Penghitung Umur Sederhana**
```go
package main

import "fmt"

func main() {
    var nama string
    var tahunLahir int

    // Meminta input Nama
    fmt.Print("Masukkan nama Anda: ")
    fmt.Scanln(&nama) // Simbol & (Pointer) wajib digunakan saat Scan untuk menyimpan data ke alamat memori

    // Meminta input Tahun Lahir
    fmt.Print("Masukkan tahun lahir: ")
    fmt.Scanln(&tahunLahir)

    // Proses Kalkulasi
    umur := 2026 - tahunLahir

    // Output dengan format terstruktur (Printf)
    // %s untuk String, %d untuk Angka (Digit)
    fmt.Printf("\nHalo %s! Umur kamu tahun ini diperkirakan %d tahun.\n", nama, umur)
}
```

---

### **Tugas Mandiri (Studi Kasus: Sistem Kasir Kantin)**

**Tantangan: "Kalkulator Diskon Kantin"**
Buatlah sebuah program Go dengan ketentuan sebagai berikut:  
1.  Buat folder dan inisialisasi module baru bernama `tugas-kasir`.  
2.  Program akan meminta pengguna memasukkan **Harga Makanan** (angka) dan **Jumlah Porsi** (angka) yang dibeli.  
3.  Hitung **Total Harga** (Harga Makanan * Jumlah Porsi).  
4.  Kantin sedang berbaik hati, berikan **Diskon tetap sebesar 10%** dari Total Harga (Gunakan operator pembagian atau perkalian desimal).  
5.  Hitung **Total Bayar** (Total Harga - Diskon).  
6.  Tampilkan struk belanja yang rapi di terminal.

**Contoh Output yang Diharapkan:**
```text
=== KASIR KANTIN SEKOLAH ===
Harga per porsi : 15000
Jumlah porsi    : 2
----------------------------
Total Harga     : 30000
Diskon 10%      : 3000
Total Bayar     : 27000
============================
```