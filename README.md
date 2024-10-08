# Jarkom-Modul-1-IT18-2024

**KELOMPOK IT18**
| Nama | NRP |
|---------------------------|------------|
|Hazwan Adhikara Nasution | 5027231017 |
|Farand Febriansyah | 5027231084 |

<hr>

### 1. Advance Sanity Check

<img width="649" alt="image" src="https://github.com/user-attachments/assets/de9cb709-41be-4729-ad83-79f9637c5fe9">


`Step Pengerjaan`

- frame contains “username”.
- frame containts “.txt”.
- Di Clue3.txt ada kalimat untuk membuka PPT.
- Saat melihat bagian Peraturan Soal Shift pada PPT terdapat sesuatu yang harus kita decode menggunakan base64.
- Lalu input hasil Decodenya dan Flag pun muncul.

### 2. 22 Nightmare

<img width="651" alt="image" src="https://github.com/user-attachments/assets/2c553345-9cd1-412b-b89d-383b7e36330f">


`Step Pengerjaan`

- Karena diberi formatnya yaitu filename.extension jadi saya mencoba semua extension file, dan yang saya dapatkan di extension .jpg.
- Lalu terlihat nama file Sh1k4.jpg
<img width="1710" alt="image" src="https://github.com/user-attachments/assets/fe4d0dbe-04fc-4d71-bd89-001f13d54387">
- Saya curiga dengan kata kata STOR, oleh karena itu ketika saya filter kata tersebut, saya menemukan 2 file.
<img width="1710" alt="image" src="https://github.com/user-attachments/assets/6ca98f15-9ed3-4996-8cd5-dab96d427668">
- Setelah itu saya select dan export kedua file tersebut.
<img width="1710" alt="image" src="https://github.com/user-attachments/assets/2d64204c-5dcd-4c20-b4eb-8463d453cb6b">
- Ketika dibuka saya menemukan kata "NUN". Selanjutnya, saya follow file yang ke-2 yaitu noko.py dan melihat stream di kanan bawah.
<img width="1710" alt="image" src="https://github.com/user-attachments/assets/10528f12-9486-4a98-bb0d-a90c0951f357">
- Ketika stream 141 kita naikkan 1 menjadi 142, terlihat clue dari noko.py

```bash
Import Shika

Class Noko
    input = int
    key = String
    value = String
    
    # input = 001001100011010000100010001000100011101001101110001001110011100001101110000110100011101000111100001011110011111000100001011011100001111000100001001111010011110100100111
    
    key = jpg msg
    
    op xor bit
```

- Disitu terlihat clue, yaitu kita diminta untuk melakukan operasi XOR dengan key "NUN". Lalu kita lakukan dengan code dibawah ini:

```bash
class Noko:
    def __init__(self, input_binary, key):
        self.input = input_binary
        self.key = key

    def xor_binary(self):
        # Convert input and key to binary strings
        key_bin = ''.join(format(ord(c), '08b') for c in self.key)
        input_len = len(self.input)

        # Repeat key to match the length of the input
        key_bin_repeated = (key_bin * (input_len // len(key_bin) + 1))[:input_len]

        # Perform XOR operation
        result_binary = ''.join(str(int(self.input[i]) ^ int(key_bin_repeated[i])) for i in range(input_len))

        # Convert resulting binary to text
        result_text = ''.join(chr(int(result_binary[i:i+8], 2)) for i in range(0, len(result_binary), 8))
        return result_text

# Example usage:
input_binary = "001001100011010000100010001000100011101001101110001001110011100001101110000110100011101000111100001011110011111000100001011011100001111000100001001111010011110100100111"
key = "NUN"

noko = Noko(input_binary, key)
output = noko.xor_binary()
print(output)

```

dari situ muncul output, `hallo im Torako Koshi`

### 3. Illegal Breakthrough

<img width="652" alt="image" src="https://github.com/user-attachments/assets/e0fc876a-52b6-47cc-a186-c8a735f48453">


`Step Pengerjaan`

- Saat wireshark terbuka, saya langsung coba untuk menggunakan IP Destination yang paling atas lalu saya Follow untuk mendapatkan PORT.
<img width="1710" alt="image" src="https://github.com/user-attachments/assets/56363b90-be1e-44a5-b11b-7f6b37ddb5d4">
- Setelah itu, setelah membaca pertanyaan terkait endpoint yang terdapat login, saya kepikiran untuk filter dengan kata username.
<img width="1710" alt="image" src="https://github.com/user-attachments/assets/092dce21-45e8-4f6f-8813-0f91363b768f">
- Lalu, kita filter -v karena dicari version dan saya melihat dari 3 HTTP yang ada, ada 1 yang berbeda. Terlihat disitu ada versinya setelah di follow.
<img width="1710" alt="image" src="https://github.com/user-attachments/assets/ff84bfef-d7c3-4536-8ac7-fb35e8ecc435">
- Filter dengan http && ip.src eq 172.21.88.207, lalu cari yang FOUND setelah itu follow. terlihat ada username dan password.
<img width="1710" alt="image" src="https://github.com/user-attachments/assets/91a8ec64-19d2-423c-b455-b3b529fc364a">

### 4. Packets Barrage

<img width="651" alt="image" src="https://github.com/user-attachments/assets/8b839aa0-d2dd-4f03-ab8d-aa57cfc54d09">

`Step Pengerjaan`

- Pertama, saya coba untuk masukkan IP Source yang paling atas dan ternyata bisa.
- Kedua, terlihat bahwa ketika kita melakukan filter `http && ip.src eq 172.21.88.207` ada 1 file FOUND, maka dikanan bawah yang terdisplay ada 1918 dapat dikurangkan 1 yaitu 1917.
<img width="1710" alt="image" src="https://github.com/user-attachments/assets/625d94a3-0d04-4720-9545-e6a406ec621d">
- Terakhir, untuk mendapatkan filename.extension, kita bisa follow file yang paling bawah dan terlihat ada Albatros.txt beserta isinya.
<img width="1710" alt="image" src="https://github.com/user-attachments/assets/327d7b81-cd23-459b-aa33-9e048f87c3fb">

### 5. FTP Login

<img width="650" alt="image" src="https://github.com/user-attachments/assets/9e8b7997-049c-4887-9ea4-7bd93d49bf69">

`Step Pengerjaan`

- Filter `ftp` lalu cukup scroll untuk menemukan jawabannya.
<img width="1710" alt="image" src="https://github.com/user-attachments/assets/0d88b527-3256-4378-80c4-70ce93b29fe2">
- Lalu anda akan mendapatkan flag setelah input username dan password.

### 6. Suprise

<img width="649" alt="image" src="https://github.com/user-attachments/assets/f22be560-68bd-4705-9266-4b5f661a8ddf">

`Step Pengerjaan`

- Pertama, kita langsung diminta mencari service yang digunakan FTP server. Kita langsung dapat lakukan frame contains "Login" karena itu berhubungan dengan server dan protocolnya juga FTP.
<img width="1710" alt="image" src="https://github.com/user-attachments/assets/cb96c50b-9ea8-4ac2-8ac2-1e02d72e2ffe">
- Setelah itu, ada satu yang successful, langsung kita follow dan didapatkan servicenya paling atas dan juga ada nama file yang dikirim oleh attacker.
<img width="1710" alt="image" src="https://github.com/user-attachments/assets/07955c7d-b98d-47cd-bb05-34f606ca6a7a">
- Selanjutnya, kita dapat menaikkan satu Stream yang ada di kanan bawah menjadi 5. Maka, kita akan mendapat isi dari g0tcha.cpp yang langsung kita compile untuk mendapatkan jawabannya
<img width="1710" alt="image" src="https://github.com/user-attachments/assets/33c53edd-319f-4595-b558-5c667020373a">
 
### 7. Pegawai Negeri Sebelah

<img width="652" alt="image" src="https://github.com/user-attachments/assets/963be1bc-8c72-43b2-853d-d1aea4d49db5">

`Step Pengerjaan`

- Dari soal pertama kita dapat langsung filter yang tertera di soal.
<img width="1710" alt="image" src="https://github.com/user-attachments/assets/f5cf015e-1672-414b-9863-0e9f7341e200">
- Lalu, saat kita follow file tersebut. Terlihat ada banyak data yang bisa kita find sesuai kebutuhan di bagian bawah.
<img width="1710" alt="image" src="https://github.com/user-attachments/assets/90b7ecc6-b89a-4c46-8838-51644869aac4">
- Semua pertanyaan hanya perlu di find untuk menjawabnya.

### 8. Corporate Breach

<img width="650" alt="image" src="https://github.com/user-attachments/assets/64631a1a-cc8d-4b53-b925-a42cf713290d">

`Step Pengerjaan`

- Saat Wireshark terbuka kita bisa coba follow yang paling atas terlebih dahulu, ternyata disitu tertera nama si attacker.
- Selanjutnya, saya filter "gmail" karena di soal formatnya gmail, dan saya menemukan kejanggalan di satu file.
<img width="1710" alt="image" src="https://github.com/user-attachments/assets/1f4e7ef9-08b0-4fbc-bbe6-b8373ed0f8a3">
- Ternyata benar, ada jawaban dari soalnya yaitu email dan passwordnya. Flag pun kita dapatkan.
<img width="1710" alt="image" src="https://github.com/user-attachments/assets/30b86055-9dd2-467a-9cbd-369580b589ac">

### 9. EZ

<img width="648" alt="image" src="https://github.com/user-attachments/assets/96da33ba-a2fe-4186-96a6-36ddda129818">

`Step Pengerjaan`

- Saat Wireshark terbuka kita bisa coba follow yang paling atas terlebih dahulu, ternyata disitu ada pesan untuk menjawab soal.
<img width="1710" alt="image" src="https://github.com/user-attachments/assets/90cb477e-f53c-4424-8dd1-aa58822c5fb7">
- Untuk port yang digunakan, kita hanya perlu double click yang paling atas dan akan terlihat destination port untuk mendapatkan flag.
<img width="1710" alt="image" src="https://github.com/user-attachments/assets/29f1b3b0-f4f5-4433-a645-359023b9bff8">

### 10. Rizzset
  
   ![image](https://github.com/user-attachments/assets/bc74228a-8057-4211-8754-46ad92e6ae2c)

   ![image](https://github.com/user-attachments/assets/c672a7a9-3abc-4979-af43-c38143eae616)
1. Karena pada soal pertama adalah domain dengan format www.domain.com dan domain yang paling sering muncul adalah 
   its.ac.id maka saya gunakan domain tersebut
2. Kemudian saya gunakan ip 5.189.94.79 karena ip tersebut merupakan ip dari its itu sendiri.
   ![image](https://github.com/user-attachments/assets/c043b4fd-2830-494f-af53-fbc3590686dc)
3. Untuk jarm dari domain saya menggunakan tools jarm sehingga menghasilkan jarm tersebut.

### 11.Gajah Terbang (Attacker Recon)
  
   ![image](https://github.com/user-attachments/assets/c1c6404c-0101-454d-b127-47c30551dc0c)
   *Saya mengambil informasi dari TCP berikut ini*
   ![image](https://github.com/user-attachments/assets/34aefe53-38fe-4b8c-825f-73ddc3c61cb2)
1. Saya mencoba satu satu email atacker dan yang benar adalah kuntoajiisrillll@gmail.com
   ![image](https://github.com/user-attachments/assets/d179bd57-fb21-48a3-b132-47b59f8b5c92)
2. Untuk password saya mendecrypt dari string yang tertera kemudian munculah kissme
3. Untuk tanggal di ban juga dapat di lihat pada TCP yaitu "2024-06-09"
4. Kemudian barang yang dibeli adalah rokok dan es krim yang dapat dilihat pada TCP
5. Jumlahkan harga rokok dan eskrim dan jadi 24.500

### 12.  Malicious Code 

   ![image](https://github.com/user-attachments/assets/8a05d71a-80d7-44d6-9cd7-777aa6d90761)

1. Menggunakan filter ".php" karena pada soa menggunakan format ".php" dan ketika difilter maka akan muncul 52 packets.
   ![image](https://github.com/user-attachments/assets/c1fa0fe6-d71e-4967-9dab-47949a4c1dc7)
2. Endpoint yang berhasil attacker dapatkan adalah "index.php", yaitu login status ok
   ![image](https://github.com/user-attachments/assets/553ca127-e406-4d43-b913-4f69dd9a9696)
3. Attacker melakukan brute force dan berhasil pada ke 153 kali percobaan.
4. ![image](https://github.com/user-attachments/assets/f373698d-57db-4fda-a6f2-72fa623ee571)
   Terdapat kode yang berarti "apa warna favorit pembuat challenge? (hint: sweater)"
5. Dan mendapatkan Flag "JarkomIT{s3cr3t_m3ss4ge_fr0m_4uth0r_07u4Xysoo6AEMlBdKEWnBn0dMC0WEedQTQLtamc9Y5EKfIT0eEGYL0R}"

### 13. Stegography

   ![image](https://github.com/user-attachments/assets/a3866f1a-1b10-45d6-aad9-b4e334f10dc2)

   1. Memfilter dengan "png" dan muncullah jumlah berikut
      ![image](https://github.com/user-attachments/assets/30c783fb-3da2-41bb-8cf5-ff67364bff1a)
   2. Di ekspor menggunakan export object dan menjadi FTP-data
   3. Dekode gambar menggunakan script python yang sudah diberikan namun dimodifikasi sedikit menggunakan GPT agar script berjalan dengan baik, berikut adalah scriptnya
      ![image](https://github.com/user-attachments/assets/34dc69a5-b27f-4828-b8c6-e958ce7b64ca)
   4. Dan kita akan mendapatkan hasil yaitu "ATP, EH, dan KJK"
   5. Pesannya jika digabung "pahlawan keamanan siber"
   6. Flagnya adalah "JarkomIT{S3LaM4t_p4rA_PahL4WaN_QdB1kQzmEJh3HigL0UJ7Jp070P5sgPfIpncrdKMNpjv28AKAALevxhC5}"

### 14. inneRCE

   ![image](https://github.com/user-attachments/assets/94022ccb-ca67-4f39-b3d6-9a9a3d11fe77)

   1. Memfilter shell agar dapat melihat http, sama seperti pada soal sebelumnya maka kita lihat status 200 OK, berarti penyerang berhasil mengupload file.
   2. Menggunakan filter hostname sehingga dapat menemukan nama servernya
      ![image](https://github.com/user-attachments/assets/1045aaba-4cf3-4458-add2-edaefaab8185)
   3. Pada file idzoyyshell.php kita dapat menemukan command pertama yaitu whoaimi
   4. Lakukan filter dengan idzoyy
   5. Dekode string menggunakan base64
   6. Flagnya adalah "JarkomIT{P4L1nG_g4mPaNg_An4L1sA_W3b_aTk_m91R6RAR55VMAMQ0ntmajN42VW4i4eXqe8B7Wn4NtGHm2O52xXFH8RCE}"

### 15. Baby Hengker

   ![image](https://github.com/user-attachments/assets/943d4819-67d8-4ed7-9032-e52b1b2a99a5)

   1. Gunakan filter berikut untuk melohad HID DATA 
      ![image](https://github.com/user-attachments/assets/d55da712-29e7-4049-9589-fbba642c8ea7)
   2. Ekstrak HID DATA dengan format csv dan rubah HID DATA menjadi teks dengan code cpp
      ![image](https://github.com/user-attachments/assets/c1a870f7-1b15-4250-ac09-6796e94d31c9)
   3. Ketika di run maka akan menghasilkan output strig yaitu "ini passwordnya apa ya?"
   4. Flagnya adalah "JarkomIT{4ku_p9n_j4d1_h3n9k3r_YYkqWM8r0YQoOXRIRPRLQhtw9Am1zPNMpHJBkZoJ085eEBjxpn6naHCK}"

### 16. Gajah Terbang (Server Recon)

![image](https://github.com/user-attachments/assets/be27cb19-8d78-437c-821a-39fbd160faf9)

**Server Recon Summary: Gajah Terbang**

**IP Address and Port:**
- **IP**: `10.15.42.60`
- **Port**: `61000`

**DBMS Information:**
- Setelah analisis file *pcap*, diketahui bahwa server pada IP ini menggunakan **PostgreSQL** sebagai sistem manajemen basis data (DBMS).

**Server Details:**
- Pada paket dengan panjang `560`, ditemukan bahwa server berjalan di atas sistem operasi **Debian**. Hal ini menunjukkan bahwa port `61000` digunakan oleh server DBMS.

**Operating System Confirmation:**
- Setelah pemeriksaan lebih lanjut, terkonfirmasi bahwa sistem operasi yang digunakan oleh server ini adalah **Debian**.

**Database Information:**
- Username valid untuk DBMS adalah `s1gm4`.
- Nama database yang digunakan adalah `sigmaskibidigyatrizzzz`.
- Dalam database ini terdapat empat pengguna:
  - **Kevin**
  - **Jojo**
  - **Siska**
  - **Kuntoaji**

**Admin Information:**
- Email admin terdaftar: `jojohermawan@gmail.com`
- Password yang digunakan oleh admin: `admin1234`. Password ini kemudian di-*hash* untuk mengetahui nilai aslinya.




    

    



   

   




