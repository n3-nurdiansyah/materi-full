# Pertemuan 5: Function dan Error Handling

Seiring membesarnya aplikasi, kita tidak mungkin menumpuk semua kode di dalam `func main()`. Kita harus memecahnya menjadi potongan-potongan kecil yang bisa digunakan berulang kali. 

## 1. Function (Fungsi)  
Function adalah blok kode yang diberi nama dan dibuat untuk melakukan tugas spesifik. 

**A. Fungsi Dasar & Parameter:**
```go
package main
import "fmt"

// Fungsi yang menerima data (parameter)
func sapaUser(nama string) {
    fmt.Printf("Halo, %s! Selamat datang kembali.\n", nama)
}

func main() {
    sapaUser("Rangga") // Memanggil fungsi
}
```

**B. Multiple Return Values (Keunikan Golang):**  
Di bahasa lain, fungsi biasanya hanya bisa mengembalikan 1 nilai. Di Go, fungsi bisa mengembalikan 2 nilai atau lebih sekaligus. Ini sangat berguna!
```go
func hitungLuasKeliling(p, l int) (int, int) {
    luas := p * l
    keliling := 2 * (p + l)
    return luas, keliling
}

func main() {
    // Menangkap 2 nilai sekaligus
    hasilLuas, hasilKeliling := hitungLuasKeliling(10, 5)
    fmt.Println("Luas:", hasilLuas, "Keliling:", hasilKeliling)
}
```

## 2. Error Handling (Cara Golang)
Golang tidak menggunakan `try-catch` seperti Java atau PHP. Di Go, *Error* diperlakukan sebagai sebuah nilai biasa yang dikembalikan oleh fungsi. 

```go
import (
    "errors"
    "fmt"
)

// Mengembalikan hasil pembagian DAN error (jika ada)
func bagiAngka(a, b int) (int, error) {
    if b == 0 {
        return 0, errors.New("gagal: tidak bisa membagi dengan angka nol")
    }
    return a / b, nil // nil berarti "Kosong" (Tidak ada error)
}

func main() {
    hasil, err := bagiAngka(10, 0)
    
    // Pola Wajib Golang: Cek apakah error tidak kosong (!= nil)
    if err != nil {
        fmt.Println("Terjadi Kesalahan:", err.Error())
        return // Hentikan proses
    }
    
    fmt.Println("Hasil pembagian:", hasil)
}
```

### **Tugas Mandiri (Studi Kasus: E-Wallet)**

**Tantangan: "Sistem Pembayaran E-Wallet Sederhana"**  
Buatlah sebuah program Go dengan ketentuan:  
1.  Buat folder dan inisialisasi module baru bernama `tugas-ewallet`.  
2.  Buat sebuah fungsi bernama `bayarTagihan` dengan parameter:  
    - `saldo`
    - `jumlahTagihan` (bertipe integer biasa `int`)  
    - Mengembalikan tipe data `error`.  
3.  Di dalam fungsi `bayarTagihan`:  
    - Jika `*saldo` kurang dari `jumlahTagihan`, kembalikan *error* dengan pesan "Saldo tidak mencukupi!".  
    - Jika cukup, kurangi `*saldo` dengan `jumlahTagihan`, lalu kembalikan `nil` (tidak ada error).  
4.  Di dalam `func main()`:  
    - Buat variabel `saldoUtama` sebesar 50.000.  
    - Coba lakukan pembayaran pertama sebesar 30.000 menggunakan fungsi `bayarTagihan(&saldoUtama, 30000)`. Cek errornya, jika sukses tampilkan sisa saldo.  
    - Coba lakukan pembayaran kedua sebesar 25.000. Cek errornya. Karena saldo sisa 20.000, harusnya pembayaran ini gagal dan menampilkan pesan error.  

**Output yang Diharapkan:**
```text
=== TRANSAKSI 1 (Rp. 30.000) ===
Pembayaran Berhasil! Sisa Saldo: Rp. 20000

=== TRANSAKSI 2 (Rp. 25.000) ===
Pembayaran Gagal: Saldo tidak mencukupi!
Sisa Saldo Akhir: Rp. 20000
```