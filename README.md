# Mini-Project-1-PAB
Nurhidayah | 2409116002 A’24

## 1) Tampilan Setiap Section/Fitur

### A. Navbar (Menu Navigasi)

<img width="1890" height="89" alt="image" src="https://github.com/user-attachments/assets/87126430-b71c-4908-a5ee-e636e6a4e0a5" />

Navbar saya letakkan di bagian paling atas halaman dan saya buat bersifat sticky, sehingga tetap terlihat ketika pengguna melakukan scroll. Di dalam navbar terdapat brand any.gmmtv. serta tiga menu utama yaitu Home, About, dan Certificates. Setiap menu akan mengarahkan pengguna ke section yang sesuai melalui sistem anchor link.

### B. Hero / Home

<img width="1871" height="795" alt="image" src="https://github.com/user-attachments/assets/404a724d-8674-47e5-9991-9792a9886dae" />

Pada bagian Hero atau Home, saya menampilkan perkenalan singkat berupa judul “Halo, aku ANY” yang dilengkapi dengan deskripsi singkat mengenai karakter tersebut. Di bagian ini juga terdapat tombol “Get to Know Me” yang akan mengarahkan pengguna ke section About. Di sisi kanan, saya menampilkan gambar profil yang sudah disesuaikan agar tetap proporsional dan responsif di berbagai ukuran layar.

### C. About Me

<img width="1885" height="809" alt="image" src="https://github.com/user-attachments/assets/044ab823-77bf-42e8-9f79-5cb1a00ef804" />

Pada section About Me, saya membaginya menjadi dua bagian utama dalam bentuk card. Card pertama berisi deskripsi lengkap mengenai karakter Any. Card kedua menampilkan daftar skills dalam bentuk progress bar dengan persentase yang berbeda-beda. Progress bar ini dibuat dinamis sehingga lebarnya mengikuti nilai persentase yang sudah ditentukan.

### D. Certificates

<img width="1886" height="115" alt="image" src="https://github.com/user-attachments/assets/01c40fc5-e408-45af-ac00-19e69b7b10e6" />

Pada bagian Certificates, saya menampilkan beberapa sertifikat dalam bentuk card yang tersusun dalam tiga kolom. Setiap card berisi judul sertifikat, penyelenggara, tahun, serta tombol “View Certificate” yang terhubung langsung ke link Google Drive. Tampilan card dibuat interaktif dengan efek hover agar terlihat lebih modern.

### E. Footer

<img width="1892" height="654" alt="image" src="https://github.com/user-attachments/assets/8badc507-e4a8-43db-8e26-9b157b76173a" />

Pada bagian footer, saya menampilkan copyright yang secara otomatis menyesuaikan dengan tahun saat ini menggunakan JavaScript. Selain itu, terdapat tombol “Back to top” yang memudahkan pengguna untuk kembali ke bagian atas halaman dengan cepat.

## 2) Penjelasan Code Setiap Section/Fitur

### A. Navbar

**HTML (`index.html`)**

```html
<nav class="navbar navbar-expand-lg navbar-dark sticky-top nav-glass">
```

Pada bagian navbar, saya menggunakan komponen bawaan dari Bootstrap yaitu `navbar` untuk membuat menu navigasi. Class `navbar-expand-lg` saya gunakan agar navbar bersifat responsif dan berubah menjadi menu hamburger ketika dibuka di layar kecil. Saya juga menambahkan `sticky-top` supaya navbar tetap berada di bagian atas ketika halaman discroll. Untuk tampilan visualnya, saya membuat class custom `nav-glass` yang memberikan efek blur transparan atau glassmorphism agar terlihat lebih modern.

Menu navigasi menggunakan sistem anchor seperti berikut:

```html
<a class="nav-link text-white" href="#about">About</a>
```

Ketika menu tersebut diklik, halaman akan otomatis berpindah ke section dengan `id="about"`.

**CSS (`style.css`)**

```css
.nav-glass{
  background: rgba(11,18,32,.85) !important;
  backdrop-filter: blur(10px);
  border-bottom: 1px solid var(--border);
}
```

Pada bagian CSS ini, saya mengatur background menjadi semi-transparan dan menambahkan efek blur menggunakan `backdrop-filter`. Saya juga menambahkan garis border di bagian bawah agar navbar terlihat lebih tegas.

Selain itu, saya menambahkan pengaturan berikut agar saat melakukan scroll ke section tertentu, konten tidak tertutup oleh navbar sticky:

```css
#home, #about, #certificates{ scroll-margin-top: 90px; }
```

### B. Hero / Home

**HTML**

```html
<header id="home" class="section hero-section">
```

Section ini saya beri `id="home"` agar bisa diakses melalui menu Home pada navbar. Judul pada bagian ini menggunakan data binding dari Vue JS seperti berikut:

```html
Halo, aku <span class="text-info">{{ profile.name }}</span>
```

Isi `{{ profile.name }}` diambil langsung dari object data pada Vue, sehingga jika saya ingin mengganti nama, saya cukup mengubahnya di bagian script tanpa perlu mengedit struktur HTML.

Data tersebut berada di bagian:

```js
profile: { name: "ANY", shortIntro: "..." }
```

Untuk gambar profil, saya menggunakan:

```html
<img class="profile-img" src="assets/any.jpeg" alt="Foto Profil">
```

Gambar ini kemudian saya atur tampilannya melalui CSS agar tetap proporsional dan responsif.

**CSS**

```css
.profile-img{
  width: min(320px, 90%);
  aspect-ratio: 1/1;
  object-fit: cover;
  border-radius: 22px;
}
```

Saya menggunakan `aspect-ratio` agar gambar tetap berbentuk kotak, `object-fit: cover` supaya tidak terdistorsi, dan `border-radius` untuk memberikan sudut membulat agar terlihat lebih modern.

Efek glow pada hero saya tambahkan menggunakan pseudo-element:

```css
.hero-section::before{
  background: radial-gradient(circle, rgba(206,1,88,0.25), transparent 70%);
  filter: blur(100px);
}
```

Efek ini memberikan pencahayaan lembut di belakang konten hero.

### C. About Me

**HTML**

```html
<section id="about" class="section">
```

Pada section About, saya menampilkan deskripsi dan daftar skills. Deskripsi diambil dari data Vue seperti berikut:

```html
<p class="text-white-50 mb-0">{{ about.description }}</p>
```

Data tersebut disimpan di dalam object:

```js
about: { description: "ANY adalah ..." }
```

Untuk menampilkan skills, saya menggunakan directive `v-for`:

```html
<div v-for="(s, i) in skills" :key="i" class="mb-3">
```

Dengan cara ini, setiap data dalam array `skills` akan ditampilkan secara otomatis tanpa perlu menuliskan ulang HTML berulang kali.

Progress bar dibuat dinamis menggunakan binding style:

```html
<div class="progress-bar" :style="{ width: s.level + '%' }"></div>
```

Lebar progress bar akan mengikuti nilai `level` pada masing-masing skill.

**CSS Progress**

```css
.progress{ border-radius: 999px; height: 12px; }
.progress-bar{ background: var(--accent) !important; }
```

Saya mengatur tinggi progress bar dan warna agar sesuai dengan tema yang sudah ditentukan.

### D. Certificates

**HTML**

```html
<section id="certificates" class="section section-alt">
```

Section ini saya beri class `section-alt` agar memiliki background berbeda dari section sebelumnya. Daftar sertifikat ditampilkan menggunakan `v-for`:

```html
<div class="col-md-4" v-for="(c, i) in certificates" :key="i">
```

Artinya setiap data dalam array `certificates` akan dibuat menjadi satu card.

Tombol sertifikat hanya muncul jika terdapat link:

```html
<a v-if="c.link" :href="c.link" target="_blank" class="btn btn-sm btn-info">
```

Saya menggunakan `v-if` untuk memastikan tombol hanya muncul ketika link tersedia, dan `target="_blank"` agar link terbuka di tab baru.

**CSS**

```css
.cert-card{
  border-radius: 18px;
  box-shadow: 0 18px 60px rgba(0,0,0,.18);
}
.cert-card:hover{
  transform: translateY(-6px);
}
```

Saya menambahkan efek hover agar card terlihat lebih interaktif ketika diarahkan oleh kursor.

### E. Footer

**HTML**

```html
© {{ new Date().getFullYear() }} {{ profile.name }} • Portfolio
```

Pada bagian footer, saya menggunakan ekspresi JavaScript `new Date().getFullYear()` agar tahun selalu otomatis menyesuaikan dengan tahun saat ini, sehingga tidak perlu diperbarui secara manual setiap tahun.

## F. Vue Cloak

```css
[v-cloak] { display: none; }
```

```html
<div id="app" v-cloak>
```

Saya menggunakan atribut `v-cloak` agar tanda kurung ganda `{{ }}` tidak terlihat sebelum Vue selesai melakukan proses rendering.

### G. Tema Warna & Override Bootstrap

```css
:root{
  --primary: #6c0630;
  --accent:  #ce0158;
}
```

Saya menggunakan CSS Variables untuk menyimpan warna utama dan aksen agar konsisten di seluruh website dan mudah diganti jika ingin mengubah tema.

Override tombol Bootstrap:

```css
.btn-info{
  --bs-btn-bg: var(--accent) !important;
  --bs-btn-hover-bg: var(--primary) !important;
}
```

Saya melakukan override agar tombol Bootstrap mengikuti warna custom yang sudah saya tentukan.

## 3) Teknologi yang Digunakan

* **HTML5** → struktur halaman (navbar, section, footer) 
* **CSS3** → tema warna, efek glassmorphism, hover, glow, animasi 
* **Bootstrap 5.3.3 (CDN)** → grid layout, navbar, button, card spacing 
* **Vue JS 3 (CDN)** → data binding `{{ }}`, loop `v-for`, kondisi `v-if` 
* **JavaScript** → logic Vue App (`createApp`, data) 

## 4) Struktur folder

<img width="562" height="295" alt="image" src="https://github.com/user-attachments/assets/226170d8-fca4-4160-9102-6308c5478e6e" />
