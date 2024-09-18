# Jarkom-Modul-1-IT18-2024

**KELOMPOK IT18**
| Nama | NRP |
|---------------------------|------------|
|Hazwan Adhikara Nasution | 5027231017 |
|Farand Febriansyah | 5027231084 |

<hr>

### Advance Sanity Check

<img width="649" alt="image" src="https://github.com/user-attachments/assets/de9cb709-41be-4729-ad83-79f9637c5fe9">


`Step Pengerjaan`
- frame contains “username”.
- frame containts “.txt”.
- Di Clue3.txt ada kalimat untuk membuka PPT.
- Saat melihat bagian Peraturan Soal Shift pada PPT terdapat sesuatu yang harus kita decode menggunakan base64.
- Lalu input hasil Decodenya dan Flag pun muncul.

### 22 Nightmare

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



