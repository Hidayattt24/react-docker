# React Vite with Docker - Simple Tutorial

Tutorial sederhana untuk menggunakan Docker dengan aplikasi React Vite menggunakan Docker Desktop.

## 📋 Prerequisites

Sebelum memulai, pastikan Anda telah menginstall:

- [Docker Desktop](https://www.docker.com/products/docker-desktop/) untuk Windows
- Git (untuk version control)

## 🚀 Quick Start

### 1. Build Docker Image

```bash
# Build image dengan nama react-vite-app
docker build -t react-vite-app .
```

### 2. Run Container

```bash
# Jalankan container dan expose ke port 3000
docker run -p 3000:3000 react-vite-app
```

### 3. Akses Aplikasi

Buka browser dan akses: http://localhost:3000

## 📂 Struktur File Docker

```
react-vite-docker/
├── Dockerfile              # File konfigurasi Docker
├── .dockerignore           # File yang diabaikan saat build
└── README.md              # Dokumentasi ini
```

## 🔧 Penjelasan File Docker

### 1. Dockerfile

File konfigurasi untuk membuat Docker image:

- **Base Image**: Menggunakan `node:20-alpine` - image Linux yang ringan dengan Node.js 20 (required untuk Vite 7+)
- **Working Directory**: Set `/app` sebagai direktori kerja di dalam container
- **Copy Files**: Copy `package.json` dan source code ke container
- **Install Dependencies**: Menggunakan `npm ci` untuk install dependencies
- **Build**: Menjalankan `npm run build` untuk build aplikasi production
- **Serve**: Menggunakan `serve` untuk menjalankan aplikasi static
- **Expose Port**: Membuka port 3000 untuk akses dari luar container

> **Note**: Vite 7+ memerlukan Node.js versi 20.19+ atau 22.12+. Jika menggunakan Node.js 18, akan muncul error saat build.

### 2. .dockerignore

File ini mencegah file/folder yang tidak diperlukan masuk ke Docker context:

- `node_modules` - akan diinstall ulang di container
- `dist`, `build` - output build yang akan dibuat ulang
- `.env` files - environment variables
- IDE files, logs, temporary files

## 🛠️ Perintah Docker yang Berguna

### Manajemen Images

```bash
# Lihat semua images
docker images

# Hapus image
docker rmi react-vite-app

# Hapus semua unused images
docker image prune
```

### Manajemen Containers

```bash
# Lihat running containers
docker ps

# Lihat semua containers (termasuk yang sudah stop)
docker ps -a

# Stop container yang sedang berjalan
docker stop <container-id>

# Hapus container
docker rm <container-id>

# Jalankan container di background
docker run -d -p 3000:3000 --name react-app react-vite-app
```

### Debug dan Monitoring

```bash
# Lihat logs container
docker logs react-app

# Akses container untuk debugging
docker exec -it react-app sh

# Check status container
docker inspect react-app
```

## 🔍 Troubleshooting

### 1. Port sudah digunakan

```bash
# Windows: Cek port yang digunakan
netstat -ano | findstr :3000

# Kill process di port tertentu
taskkill /PID <PID> /F
```

### 2. Build gagal karena Node.js version

Jika muncul error seperti:

```
You are using Node.js 18.x.x. Vite requires Node.js version 20.19+ or 22.12+
```

**Solusi**: Pastikan Dockerfile menggunakan `node:20-alpine` atau `node:22-alpine`

### 3. Build gagal karena dependency

```bash
# Clear Docker cache
docker builder prune

# Build dengan no-cache
docker build --no-cache -t react-vite-app .
```

### 4. Container tidak bisa diakses

```bash
# Check container logs
docker logs react-app

# Check container status
docker inspect react-app
```

## 📚 Best Practices

### 1. Optimasi Image Size

- Menggunakan Alpine Linux base images
- Proper `.dockerignore` file untuk menghindari file yang tidak perlu

### 2. Security

- Regular update base images
- Tidak include file sensitive di image

## 🚀 Langkah-langkah Lengkap

### 1. Pastikan Docker Desktop Running

Buka Docker Desktop dan pastikan status running (ikon Docker di system tray berwarna hijau)

### 2. Buka Terminal/Command Prompt

```bash
# Masuk ke direktori project
cd react-vite-docker
```

### 3. Build Docker Image

```bash
# Build image (proses ini akan download dependencies dan build aplikasi)
docker build -t react-vite-app .
```

### 4. Run Container

```bash
# Jalankan container
docker run -p 3000:3000 react-vite-app

# Atau jalankan di background
docker run -d -p 3000:3000 --name my-react-app react-vite-app
```

### 5. Test Aplikasi

Buka browser dan akses: http://localhost:3000

## 📖 Referensi

- [Docker Desktop](https://www.docker.com/products/docker-desktop/)
- [Docker Documentation](https://docs.docker.com/)
- [Vite Documentation](https://vitejs.dev/)

---

**Happy Dockerizing! 🐳**

#
