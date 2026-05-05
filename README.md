#  MP4 → WebM Converter (Enhanced Audio + Noise Reduction)

🌐 **Language**:
- 🇺🇸 English (current)
- 🇮🇩 Indonesia → see file [README ~ Bahasa Indonesia](README.id.md)

This project uses **FFmpeg** to:
- Convert `.mp4` → `.webm`
- Reduce file size by 78.49% without compromising video quality.
- Improve audio quality
- Remove noise using the `cb.rnnn` model

---

## 🚀 Prerequisites

- FFmpeg
- `cb.rnnn` model file

---

## 📦 FFmpeg Installation

### 🪟 Windows

1. Download FFmpeg from:
   https://www.gyan.dev/ffmpeg/builds/
   
   Download file:
   ```
   ffmpeg-git-full.7z
   ```  

2. Extract to a folder (e.g., `C:\ffmpeg`)

3. Navigate to:
   ```
   C:\ffmpeg\bin
   ```

4. Add to Environment Variables (`Path`)

5. Verify:
   ```bash
   ffmpeg -version
   ```

---

### 🍎 macOS

```bash
brew install ffmpeg
```

Verify:
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

Verify:
```bash
ffmpeg -version
```

---

## 📥 Download Noise Reduction Model

Download raw file:

https://github.com/richardpl/arnndn-models/blob/master/cb.rnnn


Save as:
```
cb.rnnn
```

---

## 📁 Folder Structure

```bash
project-folder/
├── input.mp4
├── cb.rnnn
```

---

## ⚙️ How to Use
🧩 Command Template
```bash
ffmpeg -hwaccel [Hardware-Accelerated-Processing] -i input.mp4 -af "arnndn=m=cb.rnnn" -c:v libvpx-vp9 -crf 30 -b:v 0 -threads [LOGICAL_COUNT] -c:a libopus output.webm
```

---

## 🖥️ By OS (example Logical Count = 8)

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


## 💡 Important Notes

- Replace:
   - `input.mp4` → the file to be converted
   - `output.webm` → desired output filename
   - `[LOGICAL_COUNT]` → number of logical CPUs (check Task Manager / System Monitor)

- All commands include:
  - Noise reduction (`arnndn`)
  - Optimal WebM codec (`libvpx-vp9 + libopus`)

---
