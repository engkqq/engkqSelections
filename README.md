# eSelections.inc 
 
`eSelections.inc` adalah sebuah *library* (include) kustom untuk framework **open.mp** / SA-MP yang dirancang untuk membuat antarmuka pemilihan model visual (Skin, Kendaraan, atau Objek) secara dinamis menggunakan Player TextDraw. 
 
Include ini dibuat sebagai alternatif yang jauh lebih ringan, rapi, dan optimal dibanding `mSelection.inc` lama, dengan memanfaatkan optimasi perulangan (*looping*) grid koordinat untuk menghemat penggunaan alokasi memori TextDraw server. 
 
--- 
 
## Preview Layout 
 
Berikut adalah tampilan menu slot dari `eSelections.inc`: 
 
![eSelections Preview](Screenshot%20(387).png)
 
--- 
 
## Fitur Utama 
 
* **Layout 15 Slot Grid:** Otomatis menyusun hingga 15 item model preview per halaman (3 baris x 5 kolom) secara presisi ke bawah tanpa perlu hardcode koordinat satu per satu. 
* **Dynamic File Loader:** Dapat langsung membaca daftar ID model dari file teks biasa (`.txt`) di dalam folder `scriptfiles`, membuat kamu bisa mengubah daftar isi baju/kendaraan kapan saja tanpa perlu *compile* ulang gamemode. 
* **Player-Based Data Storage:** Menggunakan sistem penyimpanan data berbasis per-player (Enum), menjamin data aman dan tidak akan terjadi bentrok visual atau *bug* halaman jika ada banyak pemain yang membuka menu secara bersamaan. 
* **Interactive Indication:** Warna latar belakang slot otomatis berubah secara real-time saat diklik, berfungsi sebagai penanda visual item mana yang sedang aktif dipilih sebelum dikonfirmasi. 
* **Simpel Callback Integration:** Hasil akhir pilihan pemain langsung dikirim secara instan ke script utama atau filterscript melalui fungsi callback bawaan `OnPlayerSelectEModel`. 
 
--- 
 
## Fungsi yang Tersedia 
 
```pawn 
// Membuka menu menggunakan daftar ID model dari array lokal script 
ShowPlayereSelection(playerid, const headerTitle[], extraid, const models[], total_models); 
 
// Membuka menu dengan membaca file teks secara langsung dari folder scriptfiles 
ShowPlayereSelectionFromFile(playerid, const headerTitle[], extraid, const fileName[]); 
 
// Menutup menu, menghapus memori TextDraw pemain, dan menghilangkan kursor mouse 
HidePlayereSelection(playerid); 
 ```

--- 
 
## Cara Penggunaan Singkat 
 
### 1. Setup File di `scriptfiles` 
Buat file teks di dalam folder `scriptfiles/` (misalnya: `skins_male.txt`) dan isi dengan daftar ID model secara vertikal: 
```text
26 
21 
22 
28 
299 
```
 
### 2. Memanggil Menu di Script 
```pawn
#include <eSelections> 
 
CMD:pilihskin(playerid, params[]) 
{ 
    // Membuka file skins_male.txt dengan penanda ExtraID = 1 
    ShowPlayereSelectionFromFile(playerid, "Pilih Skin Karakter", 1, "skins_male.txt"); 
    return 1; 
}
```

 
### 3. Mengambil Hasil Pilihan via Callback 
```pawn
public OnPlayerSelectEModel(playerid, extraid, index, modelid) 
{ 
    if(extraid == 1) // Cocokkan dengan ExtraID saat memanggil menu 
    { 
        SetPlayerSkin(playerid, modelid); 
        SendClientMessage(playerid, -1, "Kamu berhasil mengganti baju!"); 
    } 
    return 1; 
} 
```
 
--- 
 
## Credits 
* **Engkq** -- Creator & Developer 

---

## Contributors
<div align="center">
 
<a href="https://github.com/engkqq/eSelections/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=engkqq/eSelections" alt="Contributors List" />
</a>

Silakan kirim Pull Request jika ingin menambahkan fitur baru atau memperbaiki bug!
</div>
