# Mini-Project-1-PAB
Nurhidayah | 2409116002 A’24

Oke, sekarang aku jelaskan berdasarkan **kode asli kamu** di `index.html`  dan `style.css`  supaya bisa langsung kamu pakai untuk penjelasan di README atau presentasi.

## 1) Tampilan Setiap Section/Fitur

Berikut tampilan yang ada di website kamu:

### A. Navbar (Menu Navigasi)

* Ada di bagian paling atas.
* **Sticky** (tetap di atas saat scroll).
* Berisi brand **any.gmmtv.** dan menu: **Home, About, Certificates**.

### B. Hero / Home

* Menampilkan judul: “Halo, aku ANY”
* Ada deskripsi singkat.
* Tombol **Get to Know Me** menuju section About.
* Ada gambar profil di kanan.

### C. About Me

* Menampilkan 2 card:

  1. **Deskripsi** tentang Any.
  2. **Skills** berupa progress bar + persentase (HTML, CSS, Desain, dll).

### D. Certificates

* Menampilkan daftar sertifikat dalam bentuk **card** (3 kolom).
* Masing-masing ada tombol **View Certificate** (link ke Google Drive).

### E. Footer

* Menampilkan copyright otomatis tahun sekarang.
* Ada tombol **Back to top** kembali ke Home.

## 2) Penjelasan Code Setiap Section/Fitur

### A. Navbar

**HTML (`index.html`)** 

```html
<nav class="navbar navbar-expand-lg navbar-dark sticky-top nav-glass">
```

Penjelasan:

* `navbar` → komponen navbar dari Bootstrap
* `navbar-expand-lg` → navbar responsive (di HP jadi hamburger)
* `sticky-top` → navbar menempel di atas saat scroll
* `nav-glass` → class custom buatan kamu untuk efek “kaca/blur”

Menu pakai anchor:

```html
<a class="nav-link text-white" href="#about">About</a>
```

Artinya klik “About” → scroll ke section `id="about"`.

**CSS (`style.css`)** 

```css
.nav-glass{
  background: rgba(11,18,32,.85) !important;
  backdrop-filter: blur(10px);
  border-bottom: 1px solid var(--border);
}
```

Ini bikin navbar transparan + blur (glassmorphism).

Tambahan penting biar scroll anchor tidak ketutup navbar:

```css
#home, #about, #certificates{ scroll-margin-top: 90px; }
```

### B. Hero / Home

**HTML** 

```html
<header id="home" class="section hero-section">
```

`id="home"` dipakai untuk tujuan scroll menu Home.

Judul menggunakan Vue binding:

```html
Halo, aku <span class="text-info">{{ profile.name }}</span>
```

`{{ profile.name }}` diambil dari data Vue:

```js
profile: { name: "ANY", shortIntro: "..." }
```

Gambar profil:

```html
<img class="profile-img" src="assets/any.jpeg" alt="Foto Profil">
```

**CSS** 

```css
.profile-img{
  width: min(320px, 90%);
  aspect-ratio: 1/1;
  object-fit: cover;
  border-radius: 22px;
}
```

* `aspect-ratio: 1/1` → gambar tetap kotak
* `object-fit: cover` → gambar tidak gepeng
* `border-radius` → sudut membulat

Efek glow pada hero:

```css
.hero-section::before{
  background: radial-gradient(circle, rgba(206,1,88,0.25), transparent 70%);
  filter: blur(100px);
}
```

### C. About Me

**HTML** 
Section about:

```html
<section id="about" class="section">
```

Card Deskripsi:

```html
<p class="text-white-50 mb-0">{{ about.description }}</p>
```

Data dari Vue:

```js
about: { description: "ANY adalah ..." }
```

Card Skills pakai `v-for`:

```html
<div v-for="(s, i) in skills" :key="i" class="mb-3">
```

Artinya: Vue mengulang data skills (HTML, CSS, dll).

Progress bar dinamis:

```html
<div class="progress-bar" :style="{ width: s.level + '%' }"></div>
```

Lebar progress = sesuai nilai `level` (misal 70%).

**CSS Progress** 

```css
.progress{ border-radius: 999px; height: 12px; }
.progress-bar{ background: var(--accent) !important; }
```

### D. Certificates

**HTML** 
Section:

```html
<section id="certificates" class="section section-alt">
```

`section-alt` → background beda warna (lebih gelap/beda).

List sertifikat pakai `v-for`:

```html
<div class="col-md-4" v-for="(c, i) in certificates" :key="i">
```

Tombol link hanya muncul jika `c.link` ada:

```html
<a v-if="c.link" :href="c.link" target="_blank" class="btn btn-sm btn-info">
```

* `v-if="c.link"` → tombol muncul kalau ada link
* `target="_blank"` → link kebuka tab baru

**CSS Card Sertifikat** 

```css
.cert-card{
  border-radius: 18px;
  box-shadow: 0 18px 60px rgba(0,0,0,.18);
}
.cert-card:hover{
  transform: translateY(-6px);
}
```

Efek hover naik biar interaktif.

### E. Footer

**HTML** 

```html
© {{ new Date().getFullYear() }} {{ profile.name }} • Portfolio
```

Tahun otomatis sesuai tahun sekarang (tidak perlu update manual).

### F. Vue Cloak (biar {{ }} tidak muncul)

**CSS** 

```css
[v-cloak] { display: none; }
```

**HTML** 

```html
<div id="app" v-cloak>
```

Artinya: sebelum Vue selesai render, konten disembunyikan supaya tulisan `{{ }}` tidak kelihatan.

### G. Tema Warna & Override Bootstrap

**CSS Variables** 

```css
:root{
  --primary: #6c0630;
  --accent:  #ce0158;
}
```

Keuntungan: ganti tema cukup ubah 1 tempat.

Override tombol bootstrap:

```css
.btn-info{
  --bs-btn-bg: var(--accent) !important;
  --bs-btn-hover-bg: var(--primary) !important;
}
```

Jadi tombol Bootstrap ngikut warna custom kamu.

## 3) Teknologi yang Digunakan

* **HTML5** → struktur halaman (navbar, section, footer) 
* **CSS3** → tema warna, efek glassmorphism, hover, glow, animasi 
* **Bootstrap 5.3.3 (CDN)** → grid layout, navbar, button, card spacing 
* **Vue JS 3 (CDN)** → data binding `{{ }}`, loop `v-for`, kondisi `v-if` 
* **JavaScript** → logic Vue App (`createApp`, data) 
