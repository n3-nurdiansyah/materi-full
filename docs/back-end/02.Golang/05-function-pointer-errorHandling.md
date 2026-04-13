# Pertemuan 5: Function, Pointer, dan Error Handling

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

## 3. Pointer (Penunjuk Alamat Memori)  
Secara *default*, saat kita mengirim variabel ke dalam fungsi, Go akan "menggandakan" data tersebut (Copy by Value). Jika datanya besar, RAM akan cepat penuh.   
Pointer memungkinkan fungsi mengubah data **asli** di memori tanpa perlu menggandakannya.

- Simbol `&` (Ampersand): Mencari tahu alamat memori.
- Simbol `*` (Asterisk): Mengambil/mengubah nilai di alamat tersebut.

```go
// Tanda *int berarti fungsi ini meminta ALAMAT dari variabel integer
func diskonHarga(hargaAwal *int) {
    // Ubah nilai di alamat aslinya
    *hargaAwal = *hargaAwal - 5000 
}

func main() {
    hargaKopi := 20000
    fmt.Println("Harga Awal:", hargaKopi)

    // Kirim alamat memori hargaKopi menggunakan &
    diskonHarga(&hargaKopi) 

    fmt.Println("Harga Setelah Diskon:", hargaKopi) // Output: 15000
}
```

---

### **Tips Analogi untuk Pengajar**

* **Function (Fungsi):** Ibaratkan **Koki Spesialis**. Anda tidak perlu tahu cara membuat sate, Anda cukup memberikan Daging Mentah (Parameter) kepada Koki Sate, lalu Koki tersebut akan mengembalikan Sate Matang (Return Value) kepada Anda.  
* **Error Handling:** Ibaratkan **Satpam Bandara**. Sebelum Anda (data) diizinkan masuk ke pesawat (proses selanjutnya), barang bawaan Anda selalu dicek. *Ada barang terlarang (error)?* Jika ya, Anda ditahan di tempat (`if err != nil`).  
* **Pointer:** Ini adalah analogi terbaiknya: **Dokumen Skripsi**.   
    * Tanpa Pointer: Anda mengirim file `Skripsi.docx` ke Dosen via Email (Copy). Jika Dosen merevisi dan menyimpannya di laptopnya, file asli di laptop Anda **tidak akan berubah**.  
    * Dengan Pointer: Anda membagikan **Link Google Docs** (`&`). Saat dosen mengubah isinya melalui link tersebut (`*`), dokumen asli milik Anda **ikut berubah**. Ini jauh lebih hemat karena file-nya tetap hanya ada satu.

---

### **Tugas Mandiri (Studi Kasus: E-Wallet)**

**Tantangan: "Sistem Pembayaran E-Wallet Sederhana"**  
Buatlah sebuah program Go dengan ketentuan:  
1.  Buat folder dan inisialisasi module baru bernama `tugas-ewallet`.  
2.  Buat sebuah fungsi bernama `bayarTagihan` dengan parameter:  
    - `saldo` (bertipe pointer integer `*int`)  
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