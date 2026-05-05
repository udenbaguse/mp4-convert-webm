#  MP4 → WebM Converter (Enhanced Audio + Noise Reduction)

🌐 **Bahasa**:
- 🇮🇩 Indonesia (saat ini)
- 🇺🇸 English → lihat file [README ~ English](README.md)

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

https://github.com/richardpl/arnndn-models/blob/master/cb.rnnn

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
🧩 Template
```bash
ffmpeg -hwaccel [Hardware-Accelerated-Processing] -i input.mp4 -af "arnndn=m=cb.rnnn" -c:v libvpx-vp9 -crf 30 -b:v 0 -threads [JUMLAH_LOGICAL] -c:a libopus output.webm
```

---

## 🖥️ Berdasarkan OS

### 🪟 Windows
```bash
ffmpeg -hwaccel d3d11va -i input.mp4 -af "arnndn=m=cb.rnnn" -c:v libvpx-vp9 -crf 30 -b:v 0 -threads 8 -c:a libopus output.webm
```

### 🐧 Linux
```bash
ffmpeg -hwaccel vaapi -vaapi_device /dev/dri/renderD128 -i input.mp4 -af "arnndn=m=cb.rnnn" -c:v libvpx-vp9 -crf 30 -b:v 0 -threads 8 -c:a libopus output.webm
```

### 🍎 macOS
```bash
ffmpeg -hwaccel videotoolbox -i input.mp4 -af "arnndn=m=cb.rnnn" -c:v libvpx-vp9 -crf 30 -b:v 0 -threads 8 -c:a libopus output.webm
```

## 💡 Catatan Penting

- Ganti:
   - `input.mp4` → nama file yang akan dikonversi
   - `output.webm` → nama file yang nantinya jadi hasil konversi
   - `[JUMLAH_LOGICAL]` → jumlah logical CPU (lihat Task Manager / System Monitor)

- Semua command sudah termasuk:
  - Noise reduction (`arnndn`)
  - Codec optimal WebM (`libvpx-vp9 + libopus`)

---
