# NEON FRONTIER — Drone Training FPS

Game FPS 3D arcade bergaya sci-fi yang dibuat dengan Three.js + Vite, lalu dibungkus menjadi aplikasi Android menggunakan Capacitor. Proyek ini ditujukan untuk latihan target drone fiktif, bukan simulasi senjata atau situasi nyata.

## Fitur

- Arena 3D low-poly bertema neon.
- Drone latihan 3D yang dibuat dari geometri Three.js.
- Pulse-caster fiktif dengan efek tembakan energi.
- Efek suara sintetis melalui Web Audio API.
- Joystick layar sentuh, geser layar untuk melihat/membidik, tombol lompat, dan tombol pulse.
- Kontrol keyboard untuk pengujian di PC: WASD/arrow, Space untuk lompat, Enter untuk menembak.
- Sesi latihan 90 detik, skor, jeda, dan main ulang.
- Game dapat berjalan offline setelah aset web termuat di APK.
- GitHub Actions menghasilkan APK debug secara otomatis.

## Struktur folder

```text
neon-frontier-fps/
├── .github/
│   └── workflows/
│       └── android-apk.yml      # Workflow build APK GitHub Actions
├── public/
│   └── assets/
│       ├── app-icon.svg         # Ikon aplikasi
│       ├── arena-grid.svg       # Referensi tekstur arena
│       └── drone-symbol.svg     # Simbol drone
├── scripts/
│   └── patch-android.mjs        # Mengatur orientasi Android ke landscape
├── src/
│   ├── game/
│   │   ├── assets.js            # Pembuatan arena, drone, dan pulse-caster 3D
│   │   ├── audio.js             # Efek suara sintetis
│   │   └── Game.js              # Scene, kamera FPS, gerak, tembakan, skor
│   ├── ui/
│   │   └── controls.js          # Joystick, look gesture, tombol dan keyboard
│   ├── main.js                 # Menghubungkan game dengan antarmuka
│   └── styles.css              # HUD dan layout layar
├── capacitor.config.json       # Identitas aplikasi Android
├── index.html                  # Halaman utama game
├── package.json                # Dependensi dan perintah build
└── vite.config.js               # Konfigurasi bundler web
```

Model 3D utama dibuat secara prosedural di `src/game/assets.js`, jadi tidak perlu mengunduh model eksternal. File SVG di `public/assets/` adalah aset visual tambahan. Ini membuat proyek lebih ringan dan semua aset yang diperlukan ikut di dalam repositori.

## Membuat APK melalui GitHub dari HP

1. Ekstrak ZIP proyek ini di HP.
2. Buat repository baru di GitHub, misalnya `neon-frontier-fps`.
3. Unggah **isi folder proyek** ke repository, bukan hanya file ZIP. Pastikan folder `.github/workflows/` ikut terunggah dan nama workflow tetap `android-apk.yml`.
4. Buka tab **Actions** di repository. Pilih workflow **Build Neon Frontier APK**.
5. Tekan **Run workflow** bila workflow belum berjalan otomatis. Tunggu sampai job berstatus hijau.
6. Buka hasil run yang sukses, gulir ke bagian **Artifacts**, lalu unduh `neon-frontier-debug-apk`.
7. Ekstrak ZIP artifact tersebut. File yang dipasang adalah `app-debug.apk`.

Setiap kali kamu melakukan push ke branch `main` atau `master`, workflow juga berjalan otomatis.

## Menjalankan untuk uji web (opsional)

Butuh Node.js 20 atau lebih baru.

```bash
npm install
npm run dev
```

Untuk membuat bundel web:

```bash
npm run build
```

## Identitas APK

- Nama aplikasi: `Neon Frontier`
- Package ID: `com.neonfrontier.dronetraining`
- Orientasi: Landscape
- Jenis output: Debug APK (untuk uji coba)

## Catatan build

- APK debug bukan rilis Play Store. Untuk distribusi publik diperlukan proses signing release dan pengujian tambahan.
- Workflow membuat folder `android/` saat berjalan, jadi folder itu tidak perlu diunggah ke GitHub.
- Jika workflow gagal, buka run yang merah, pilih langkah pertama yang gagal, lalu salin log error lengkapnya.
- Font dari Google Fonts hanya dekorasi. Jika perangkat offline, game tetap dapat dimainkan dengan font pengganti sistem.
