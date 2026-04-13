# Pertemuan 4: Struktur Data Lanjutan (Array, Slice, dan Map)

Dalam aplikasi nyata, kita jarang menyimpan data satu per satu di dalam variabel terpisah. Kita butuh wadah yang bisa menampung banyak data sekaligus. Golang memiliki tiga struktur data utama untuk ini: Array, Slice, dan Map.

## 1. Array (Si Kaku)  
Array adalah kumpulan data yang tipe datanya sama, tetapi **ukurannya tetap (tidak bisa ditambah atau dikurangi)** setelah dibuat. Di industri, Array jarang digunakan secara langsung, tetapi menjadi pondasi bagi Slice.

```go
package main
import "fmt"

func main() {
    // Array dengan kapasitas pas 3 slot
    var loker [3]string
    loker[0] = "Buku"
    loker[1] = "Tas"
    loker[2] = "Laptop"
    
    // loker[3] = "Sepatu" // INI AKAN ERROR karena slot maksimal hanya 3
    fmt.Println(loker)
}
```

## 2. Slice (Si Fleksibel)  
Slice adalah "Array yang dinamis". Ini adalah struktur data yang **paling sering digunakan** di Golang. Ukurannya bisa bertambah secara otomatis jika kita menambahkan data baru menggunakan fungsi `append`.

```go
    // Deklarasi Slice (Tanpa angka di dalam kurung siku)
    keranjang := []string{"Apel", "Mangga"}

    // Menambahkan data baru di akhir
    keranjang = append(keranjang, "Jeruk")
    keranjang = append(keranjang, "Pisang")

    fmt.Println("Isi Keranjang:", keranjang)
    fmt.Println("Jumlah buah:", len(keranjang)) // len() untuk menghitung jumlah data
```

## 3. Map (Kamus / Key-Value)  
Jika Slice menggunakan angka/indeks (0, 1, 2) untuk mencari data, **Map menggunakan kata kunci (Key)**. Ini sangat mirip dengan struktur data JSON pada API.

```go
    // map[TipeKey]TipeData
    hargaMenu := map[string]int{
        "Kopi": 15000,
        "Teh":  10000,
    }

    // Menambah data baru ke Map
    hargaMenu["Roti"] = 12000

    // Mengambil data spesifik
    fmt.Println("Harga Kopi:", hargaMenu["Kopi"])

    // Menghapus data dari Map
    delete(hargaMenu, "Teh")
```

---

### **Tips Analogi untuk Pengajar**

* **Array vs Slice:** Ibaratkan **Array itu seperti Rak Sepatu**. Kalau raknya cuma 5 tingkat, ya cuma muat 5 sepatu. Kalau mau nambah, harus beli rak baru. Sedangkan **Slice itu seperti Gerbong Kereta Api**. Saat penumpang penuh, kita tinggal panggil fungsi `append`, dan otomatis gerbong baru akan tersambung di belakang.  
* **Map:** Ibaratkan **Kontak di HP (Buku Telepon)**. Kita tidak menghafal "Teman saya ada di urutan ke-15" (itu Slice). Kita mencarinya pakai Nama (Key). "Cari kontak bernama *Budi*, lalu tampilkan *Nomor HP-nya* (Value)".

---

### **Tugas Mandiri (Studi Kasus: Sistem Manajemen Warung)**

**Tantangan: "Aplikasi Kasir dan Keranjang Warung"**  
Buatlah sebuah program Go dengan ketentuan:  
1.  Buat folder dan inisialisasi module baru bernama `tugas-warung`.  
2.  Buat sebuah **Map** bernama `daftarHarga` yang berisi minimal 3 barang dan harganya (misal: "Beras": 12000, "Telur": 3000, "Minyak": 15000).  
3.  Buat sebuah **Slice** bernama `keranjang` dengan tipe `string` (awalnya kosong) untuk menampung nama barang yang dibeli.  
4.  Gunakan `for {}` (*Infinite Loop*) untuk menampilkan input terminal yang meminta pengguna mengetik nama barang yang ingin dibeli.  
5.  Setiap kali pengguna mengetik nama barang:  
    - Masukkan nama barang tersebut ke dalam `keranjang` menggunakan `append`.  
    - Tampilkan pesan: "[Nama Barang] berhasil dimasukkan ke keranjang."  
6.  Jika pengguna mengetik **"selesai"**, hentikan perulangan menggunakan `break`.  
7.  **Tantangan Ekstra:** Setelah perulangan selesai, gunakan perulangan `for` untuk membaca isi `keranjang`, cocokkan namanya dengan `daftarHarga`, dan hitung **Total Belanjaan**.  

**Output yang Diharapkan:**
```text
=== WARUNG GOLANG ===
Ketik nama barang (ketik 'selesai' untuk bayar):
> Beras
Beras masuk ke keranjang.
> Telur
Telur masuk ke keranjang.
> Telur
Telur masuk ke keranjang.
> selesai

=== STRUK BELANJA ===
Isi Keranjang : [Beras Telur Telur]
Total Belanja : Rp. 18000
Terima kasih!
```
*(Catatan Guru: Untuk mencari total, siswa harus meloop slice `keranjang` di akhir program, lalu menjumlahkan nilainya dari map `daftarHarga` ke dalam sebuah variabel `total`)*.