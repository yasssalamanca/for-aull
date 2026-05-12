# IMPLEMENTATION GUIDE: "For My Girl" Web App

Dokumen ini berisi panduan arsitektur dan desain untuk membangun sebuah website apresiasi/penyemangat yang ditujukan untuk pacar User. Website ini harus terasa sangat personal, manis, elegan, dan membuat siapa saja yang melihatnya tersenyum.

---

## 1. Tech Stack (Rekomendasi Terbaik & Teringan)
Karena ini adalah website yang berfokus pada konten visual, interaksi, dan animasi (tanpa backend kompleks), stack yang paling cocok dan mudah dieksekusi adalah pendekatan **Vanilla + CDN**:
- **HTML5**: Sebagai struktur utama.
- **Tailwind CSS (via CDN)**: Untuk styling yang sangat cepat, konsisten, dan mudah dibuat responsif tanpa perlu menulis banyak custom CSS.
- **Vanilla JavaScript**: Untuk menangani event klik, interaksi dasar, dan memutar audio (jika ada).
- **AOS (Animate On Scroll) atau GSAP via CDN**: Untuk membuat elemen muncul dengan animasi yang mulus ketika di-scroll.
- **Canvas Confetti (via CDN)**: Sebagai tambahan interaksi kejutan ketika tombol tertentu ditekan.

## 2. Design System & Tema Visual
Fokus utama adalah kenyamanan mata, estetika modern, dan kesan manis.

- **Palet Warna**:
  - **Background**: Putih bersih (`#ffffff`) atau *Off-white* dengan hint pink sangat tipis (`#fffafb`).
  - **Primary (Aksen & Tombol)**: Soft Pink (`#ffb6c1` atau `#f9a8d4`) dan Rose Pink (`#fb7185`).
  - **Secondary (Kartu/Elemen Timbul)**: Putih dengan bayangan/shadow pink lembut (`box-shadow: 0 4px 14px 0 rgba(251, 113, 133, 0.2);`).
  - **Text**: Abu-abu kehitaman (`#334155` atau `#475569`) untuk keterbacaan tinggi. Jangan gunakan hitam murni (`#000000`).
  - **Tambahan**: Merah muda pastel untuk gradient.
- **Tipografi (Google Fonts)**:
  - **Heading/Title**: `Outfit`, `Poppins`, atau `Quicksand` (Memberikan kesan modern, membulat, dan bersahabat).
  - **Body/Text Paragraph**: `Inter` atau `Nunito`.

## 3. Struktur Layout & UI/UX (SANGAT PENTING: Mobile-First)
Karena target utama melihat website ini melalui **Handphone**, desain HARUS `mobile-first`.
1. **Hero Section (Bagian Paling Atas)**:
   - Teks sapaan manis yang besar.
   - Efek *typing text* atau *fade-in* lambat agar dramatis.
   - Gambar kecil/Avatar lucu di tengah.
2. **Message Cards Section**:
   - Kumpulan "Card" (kotak dengan sudut melengkung `rounded-2xl`).
   - Setiap card berisi:
     - Teks penyemangat.
     - Gambar atau GIF lucu (misal: GIF kucing berpelukan, Bubu Dudu, dll).
   - Layout card pada mobile disusun berderet ke bawah (stack vertikal), dengan *gap* yang cukup lega.
3. **Interactive Section**:
   - Tombol berukuran besar (mudah ditekan jempol) dengan tulisan seperti "Pencet Aku!".
   - Saat ditekan, layar akan dipenuhi animasi konfeti dan memunculkan teks/pesan rahasia.

## 4. Panduan Animasi & Interaksi
- **Soft Transitions**: Semua tombol harus memiliki efek transisi saat disentuh/di-hover (misal: `hover:scale-105 active:scale-95 transition-all duration-300`).
- **Scroll Animations**: Gunakan library animasi agar setiap Card muncul dari bawah atau perlahan memudar (fade-up) saat di-scroll.
- **Floating Elements**: Tambahkan beberapa ikon hati (❤️ atau 🌸) yang melayang-layang perlahan di background menggunakan animasi CSS (keyframes).

---

## 6. Fitur Utama: "Menyemangati Hari-Harinya" 🌸

Ini adalah jantung dari aplikasi. Tujuannya bukan hanya sekali dilihat, tapi bisa dia buka setiap hari dan selalu menemukan sesuatu yang hangat. Implementasikan semua fitur berikut:

### 6.1 — Daily Encouraging Quote 💬
- Buat sebuah array JavaScript berisi **minimal 15 pesan penyemangat** yang personal dan lembut.
  - Contoh isi: *"Hei kamu, hari ini mungkin berat, tapi kamu sudah sejauh ini. Aku bangga banget sama kamu."*, *"Apapun yang kamu rasain hari ini, aku di sini. Selalu."*, *"Kamu lebih kuat dari yang kamu pikir, dan lebih cantik dari yang kamu bayangkan."*
- Setiap kali halaman dibuka, tampilkan **satu quote acak** (bisa `Math.floor(Math.random() * quotes.length)`).
- Tampilkan di bagian **paling atas (Hero Section)** dalam kotak card semi-transparan dengan efek *frosted glass* (`backdrop-blur`).
- Tambahkan tombol kecil **"🔁 Quote Baru"** yang mengganti quote dengan animasi fade-out → fade-in saat ditekan.
- Optional: simpan quote hari ini di `localStorage` agar quote tidak berubah dalam satu hari yang sama (baru ganti besok).

### 6.2 — "Hari Ini Gimana?" Mood Tracker 🎭
- Tampilkan sebuah card sederhana dengan teks: **"Hei, hari ini kamu gimana?"**
- Sediakan **4-5 tombol emoji** sebagai pilihan suasana hati:
  - 😊 Baik banget  |  😌 Lumayan  |  😔 Agak sedih  |  😩 Capek  |  🥰 Kangen kamu
- Ketika dia menekan salah satu:
  - Munculkan **respons personal yang sesuai** (bukan teks generik). Contoh:
    - Kalau pilih 😔: *"Ih, boleh sedih, tapi jangan lama-lama ya. Sini aku peluk (virtual) 🫂"*
    - Kalau pilih 🥰: *"Hahaha aku juga kangeeen. Btw, kamu udah makan belum?"*
  - Tampilkan GIF/stiker yang relevan (kucing memeluk, dll.) di bawah respons.
  - Animasikan munculnya respons dengan efek *slide-up* + *fade-in*.

### 6.3 — Countdown "Waktu Kita" ⏳
- Tambahkan sebuah section kecil yang menampilkan **hitungan mundur atau hitungan naik** menuju/dari tanggal spesial.
- Contoh tampilan:
  > *"Sudah* **X hari X jam X menit** *kita jalan bareng 🥹"* (Hitung dari tanggal anniversary/PDKT)
  > — atau —
  > *"Tinggal* **X hari** *lagi sebelum kita ketemu 🎉"* (Hitung mundur ke tanggal ketemuan)
- Gunakan `setInterval` JavaScript yang memperbarui tampilan setiap detik.
- **PENTING**: Beri komentar `<!-- GANTI TANGGAL DI SINI -->` di dekat variabel tanggal di JavaScript, agar User mudah menggantinya.
- Desain counter dengan angka besar, font *Quicksand*, warna aksen pink, dan kartu dengan shadow lembut.

### 6.4 — Mini "Surat Hari Ini" 💌
- Buat sebuah "amplop" yang bisa diklik/ditekan.
- Saat diklik, amplop akan membuka dengan animasi CSS (animasi buka tutup menggunakan `transform: rotateX`).
- Setelah terbuka, tampilkan **pesan pendek yang intim dan hangat** — ditulis seolah-olah dari sang pacar.
  - Contoh: *"Hari ini aku cuma mau ngingetin satu hal: kamu tuh berharga banget. Bukan cuma buat aku, tapi buat semua orang di sekitar kamu. Jangan lupa minum air ya 💧"*
- Isi surat bisa dirotasi setiap hari (simpan index di `localStorage`) atau dipilih secara acak.
- Tambahkan **tombol "Balas dengan ❤️"** yang memunculkan konfeti dan teks *"Makasih udah baca! 🥹"*.

### 6.5 — Pemutar "Lagu Spesial" 🎵 *(Opsional tapi Sangat Direkomendasikan)*
- Tambahkan sebuah card minimalis berupa **audio player kustom** (bukan player default browser).
- Gunakan HTML `<audio>` element yang disembunyikan, lalu kontrol dengan tombol JavaScript kustom.
- Desain player:
  - Ikon not musik 🎵 yang beranimasi (berputar atau berdenyut) saat lagu diputar.
  - Tombol Play/Pause berbentuk bulat besar dengan warna aksen pink.
  - Nama lagu dan nama "artis" (bisa diisi nama User & pasangannya, contoh: *"Our Song — By Us 🎶"*).
- **PENTING**: Beri komentar `<!-- GANTI URL AUDIO DI SINI -->` pada atribut `src` tag audio.

---

## 5. Instruksi Langkah-demi-Langkah untuk AI Agent
Kepada AI Agent yang membaca panduan ini, tugasmu adalah menghasilkan KODE LENGKAP (HTML/CSS/JS) dalam satu file `index.html` berdasarkan spesifikasi di atas. 

Ikuti langkah-langkah berikut:

1. **Setup File**: Buat satu file `index.html` dengan boilerplate HTML5 standar.

2. **Inject Dependencies (CDN)**:
   - Tailwind CSS CDN: `<script src="https://cdn.tailwindcss.com"></script>`
   - Konfigurasikan *theme colors* Tailwind (pink palette) di dalam tag `<script>`.
   - Google Fonts: `Quicksand` (heading) dan `Nunito` (body).
   - AOS Animation CSS & JS.
   - Canvas Confetti CDN.

3. **Bangun Struktur DOM** dengan urutan section berikut:
   ```
   <body>
     <!-- 1. Hero: Daily Quote + Sapaan -->
     <!-- 2. Mood Tracker: "Hari ini gimana?" -->
     <!-- 3. Countdown: Waktu Kita -->
     <!-- 4. Message Cards: Pesan Penyemangat -->
     <!-- 5. Surat Hari Ini: Amplop Interaktif -->
     <!-- 6. Audio Player: Lagu Spesial -->
     <!-- 7. Big Confetti Button -->
   </body>
   ```
   - Gunakan styling Tailwind yang rapi: `flex`, `grid`, `gap`, `p-`, `rounded-2xl`, `shadow-`, `backdrop-blur`.
   - Gunakan GIF dari Tenor/Giphy untuk mood tracker. Beri komentar `<!-- GANTI GIF DI SINI -->`.

4. **Implementasikan Logika (JavaScript)** — semua dalam satu `<script>` di bawah `</body>`:
   - `AOS.init()` untuk scroll animations.
   - **Daily Quote Engine**: Array quotes + fungsi `getQuote()` yang mengambil quote dengan `localStorage` (agar sama dalam satu hari). Tombol 🔁 memanggil `shuffleQuote()` dengan animasi fade.
   - **Mood Tracker**: Objek mapping emoji → `{ teks: '...', gif: 'url...' }`. Fungsi `showMoodResponse(mood)` menampilkan respons dengan animasi slide-up.
   - **Countdown Timer**: Variabel `targetDate` dengan komentar `<!-- GANTI TANGGAL -->`. `setInterval` setiap 1000ms untuk update DOM.
   - **Amplop Surat**: Toggle class CSS untuk animasi buka/tutup amplop. Rotasi surat dari array via `localStorage`.
   - **Audio Player Kustom**: Kontrol `play()`, `pause()` via tombol custom. Animasi ikon 🎵 saat playing.
   - **Confetti Button**: `confetti({ particleCount: 150, spread: 90, colors: ['#ffb6c1', '#fb7185', '#fde68a'] })`.

5. **Quality Control**:
   - Layout tidak rusak di layar `< 390px` (mobile kecil).
   - Warna harmonis, kontras teks nyaman (bukan hitam murni).
   - Semua animasi berjalan mulus, tidak ada layout shift.
   - Semua teks yang bersifat personal diberi komentar `<!-- BISA DIGANTI -->` agar User mudah menyesuaikan.

Lakukan yang terbaik. Hasil akhir harus benar-benar manis, estetik, dan terasa seperti pelukan digital — sesuatu yang ingin dia buka ulang setiap hari! 💕
