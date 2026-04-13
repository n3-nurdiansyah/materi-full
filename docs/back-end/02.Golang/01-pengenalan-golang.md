### **1. Isi File Markdown (`Pertemuan-01.md`)**

Anda bisa membagikan modul di bawah ini kepada murid-murid Anda:

# Pertemuan 1: Pengenalan Golang & Setup Environment

## 1. Apa itu Golang?
Go (atau Golang) adalah bahasa pemrograman yang dibuat oleh Google. Didesain untuk:  
- **Kecepatan:** Performa mendekati C/C++.  
- **Kesederhanaan:** Sintaksis bersih dan mudah dibaca.  
- **Konkurensi:** Sangat andal dalam menangani banyak proses sekaligus (Backend modern).  

## 2. Instalasi & Setup  
1. Download installer di [golang.org](https://golang.org/dl/).  
2. Verifikasi instalasi di terminal/CMD:  
   ```bash
   go version
   ```
3. Gunakan VS Code dengan ekstensi "Go" dari Google.  

## 3. Inisialisasi Proyek (Go Modules)
Selalu gunakan Go Modules agar manajemen library lebih rapi.  
```bash
mkdir belajar-golang
cd belajar-golang
go mod init belajar-golang
```

## 4. Struktur Kode "Hello World"
Buat file bernama `main.go`:  
```go
package main

import "fmt"

func main() {
    fmt.Println("Halo, ini aplikasi Go pertama saya!")
}
```

## 5. Menjalankan Kode
- **Tanpa kompilasi (Langsung):**
  ```bash
  go run main.go
  ```
- **Kompilasi menjadi file binary (.exe di Windows):**
  ```bash
  go build main.go
  ```

---

### **2. Penjelasan Sederhana untuk Murid**

Saat menjelaskan kepada murid, Anda bisa menggunakan analogi sederhana ini agar mereka tidak terintimidasi oleh kode:

1.  **`package main`**: Ibarat "Label Alamat". Go perlu tahu bahwa file ini adalah pintu masuk utama (Entry Point) dari aplikasi. Tanpa `package main`, aplikasi tidak bisa dijalankan sebagai program mandiri.  
2.  **`import "fmt"`**: Singkatan dari *Format*. Ini adalah kotak perkakas yang disediakan Go untuk urusan input dan output (seperti menampilkan tulisan ke layar).  
3.  **`func main()`**: Ini adalah "Jantung" program. Semua instruksi yang ada di dalam kurung kurawal `{ ... }` adalah yang pertama kali dieksekusi saat aplikasi dinyalakan.  
4.  **`go run` vs `go build`**: `go run` itu seperti memasak mie instan dan langsung dimakan untuk *testing*. Sedangkan `go build` itu seperti memasak, lalu membungkusnya ke dalam kemasan (menjadi file `.exe`) agar bisa dikirim dan dijalankan di komputer orang lain tanpa perlu menginstal Go.  

---

### **3. Tugas Mandiri (Studi Kasus: Sistem Profil Sekolah)**

Agar murid bisa langsung praktik dan tidak hanya sekadar *copy-paste*, berikan tantangan ini:

**Tantangan: "The School Identity"**
Buatlah sebuah program Go baru dengan ketentuan sebagai berikut:  
1.  Buat folder baru bernama `tugas-sekolah`.  
2.  Inisialisasi modul dengan nama yang sama.  
3.  Buat file `main.go` yang menampilkan informasi profil sekolah menggunakan `fmt.Println`, dengan data:  
    - Nama Sekolah.  
    - Tahun Berdiri.  
    - Akreditasi (A/B/C).  
    - Moto Sekolah.  
4.  **Output yang diharapkan di terminal:**
    ```text
    === PROFIL SMK INFORMATIKA ===
    Berdiri Tahun: 2010
    Akreditasi: A
    Moto: "Inovasi Tanpa Batas"
    ==============================
    ```