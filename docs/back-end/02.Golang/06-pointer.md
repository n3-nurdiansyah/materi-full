# Pertemuan 6: Pointer

## 1. Pendahuluan: Apa itu Pointer?

Dalam pemrograman, variabel adalah tempat menyimpan data. Namun, data tersebut sebenarnya duduk di sebuah alamat fisik di dalam memori (RAM). **Pointer** adalah sebuah variabel yang isinya bukan data (seperti angka atau teks), melainkan **alamat memori** dari variabel lain.

### Analogi Dunia Nyata

Jika variabel biasa adalah **Rumah**, maka Pointer adalah **Secarik kertas berisi alamat rumah tersebut**.

- **Mengubah isi rumah:** Datang langsung dan ganti catnya.

- **Mengubah via pointer:** Lihat alamat di kertas, datangi rumah di alamat tersebut, lalu ganti catnya.

---

## 2. Operator Dasar Pointer

Ada dua simbol keramat yang harus kalian hafal di luar kepala:

1. `&` (**Ampersand** / *Address-of*): Digunakan untuk mengambil alamat memori dari sebuah variabel.

2. `*` (**Asterisk** / *Dereferencing*): Digunakan untuk mengakses atau mengubah nilai yang ada di alamat tersebut.

### Contoh Dasar (Tanpa Function)

```go
package main

import "fmt"

func main() {
    nama := "Abqory" // Variabel biasa
    
    // Kita buat pointer yang menunjuk ke alamat 'nama'
    var pointerNama *string = &nama 

    fmt.Println("Isi variabel nama:", nama)          
    fmt.Println("Alamat variabel nama:", &nama)      
    fmt.Println("Isi dari pointerNama:", pointerNama) 

    // MENGUBAH DATA VIA ALAMAT (Dereferencing)
    // Kita gunakan tanda bintang untuk "masuk" ke alamat tersebut
    *pointerNama = "Fawwaz"

    fmt.Println("Nama setelah diubah via pointer:", nama) // Output: Fawwaz
}
```

---

## 3. Pointer dalam Function

Secara default, Golang menggunakan sistem *Pass by Value*. Jika kalian mengirim variabel ke function tanpa pointer, Golang akan membuat "copy" atau duplikatnya. Perubahan di dalam function **tidak akan** merubah variabel asli di luar.

**Solusinya?** Kirim alamatnya menggunakan Pointer.

### Contoh Kasus: Update Saldo Tabungan

```go
package main

import "fmt"

func tambahSaldo(saldo *int, nominal int) {
    // Kita gunakan *saldo untuk mengubah nilai di alamat aslinya
    *saldo = *saldo + nominal
}

func main() {
    tabungan := 100000
    
    // Kita kirim alamatnya menggunakan simbol &
    tambahSaldo(&tabungan, 50000)

    fmt.Println("Total Tabungan Sekarang:", tabungan) // Output: 150000
}
```

---

## 4. Level Pro: Pointer Receiver Method

Dalam standar industri, kita sering menempelkan fungsi langsung ke sebuah `struct` (objek). Ini disebut **Method**. Agar method tersebut bisa mengubah isi data objek yang asli, kita wajib gunakan **Pointer Receiver**.

### Contoh Kasus: Sistem Update Profil User

```go
package main

import "fmt"

type User struct {
    Username string
    Email    string
}

// Method ini 'menempel' pada User menggunakan pointer receiver (*User)
func (u *User) GantiEmail(emailBaru string) {
    u.Email = emailBaru
    fmt.Println("Log: Email berhasil diubah!")
}

func main() {
    user1 := User{Username: "rangga_dev", Email: "lama@gmail.com"}

    fmt.Println("Email Lama:", user1.Email)

    // Memanggil method (Pointer diatur otomatis oleh Golang)
    user1.GantiEmail("baru@gmail.com")

    fmt.Println("Email Baru:", user1.Email)
}
```

*Catatan: Menggunakan pointer pada method jauh lebih efisien memori karena komputer tidak perlu menyalin ulang seluruh data objek (struct) ke dalam fungsi.*

---

## 5. Tugas Mandiri (Studi Kasus)

**Judul Tugas: Sistem Manajemen Stok Toko Sederhana**

**Instruksi:**

1. Buatlah sebuah `struct` bernama `Produk` yang memiliki field: `Nama` (string), `Harga` (int), dan `Stok` (int).

2. Buatlah sebuah **Method** dengan **Pointer Receiver** bernama `KurangiStok` yang menerima parameter `jumlah` (int). Method ini harus mengurangi field `Stok` berdasarkan jumlah yang dimasukkan.

3. Buatlah sebuah **Function Biasa** (bukan method) bernama `DiskonProduk` yang menerima parameter `p *Produk` dan `persen` (int). Function ini harus mengubah `Harga` produk tersebut setelah dipotong diskon.

4. Di dalam `func main()`:
   - Buat satu objek produk (Contoh: "Keyboard Mechanical", Harga: 500000, Stok: 10).
   - Panggil method `KurangiStok` sebanyak 2 unit.
   - Panggil function `DiskonProduk` sebesar 10%.
   - Tampilkan data produk terakhir (Nama, Stok, dan Harga).

**Output yang diharapkan:**
Stok harus menjadi 8 dan Harga harus menjadi 450000.

---
*Tips: Jika kalian bingung kapan pakai `*` dan `&`, ingat ini: `&` untuk mendapatkan alamatnya, `*` untuk mengolah isinya.*