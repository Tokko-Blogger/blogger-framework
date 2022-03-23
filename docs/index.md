![20191225_155027.png](https://user-images.githubusercontent.com/21377149/154627826-44cb3ebf-5df4-4ed5-8415-64d4c70d2e2d.png)
# Twinny Framework Script - Extension

Twinny Framework Script On Github, Twinny framework ini dikhususkan untuk platform Blogger dan automatis Scan BlogID blogger anda

## Manifest sources Framewok

File manifes ketergantungan dapat ditentukan dalam dua cara - file manifes ketergantungan atau dalam file konfigurasi berlisensi sebagai kumpulan pola yang digunakan untuk menemukan file.

Manifes dimuat dari (secara berurutan)
- File manifes, jika ditemukan
- File konfigurasi berlisensi, jika file manifes tidak ditemukan dan properti konfigurasi `manifest.json` ada.

### Manifest files

File manifes digunakan untuk mencocokkan file sumber dengan paket terkait untuk menemukan dependensi paket. Jalur file manifes dapat ditentukan dalam konfigurasi aplikasi dengan pengaturan berikut:
```
"Matches" : 
{
  "https://*.blogger.com/*",
  "https://blogger.com/*"
 }
```

Jika jalur manifest tidak ditentukan untuk aplikasi, file akan dicari di aplikasi`<root_path>/manifest.json`.

Manifes dapat berupa file JS dengan objek root tunggal dan properti yang memetakan jalur file ke nama paket.
```JS
{
  "path/file-app/theme-options.js",
  "path/file-app/theme-menus.js",
  "path/file-app/theme-translate.js",
  "path/file-app/theme-widgets.js",
  "path/file-app/theme-demos.js",
  "path/file-app/theme-updates.js",
}
```

Jalur file relatif terhadap root repositori git. File metadata, `path/root/manifest.json`.txt, akan dibuat untuk setiap paket.

**NOTE** Adalah tanggung jawab pemilik repositori untuk memelihara file manifes.

Ini menunjukkan bahwa
1. Untuk Reading `Javascript` pada Path Tersebut
2. Penyertaan dan pengecualian berlaku untuk `BlogID` jika tidak terdapat / unindetify
3.Pola mengikuti format script pada `<PATH>/JS/`


#### Fitur-Fitur `Twinny Framework Dashboard- Extension` Platform `Blogger`

Pola ini dievaluasi menggunakan [Dir.js] dan harus mengikuti aturan ini:
1. Code `<template>` 
2. Update [`Pembaharuan Template Jika mendapatkan update template terbaru`]
3. Demo - Dapat Menginstall Tema jika template terdapat tema
4. Translate - Translate template dengan Mode Terbaru
5. Menu - Drag and Drop menu atau tambahkan mehu sesuai keinginan
6. Options - Pengaturan template yang dapat anda gunakan untuk mengaktifkan fitur-fitur template
7. `!` perubahan template `static` menjadi `sticky` pada css
   - menghilangkan fitur template yang tidak diinginkan `<b:if cond="false">`
   - Activation Template `!` (Wajib diinstall)
8. Pola akan match dengan Kode `<script>`

**NOTE** Jika pola pertama, atau satu-satunya, untuk dependensi adalah pola negatif, hal itu tidak akan memengaruhi kumpulan file yang cocok dengan dependensi. Pola inklusi harus selalu ditentukan sebelum pola negatif untuk ketergantungan.


### Script Sumber License 

Ketika file yang berisi konten lisensi tidak ditemukan untuk sekelompok file sumber,
Berlisensi akan mencoba mengurai teks lisensi dari komentar file sumber.

Ada beberapa batasan pada fungsi ini:

1. Komentar HARUS berisi pernyataan hak cipta
2. Komentar HARUS berupa komentar multibaris gaya-C, mis. `/* komentar */`
3. Komentar HARUS berisi lekukan identik untuk setiap baris konten.

Contoh berikut semuanya :+1:. Berlisensi akan mencoba mempertahankan pemformatan,
namun untuk hasil terbaik, komentar tidak boleh mencampur tab dan spasi di spasi putih awal.
```
/*
   <copyright statement>

   <license text>
 */

/* <copyright statement>
   <license text>
 */

/*
 * <copyright statement>
 * <license text>
 *
 * <license text>
 */
```

### From license files specified in the configuration

Jika semuanya gagal, jalur ke file lisensi ketergantungan dapat ditentukan secara manual
dalam konfigurasi. Semua jalur harus relatif terhadap root repositori.

```
const= 'path-file-yang-ditentukan'
```

### License content versioning

Sumber manifes mendukung beberapa strategi pembuatan versi untuk menentukan apakah metadata ketergantungan yang di-cache sudah usang. Strategi versi dipilih berdasarkan konfigurasi aplikasi saat ini.

1. Git commit SHA - Strategi ini menggunakan Git commit SHA terbaru yang tersedia untuk direktori jalur impor paket sebagai versi. Ini adalah strategi default yang digunakan jika tidak dikonfigurasi.
    - :warning: Git commit terbaru tidak akan menangkap perubahan apa pun yang dilakukan bersamaan dengan pembaruan file yang di-cache. Pastikan untuk memperbarui file yang di-cache setelah semua perubahan lain dilakukan.

   ```yaml
   version_license: license_tokkoblogger # atau biarkan kunci ini tidak disetel
   ```
2. Hash konten - Strategi ini menggunakan hash file di direktori jalur impor paket sebagai versi.
   ```yaml
   version_license: <path-file-template>
   ```
   
   ### SELESAI DAN TERIMAKASIH 
