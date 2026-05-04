#  MP4 → WebM Converter (Enhanced Audio + Noise Reduction)

🌐 **Bahasa**:
- 🇮🇩 Indonesia (saat ini)
- 🇺🇸 English → lihat file [README ~ English](README.en.md)

Project ini menggunakan **FFmpeg** untuk:
- Konversi `.mp4` → `.webm`
- Penyusutan ukuran file 78,49% tanpa penurunan kualitas video.
- Meningkatkan kualitas audio
- Menghilangkan noise dengan model `cb.rnnn`

---

## 🚀 Prasyarat

- FFmpeg
- File model `cb.rnnn`

---

## 📦 Instalasi FFmpeg

### 🪟 Windows

1. Download FFmpeg dari:
   https://www.gyan.dev/ffmpeg/builds/
   
   Download file:
   ```
   ffmpeg-git-full.7z
   ```  

2. Extract ke folder (contoh: `C:\ffmpeg`)

3. Masuk ke:
   ```
   C:\ffmpeg\bin
   ```

4. Tambahkan ke Environment Variables (`Path`)

5. Verifikasi:
   ```bash
   ffmpeg -version
   ```

---

### 🍎 macOS

```bash
brew install ffmpeg
```

Verifikasi:
```bash
ffmpeg -version
```

---

### 🐧 Linux

#### Ubuntu / Debian
```bash
sudo apt update
sudo apt install ffmpeg
```

#### Arch
```bash
sudo pacman -S ffmpeg
```

#### Fedora
```bash
sudo dnf install ffmpeg
```

Verifikasi:
```bash
ffmpeg -version
```

---

## 📥 Download Model Noise Reduction

Download file RAW:

https://github.com/richardpl/arnndn-models/raw/master/cb.rnnn


Simpan sebagai:
```
cb.rnnn
```

---

## 📁 Struktur Folder

```bash
project-folder/
├── input.mp4
├── cb.rnnn
```

---

## ⚙️ Cara Penggunaan
Template command:
```bash
ffmpeg [Hardware Accelerated Processing] -i input.mp4 -af "arnndn=m=cb.rnnn" -c:v libvpx-vp9 -crf 30 -b:v 0 -threads [JUMLAH_LOGICAL] -c:a libopus output.webm
```
---

### 1. Intel CPU (i3/i5/i7/i9)

#### Intel Core i3 (2 Core, 4 Logical)
```bash
ffmpeg -hwaccel qsv -i input.mp4 -af "arnndn=m=cb.rnnn" -c:v libvpx-vp9 -crf 30 -b:v 0 -threads 4 -c:a libopus output.webm
```

#### Intel Core i5/i7 (4 Core, 8 Logical)
```bash
ffmpeg -hwaccel qsv -i input.mp4 -af "arnndn=m=cb.rnnn" -c:v libvpx-vp9 -crf 30 -b:v 0 -threads 8 -c:a libopus output.webm
```

#### Intel Core i9 (6 Core, 12 Logical)
```bash
ffmpeg -hwaccel qsv -i input.mp4 -af "arnndn=m=cb.rnnn" -c:v libvpx-vp9 -crf 30 -b:v 0 -threads 12 -c:a libopus output.webm
```

---

### 2. AMD CPU (Ryzen) + GPU (VAAPI)

#### Ryzen 3 (2 Core, 4 Logical)
```bash
ffmpeg -hwaccel vaapi -vaapi_device /dev/dri/renderD128 -i input.mp4 -af "arnndn=m=cb.rnnn" -c:v libvpx-vp9 -crf 30 -b:v 0 -threads 4 -c:a libopus output.webm
```

#### Ryzen 5/7 (4 Core, 8 Logical)
```bash
ffmpeg -hwaccel vaapi -vaapi_device /dev/dri/renderD128 -i input.mp4 -af "arnndn=m=cb.rnnn" -c:v libvpx-vp9 -crf 30 -b:v 0 -threads 8 -c:a libopus output.webm
```

#### Ryzen 9 (8 Core, 16 Logical)
```bash
ffmpeg -hwaccel vaapi -vaapi_device /dev/dri/renderD128 -i input.mp4 -af "arnndn=m=cb.rnnn" -c:v libvpx-vp9 -crf 30 -b:v 0 -threads 16 -c:a libopus output.webm
```

---

### 3. NVIDIA GPU (Semua CPU)
```bash
ffmpeg -hwaccel cuda -i input.mp4 -af "arnndn=m=cb.rnnn" -c:v libvpx-vp9 -crf 30 -b:v 0 -threads 8 -c:a libopus output.webm
```

---

## 💡 Catatan Penting

- Ganti:
   - `input.mp4` → nama file yang akan dikonversi
   - `output.webm` → nama file yang nantinya jadi hasil konversi
   - `[JUMLAH_LOGICAL]` → jumlah logical CPU (lihat Task Manager / System Monitor)

- Semua command sudah termasuk:
  - Noise reduction (`arnndn`)
  - Codec optimal WebM (`libvpx-vp9 + libopus`)

---