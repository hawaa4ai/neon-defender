# PLAN.md — Neon Defender (2D Arcade Game)

Dokumen ini adalah rencana kerja dan log perkembangan proyek game arcade 2D dalam 1 file `index.html`. Dokumen diperbarui setiap kali ada perubahan kode.

---

## 1. Ikhtisar Game

- **Judul Game**: **Neon Defender**
- **Genre**: Vertical Space Shooter / Arcade Survival
- **Format**: Single-File HTML (`index.html`) tanpa dependensi eksternal
- **Platform**: Web Browser (Desktop & Mobile Responsive)
- **Audio**: Web Audio API Sintetis (tanpa file audio eksternal)
- **Penyimpanan**: LocalStorage (`arcade_leaderboard`, `arcade_last_username`)
- **Kebijakan Caching**: Zero-Cache (`no-cache, no-store, must-revalidate`)
- **Deployment**: GitHub Pages — **LIVE** di https://hawaa4ai.github.io/neon-defender/

---

## 2. Aturan Bermain & Kontrol

### Kontrol
| Input | Aksi |
| :--- | :--- |
| `←` `→` / `A` `D` | Geser pesawat kiri/kanan |
| `↑` `↓` / `W` `S` | Geser pesawat atas/bawah |
| `Space` / `Enter` | Mulai misi dari menu |
| `P` / `Esc` | Jeda / lanjutkan |
| `M` | Nyalakan / matikan suara |
| Drag (mouse / sentuh) | Menggerakkan pesawat langsung |
| Tombol `II` | Jeda (ramah perangkat sentuh) |

Tembakan berjalan **otomatis** selama misi. Fokus pemain adalah menghindar, mengumpulkan power-up, dan bertahan.

### Aturan Utama
- Pemain memiliki **3 nyawa** (maksimal 5). Tabrakan dengan musuh atau proyektil mengurangi 1 nyawa.
- Setelah terkena, pemain mendapat kebal sementara ±2,2 detik (pesawat berkedip).
- **Level naik setiap 22 detik**; musuh menjadi lebih cepat, lebih sering, dan lebih bervariasi.
- Game over terjadi saat nyawa habis. Skor langsung diperiksa untuk masuk **Top 10**.
- Leaderboard disimpan di LocalStorage dan bertahan setelah browser ditutup.

### Skor Musuh
| Musuh | Karakteristik | Skor |
| :--- | :--- | :--- |
| Drifter | Diamond neon, bergerak turun sambil bergoyang | 10 |
| Zigzag | Segitiga amber, memantul kiri-kanan | 15 |
| Shooter | Heksagon pink, berhenti dan menembak ke arah pemain | 25 |
| Tank | Kubus ungu berlapis armor, menembak 3 arah | 60 |

### Power-Up
| Simbol | Efek |
| :--- | :--- |
| `R` | Rapid Fire — tembakan lebih cepat selama 8 detik |
| `S` | Shield — menahan 1 tabrakan selama 12 detik |
| `T` | Triple Shot — 3 peluru menyebar selama 8 detik |
| `+` | Extra Life — menambah 1 nyawa (atau +200 skor bila nyawa penuh) |

---

## 3. Fase Pengembangan Universal

### Phase 0: Brainstorming & Desain Game
- [x] Konsep game ditentukan: **Neon Defender** (space shooter survival).
- [x] Kontrol: keyboard + drag sentuh/mouse, tembakan otomatis.
- [x] Aturan kalah/menang dan sistem skor.
- [x] Gaya visual: retro neon glow + starfield + scanline.

### Phase 1: Setup Single-File `index.html`
- [x] Kerangka HTML5 dengan meta tag **Zero-Cache**.
- [x] Kanvas responsif dengan rasio tetap 480×720 (2:3), mendukung HiDPI.
- [x] Struktur kode modular 8 blok di JavaScript.
- [x] Game loop `requestAnimationFrame` dengan delta time (`dt`).

### Phase 2: Username & Leaderboard LocalStorage
- [x] Modal input username dengan validasi 1–15 karakter dan sanitasi anti-XSS.
- [x] Simpan/baca username terakhir dari `arcade_last_username`.
- [x] Penyimpanan, penyortiran, dan pemotongan Top 10 di `arcade_leaderboard`.
- [x] Tabel peringkat interaktif di menu dan layar game over (dengan highlight entri baru).

### Phase 3: Mekanik Inti Permainan (Core Gameplay)
- [x] Status game (`MENU`, `PLAYING`, `PAUSED`, `GAMEOVER`).
- [x] Pergerakan pemain (keyboard + pointer) dengan batas layar.
- [x] 4 tipe musuh, pola kemunculan, dan peningkatan level.
- [x] Deteksi tabrakan (AABB / circle-rect / circle-circle), nyawa, dan skor.
- [x] Power-up, shield, rapid fire, triple shot, dan extra life.

### Phase 4: Efek Suara & Visual Juice
- [x] Efek suara sintetis: tembak, kena, ledakan, power-up, level up, game over.
- [x] Partikel ledakan, spark, dan teks skor melayang.
- [x] Screen shake, kilatan merah saat terkena, dan banner level.
- [x] Starfield parallax, nebula, dan overlay scanline CSS.
- [x] Tombol mute dengan preferensi tersimpan (`arcade_muted`).

### Phase 5: Publikasi GitHub Pages
- [x] Inisialisasi git dan branch `main`.
- [x] Buat repository GitHub publik via `gh repo create neon-defender --public --source=. --remote=origin --push`.
- [x] Aktifkan GitHub Pages dari branch `main`, folder `/` (root).
- [x] Sediakan snippet terminal siap salin untuk alur Google AI Studio.
- [x] Pantau status build Pages (`gh api /repos/hawaa4ai/neon-defender/pages/builds/latest`).
- [x] Tes live demo dan pastikan halaman tampil (HTTP 200 + meta Zero-Cache).

**Repository**: https://github.com/hawaa4ai/neon-defender  
**Live Demo**: https://hawaa4ai.github.io/neon-defender/

---

## 4. Matriks Tugas & Status Pelaksanaan

| ID | Tugas / Fitur | Fase | Status | Pelaksana | Catatan |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **T-00** | Template `AGENTS.md` & `PLAN.md` | Fondasi | `DONE` | AI | Standar single-file siap |
| **T-01** | Konsep game **Neon Defender** | Phase 0 | `DONE` | AI | Space shooter survival neon |
| **T-02** | Skeleton `index.html`, canvas HiDPI, Zero-Cache | Phase 1 | `DONE` | AI | 8 blok modular, rasio 2:3 |
| **T-03** | Username modal & leaderboard Top 10 | Phase 2 | `DONE` | AI | Validasi, sanitasi, highlight |
| **T-04** | Pergerakan, 4 musuh, tabrakan, power-up, level | Phase 3 | `DONE` | AI | Auto-fire, nyawa, skor |
| **T-05** | Audio sintetis, partikel, shake, HUD | Phase 4 | `DONE` | AI | Web Audio + visual juice |
| **T-06** | Deployment GitHub Pages | Phase 5 | `DONE` | AI | Live: https://hawaa4ai.github.io/neon-defender/ |
| **T-07** | Uji otomatis headless Chrome | QA | `DONE` | AI | Menu, main, game over, pause, leaderboard, restart: 0 error |
| **T-08** | Publikasi repository publik `neon-defender` | Phase 5 | `DONE` | AI | https://github.com/hawaa4ai/neon-defender |

*Status: `TODO` | `IN-PROGRESS` | `DONE`*

---

## 5. Changelog & Riwayat Revisi

| Versi | Tanggal | Pelaksana | Ringkasan Perubahan | Referensi Commit |
| :--- | :--- | :--- | :--- | :--- |
| **v1.0.1** | 2026-10-31 | AI | Publikasi repo publik `neon-defender` dan aktivasi GitHub Pages; live demo terverifikasi HTTP 200 | — |
| **v1.0.0** | 2026-10-31 | AI | Rilis game **Neon Defender**: 4 tipe musuh, level dinamis, power-up, audio sintetis, partikel, screen shake, HUD, modal username, dan leaderboard Top 10. Lolos uji alur headless Chrome tanpa error. | — (lokal) |
| **v0.2.2** | 2026-10-24 | AI | Menambahkan panduan alur integrasi khusus Google AI Studio & penegasan repo wajib Public | `07475fb` |
| **v0.2.1** | 2026-10-24 | AI | Menambahkan panduan detail aktivasi GitHub Pages (CLI `gh api` & Web UI visual) serta troubleshooting | `3aaf671` |
| **v0.2.0** | 2026-10-24 | AI | Konfigurasi ulang ke Single Model AI untuk siswa, modularisasi 8 blok kode, dan penyesuaian matriks tugas | `2954bb0` |
| **v0.1.0** | 2026-10-24 | AI | Inisialisasi awal file sistem `AGENTS.md` dan universal blueprint `PLAN.md` | `47aa88e` |

---

## 6. Catatan Teknis Implementasi

- **Struktur 8 blok** di dalam `<script>`: Config & Canvas, Audio, Input, State & Entities, Collision & Physics, Leaderboard, Rendering & UI, Main Loop.
- **Canvas HiDPI**: backing store mengikuti `devicePixelRatio` (maksimal 2) agar tajam di layar retina; ukuran logis tetap 480×720.
- **Skala UI**: variabel CSS `--u` dihitung dari lebar frame (`frameWidth / 480`), sehingga seluruh teks dan tombol DOM ikut menskala bersama canvas.
- **Kunci LocalStorage**: `arcade_last_username`, `arcade_leaderboard`, `arcade_muted`.
- **Keamanan**: username disanitasi (`< > & " '` dibuang) dan selalu dirender melalui `textContent`, bukan `innerHTML`.
- **Audio**: dibuat saat interaksi pertama pengguna (klik/tombol/keydown) untuk memenuhi kebijakan autoplay browser.
- **Uji otomatis**: simulasi headless Chrome menjalankan ±950 frame gameplay, memaksa game over, membuka overlay, pause/resume, kembali ke menu, dan menyimpan skor — hasil tanpa error JavaScript.
