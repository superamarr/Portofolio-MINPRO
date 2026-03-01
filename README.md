# 🚀 Taufik Ramadhani — Personal Portfolio

Ini adalah website portofolio interaktif dan modern yang saya kembangkan untuk merepresentasikan diri saya sebagai Fullstack Developer, Data Analyst, dan AI Enthusiast. Website ini dirancang dengan antarmuka yang dinamis, dilengkapi dengan animasi background 3D, serta data yang dimuat secara reaktif menggunakan framework frontend.

---

## 🛠️ Teknologi yang Digunakan

| Teknologi | Peran dalam Proyek |
|---|---|
| **HTML5** | Struktur semantik seluruh halaman |
| **CSS3 (Vanilla)** | Styling kustom, animasi, layout utama (`style.css`) |
| **Bootstrap 5** | Grid responsif, sistem kolom, dan utilitas spacing |
| **Vue.js 3** | Reactive data binding untuk Skills dan Certificates |
| **Three.js / TubesCursor** | Animasi latar belakang 3D interaktif berbasis WebGL |
| **Google Fonts** | Font `Barlow Condensed` untuk tipografi |

---

## 📁 Struktur File

```
porto/
├── index.html       # Struktur utama halaman
├── main.js          # Logika JavaScript & inisialisasi Vue / TubesCursor
├── style.css        # Seluruh styling dan animasi kustom
└── assets/
    └── images/      # Foto profil dan gambar sertifikat
```

---

## 📑 Dokumentasi Fitur & Section

---

### 1. 🎨 Hero Section & Interactive Background 3D

Bagian pembuka website yang langsung menyambut pengunjung dengan efek visual dramatis berbasis 3D.

| 📸 Tampilan (Screenshot) |
| :---: |
| <img width="1352" height="678" alt="image" src="https://github.com/user-attachments/assets/00c6e5fa-0f1c-4ffe-8d24-b5530ad43d8d" /> |

**Kode:**

```html
<!-- index.html -->
<canvas id="canvas"></canvas>

<div class="hero">
  <h1><span class="outline">HEY, I'M</span> TAUFIK RAMADHANI</h1>
  <h2><span class="outline">BUT YOU CAN CALL ME</span> TAUFIK</h2>
  <p>I'm a fullstack developer, data analyst,<br>& ai enthusiast</p>
  <div class="links">
    <a href="#about">→ more about me</a>
  </div>
</div>
```

```javascript
// main.js — Inisialisasi TubesCursor & warna acak on-click
import TubesCursor from "https://cdn.jsdelivr.net/npm/threejs-components@0.0.19/build/cursors/tubes1.min.js"

let app
document.addEventListener('DOMContentLoaded', () => {
  const canvas = document.getElementById('canvas')
  app = TubesCursor(canvas, {
    tubes: {
      colors: ["#f967fb", "#e3f306", "#6958d5"],
      lights: {
        intensity: 200,
        colors: ["#83f36e", "#fe8a2e", "#ff008a", "#60aed5"]
      }
    }
  })
})

document.body.addEventListener('click', () => {
  const colors = randomColors(3)
  const lightsColors = randomColors(3)
  app.tubes.setColors(colors)
  app.tubes.setLightsColors(lightsColors)
})

function randomColors(count) {
  return new Array(count).fill(0)
    .map(() => "#" + Math.floor(Math.random() * 16777215).toString(16).padStart(6, '0'))
}
```

```css
/* style.css — Hero Layout */
.hero {
  position: relative;
  height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  z-index: 10;
}

h1 span.outline, h2 span.outline {
  color: transparent;
  -webkit-text-stroke: 2.5px white;
}

#canvas {
  position: fixed;
  inset: 0;
  z-index: 0;
  pointer-events: none;
}
```

**Penjelasan Kode:** Section Hero merupakan bagian pembuka website yang menampilkan nama lengkap dan tagline profesi. Elemen `<canvas id="canvas">` diposisikan secara `fixed` di seluruh layar menggunakan CSS (`inset: 0`) dan berfungsi sebagai lapisan latar belakang animasi 3D. Library `TubesCursor` dari ekosistem Three.js diinisialisasi dengan nilai konfigurasi warna awal untuk tabung (`tubes.colors`) dan sumber cahaya (`lights.colors`). Setiap kali pengguna mengklik area mana pun di halaman, event listener `document.body` memangil fungsi `randomColors()` — yang menghasilkan warna HEX acak — lalu menerapkannya ke kanvas melalui `app.tubes.setColors()`. Teks hero menggunakan efek `outline` via properti CSS `-webkit-text-stroke` sehingga karakter tampak transparan dengan garis tepi putih, menciptakan kontras visual yang dramatis.

---

### 2. 🧭 Top Navigation (Navbar) & Scroll Indicator

Navigasi *floating* bergaya *glassmorphism* yang tersembunyi di awal, serta indikator animasi panah gulir di bawah layar.

| 📸 Tampilan (Screenshot) |
| :---: |
| <img width="246" height="93" alt="image" src="https://github.com/user-attachments/assets/d00e74aa-71d3-415c-9c35-fae7ad5491a8" /> <img width="346" height="57" alt="image" src="https://github.com/user-attachments/assets/43933dbf-eccb-4113-ba4f-2e08256bfaa6" /> |

**Kode:**

```html
<!-- index.html -->
<header class="topnav" id="topnav">
  <nav>
    <ul>
      <li><a href="#">Home</a></li>
      <li><a href="#about">About</a></li>
      <li><a href="#experience">Experience</a></li>
      <li><a href="#certificates">Certificates</a></li>
    </ul>
  </nav>
</header>

<div class="scroll-indicator">
  <span></span>
  <span></span>
  <span></span>
</div>
```

```javascript
// main.js — Logika show/hide navbar & scroll indicator
window.addEventListener('scroll', () => {
  const scrolled = window.scrollY > 10
  topnav.classList.toggle('show', scrolled)
  indicator.classList.toggle('hide', scrolled)
})
```

```css
/* style.css — Glassmorphism Navbar */
.topnav {
  position: fixed;
  top: 16px;
  left: 50%;
  background: rgba(10, 10, 20, 0.45);
  border: 1px solid rgba(255, 255, 255, 0.12);
  backdrop-filter: blur(10px);
  border-radius: 14px;
  transform: translate(-50%, -140%); /* tersembunyi di atas layar */
  transition: transform 0.35s ease;
}
.topnav.show {
  transform: translate(-50%, 0); /* muncul saat scroll */
}

/* Scroll Indicator — Animasi panah bouncing */
.scroll-indicator span {
  width: 16px; height: 16px;
  border-right: 2.5px solid rgba(255,255,255,0.8);
  border-bottom: 2.5px solid rgba(255,255,255,0.8);
  transform: rotate(45deg);
  animation: scrollBounce 1.5s ease infinite;
}
.scroll-indicator.hide { opacity: 0; }
```

**Penjelasan Kode:** Navbar diposisikan secara `fixed` di tengah atas layar menggunakan `left: 50%` dan `transform: translate(-50%, -140%)` — nilai `-140%` menyembunyikannya di luar batas atas layar saat pertama kali halaman dimuat. Ketika pengguna mulai menggulir halaman lebih dari 10px, event scroll di `main.js` menambahkan kelas `.show` yang mengubah `transform` kembali ke `translate(-50%, 0)`, sehingga navbar meluncur turun secara smooth berkat `transition`. Bersamaan dengan itu, kelas `.hide` diberikan ke `.scroll-indicator` yang menyebabkan elemen memudar (`opacity: 0`). Tiga elemen `<span>` dalam scroll indicator masing-masing berbentuk panah segitiga dari border CSS dengan animasi `@keyframes scrollBounce` yang diberi `animation-delay` bertahap (0s, 0.2s, 0.4s) untuk menciptakan efek beriak.

---

### 3. 👤 About & Skills Section

Bagian pengenalan diri yang memuat foto profil dengan efek *glassmorphism card* dan progress bar skill yang dirender secara reaktif oleh Vue.js.

| 📸 Tampilan (Screenshot) |
| :---: |
| <img width="1353" height="675" alt="image" src="https://github.com/user-attachments/assets/31da8c9e-37ea-46e3-b274-ed4a3b911846" /> |

**Kode:**

```html
<!-- index.html — Struktur About dengan Vue Directives -->
<div class="about" id="about">
  <div class="container">
    <div class="row align-items-center">

      <!-- Kolom Foto -->
      <div class="col-md-6">
        <div class="about-image">
          <div class="photo-card"></div>
          <img class="profile-photo" src="assets/images/Taufik Ramadhani.png" alt="Taufik Ramadhani">
        </div>
      </div>

      <!-- Kolom Teks & Skill Bar -->
      <div class="col-md-6">
        <div class="about-content">
          <h2 class="section-title">ABOUT</h2>
          <hr>
          <p>Hey, my name is Taufik Ramadhani...</p>
          <div class="about-skills">
            <div class="row g-3">
              <!-- v-for merender setiap skill dari data Vue -->
              <div class="col-12 col-md-6" v-for="skill in skills" :key="skill.name">
                <div class="skill-header">
                  <span class="skill-label">{{ skill.name }}</span>
                  <span class="skill-value">{{ skill.percent }}%</span>
                </div>
                <div class="progress">
                  <div class="progress-bar" :style="{ width: skill.percent + '%' }"></div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>

    </div>
  </div>
</div>
```

```javascript
// main.js — Data skills Vue.js
const vueApp = window.Vue.createApp({
  data() {
    return {
      skills: [
        { name: 'JavaScript', percent: 85 },
        { name: 'React.js',   percent: 80 },
        { name: 'Laravel',    percent: 75 },
        { name: 'Next.js',    percent: 78 },
        { name: 'Golang',     percent: 60 },
        { name: 'Flutter',    percent: 65 },
      ],
    }
  },
})
vueApp.mount('#app')
```

```css
/* style.css — Photo Card Glassmorphism & Progress Bar */
.about-image .photo-card {
  width: 75%; max-width: 300px; height: 400px;
  background: rgba(255, 251, 251, 0.05);
  border-radius: 16px;
  backdrop-filter: blur(11.5px);
  border: 1px solid rgba(255, 251, 251, 0.02);
}
.profile-photo {
  position: absolute;
  left: 0; top: 0;
  z-index: 1;
  margin-top: -105px; /* foto melayang di atas card */
}
.about-skills .progress-bar {
  background: white;
  height: 100%;
}
```

**Penjelasan Kode:** Layout About menggunakan Bootstrap Grid (`col-md-6`) untuk membagi tampilan menjadi dua kolom — foto di kiri dan teks di kanan — yang otomatis menumpuk secara vertikal di layar kecil. Efek foto melayang dihasilkan dengan menumpuk dua elemen: `div.photo-card` (kotak kaca transparan berbasis *glassmorphism*) dan `img.profile-photo` yang diposisikan `absolute` dengan `margin-top: -105px` agar foto tampak keluar melampaui batas atas card. Daftar skill bar dirender menggunakan Vue.js directive `v-for="skill in skills"` yang mengiterasi array objek `skills` dari `data()`. Lebar setiap progress bar ditentukan secara reaktif oleh Vue melalui binding inline `:style="{ width: skill.percent + '%' }"` — sehingga untuk menambah atau mengubah skill, cukup ubah data di `main.js` tanpa menyentuh HTML.

---

### 4. 💼 Experience Section

Daftar riwayat pengalaman profesional dan akademis berbentuk *list* yang ditulis statis.

| 📸 Tampilan (Screenshot) |
| :---: |
| <img width="1351" height="681" alt="image" src="https://github.com/user-attachments/assets/a36a4a08-be80-46b1-9eb0-2f50ff4e39d2" /> |

**Kode:**

```html
<!-- index.html — Struktur Experience List -->
<div class="experience" id="experience">
  <div class="experience-content">
    <h2 class="section-title">EXPERIENCE</h2>
    <hr>
    <ul class="exp-list">
      <li>
        <div class="exp-head">
          <span class="exp-role">Full Stack Developer</span>
          <span class="exp-time">Feb 2026 — Saat ini</span>
        </div>
        <div class="exp-org">Coding Camp powered by DBS Foundation · Magang · Samarinda</div>
        <p class="exp-desc">React.js, Node.js, dan teknologi terkait.</p>
      </li>
      <!-- item lain mengikuti pola yang sama -->
    </ul>
  </div>
</div>
```

```css
/* style.css — Layout Experience List */
.exp-list {
  list-style: none;
  padding: 0;
  display: grid;
  gap: 8px;
}
.exp-list li {
  padding: 8px 0;
  border-bottom: 1px solid rgba(255, 255, 255, 0.15);
}
.exp-head {
  display: flex;
  justify-content: space-between; /* jabatan kiri, tanggal kanan */
  align-items: baseline;
  font-weight: 600;
}
```

**Penjelasan Kode:** Section Experience menggunakan daftar `<ul class="exp-list">` berbasis HTML murni tanpa keterlibatan Vue.js karena datanya bersifat statis dan jarang berubah. Setiap item `<li>` terdiri dari tiga lapisan informasi: baris atas (`exp-head`) menampilkan nama jabatan dan rentang waktu dengan `display: flex; justify-content: space-between` sehingga keduanya otomatis berada di ujung kiri dan kanan. Baris tengah (`exp-org`) memuat nama institusi dalam warna yang lebih redup (`rgba(255,255,255,0.8)`), dan baris bawah (`exp-desc`) adalah deskripsi singkat tugas. Setiap item dipisahkan oleh garis bawah transparan `border-bottom: 1px solid rgba(255,255,255,0.15)` yang memberikan pemisah halus tanpa mengganggu nuansa gelap keseluruhan desain.

---

### 5. 🏆 Certificates Section

Galeri sertifikat berbentuk kartu responsif yang dirender secara dinamis oleh Vue.js.

| 📸 Tampilan (Screenshot) |
| :---: |
| <img width="1352" height="681" alt="image" src="https://github.com/user-attachments/assets/535c81c4-9713-4250-b4e5-e2a1bcb552fc" /> |

**Kode:**

```html
<!-- index.html — Struktur Certificate Cards dengan Vue -->
<div class="certificates" id="certificates">
  <div class="cert-content container">
    <h2 class="section-title">CERTIFICATES</h2>
    <hr>
    <div class="row g-3">
      <!-- v-for merender kartu untuk setiap sertifikat -->
      <div class="col-sm-6 col-md-4" v-for="cert in certs" :key="cert.title">
        <article class="cert-card">
          <img class="cert-img" :src="cert.src" :alt="cert.title">
          <div class="cert-meta">
            <div class="cert-title">{{ cert.title }}</div>
            <div class="cert-issuer">{{ cert.issuer }}</div>
            <div class="cert-date">{{ cert.year }}</div>
            <a class="cert-link" :href="cert.link" target="_blank">view</a>
          </div>
        </article>
      </div>
    </div>
  </div>
</div>
```

```javascript
// main.js — Data sertifikat Vue.js
certs: [
  {
    title:  'The Python Programmer 2025',
    issuer: 'Udemy',
    year:   '2024',
    src:    'assets/images/PythonProgrammer.jpeg',
    link:   'assets/images/PythonProgrammer.jpeg',
  },
  {
    title:  'Pemrograman untuk Pengembang Software',
    issuer: 'Dicoding',
    year:   '2026',
    src:    'assets/images/SoftwareDev.png',
    link:   'assets/images/SoftwareDev.png',
  },
  {
    title:  'Data Visualization with Python',
    issuer: 'Udemy',
    year:   '2025',
    src:    'assets/images/Data Analyst.jpeg',
    link:   'assets/images/Data Analyst.jpeg',
  },
]
```

```css
/* style.css — Certificate Card Glassmorphism */
.cert-card {
  background: rgba(255, 251, 251, 0.05);
  border: 1px solid rgba(255, 251, 251, 0.12);
  border-radius: 12px;
  backdrop-filter: blur(10px);
  overflow: hidden;
  display: flex;
  flex-direction: column;
}
.cert-img {
  width: 100%;
  height: 160px;
  object-fit: cover; /* gambar dipotong proporsional */
}
```

**Penjelasan Kode:** Section Certificates memanfaatkan Vue.js secara penuh untuk merender kartu sertifikat secara dinamis. Array `certs` di dalam `data()` memuat objek-objek yang masing-masing memiliki properti `title`, `issuer`, `year`, `src` (path gambar thumbnail), dan `link` (URL tujuan). Vue directive `v-for="cert in certs"` mengiterasi array tersebut dan menghasilkan `<div class="col-sm-6 col-md-4">` untuk setiap sertifikat — kolom Bootstrap yang secara otomatis menata kartu menjadi 3 kolom di layar besar (md) dan 2 kolom di tablet (sm). Atribut gambar dan tautan dihubungkan secara reaktif menggunakan binding `:src="cert.src"` dan `:href="cert.link"`. Efek visual kartu menggunakan pola *glassmorphism* yang konsisten dengan elemen foto pada section About: latar transparan tipis (`rgba(255,251,251,0.05)`) dikombinasikan dengan `backdrop-filter: blur(10px)` sehingga konten di belakang kartu tampak buram secara artistik.
