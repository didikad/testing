# Prompt Pendev — WEBSITE Bisnis Fotografi ("LensaKita")

> **Cara pakai:** Salin seluruh isi di bawah garis ini, lalu tempel ke Pendev sebagai prompt pembuatan **website**.

---

Bangunkan saya sebuah **WEBSITE** (situs web publik, bukan aplikasi internal) untuk bisnis fotografi bernama kerja **"LensaKita"**. Website ini adalah **etalase + portal booking** bagi calon klien, mencakup tiga lini usaha: (1) **sewa studio foto**, (2) **sewa kamera & alat**, dan (3) **jasa fotografer/videografer** untuk wisuda, prewedding, wedding, wedding content creator (WCC), foto produk, keluarga, dan kebutuhan fotografi lain. Fungsinya: **profil + portofolio + booking online + pembayaran + panel admin sederhana**. Seluruh antarmuka **berbahasa Indonesia**.

**WAJIB — Responsif penuh:** setiap halaman harus tampil sempurna dan nyaman digunakan di **mobile, tablet, dan desktop** (pendekatan mobile-first). Tidak boleh ada elemen yang terpotong, menumpuk, atau sulit disentuh di layar kecil.

## 0. Latar Belakang Produk (bangun website berdasarkan ini)

### 0.1 Analisis Masalah (pain points yang diselesaikan)
- **Tidak punya etalase online yang kredibel**: vendor foto hanya mengandalkan Instagram/DM, sulit menampilkan portofolio & paket secara profesional.
- **Booking ribet & lambat**: calon klien harus chat satu-satu untuk tanya jadwal, harga, dan ketersediaan; sering miskomunikasi dan **double-booking**.
- **Harga tidak transparan**: klien ragu karena paket & biaya tidak jelas di muka.
- **Portofolio tersebar** di banyak tempat, tidak terkurasi per kategori (wisuda, wedding, dll).
- **Tidak ada kanal pembayaran**: DP/booking fee masih manual, rawan jadwal diambil tapi tidak jadi.
- **Sulit ditemukan di Google** (SEO lemah) sehingga kalah dari kompetitor.

### 0.2 Analisis Kebutuhan (apa yang harus disediakan website)
- **Fungsional**: halaman profil & layanan yang jelas; **galeri portofolio** terkurasi dengan filter; daftar **paket & harga** transparan; **booking online** dengan cek ketersediaan jadwal/alat; **pembayaran DP + pelunasan**; akun klien untuk melacak pesanan & **mengunduh hasil**; form kontak + tombol WhatsApp; blog/artikel untuk SEO; panel admin sederhana untuk mengelola pesanan & konten.
- **Non-fungsional**: **responsif penuh (mobile/tablet/desktop)**, **cepat** (gambar dioptimasi, loading ringan), **SEO-friendly** (SSR/SSG, meta tag, sitemap), estetis sesuai industri kreatif, aman (link unduh hasil berbatas waktu), dan mudah dikelola pemilik.

### 0.3 Target Market & Persona
- **Segmen**: studio foto & vendor fotografi/videografi dan rental kamera skala kecil–menengah di Indonesia yang ingin punya website profesional dengan booking online.
- **Persona pengunjung**:
  - **Mahasiswa wisuda** — cari paket foto wisuda, lihat contoh hasil, booking cepat dari HP.
  - **Calon pengantin** — bandingkan paket prewedding/wedding + WCC, lihat portofolio & testimoni sebelum memutuskan.
  - **Content creator / UMKM** — sewa studio & alat untuk konten/foto produk.
  - **Hobiis/profesional** — sewa kamera/lensa/lighting harian.
- **Positioning**: "Website fotografi yang menampilkan karya terbaikmu dan memudahkan klien **booking + bayar dalam hitungan menit** — dari HP, tablet, maupun desktop."

## 1. Gaya Visual & UX
- **Estetika galeri**: foto tampil **besar, tajam, dan sinematik**; banyak ruang kosong; tipografi modern (judul tegas + body bersih). Website harus terasa premium dan kreatif.
- **Tema**: terang/krem elegan atau gelap mewah, dengan **satu aksen kreatif** (mis. indigo `#6D28D9` atau oranye `#F97316`). Konsisten di semua halaman.
- **Hero sinematik** di beranda (foto/video latar + headline + CTA ganda "Lihat Portofolio" & "Booking Sekarang").
- **Mikrointeraksi halus**: hover pada kartu portofolio, transisi lembut, lazy-load gambar, lightbox galeri, pemutar video reel.
- **Navigasi jelas**: header sticky dengan menu; di mobile/tablet jadi **menu hamburger**. Tombol WhatsApp mengambang. Footer lengkap (navigasi, kontak, sosial media, peta).
- **Responsif (WAJIB)**: mobile-first, breakpoint jelas (mobile ≤640px, tablet 641–1024px, desktop >1024px). Grid portofolio reflow (1 kolom mobile → 2 tablet → 3–4 desktop), tabel harga menjadi kartu bertumpuk di mobile, target sentuh ≥44px, tidak ada scroll horizontal.

## 2. Rekomendasi Tech Stack
- **Frontend/Framework**: **Next.js + TypeScript** (SSR/SSG untuk SEO & kecepatan), Tailwind CSS, komponen shadcn/ui, ikon lucide-react, animasi Framer Motion. Optimasi gambar via next/image + CDN.
- **Backend/Data**: **Supabase** (PostgreSQL + Auth + Storage untuk foto/video portofolio & hasil klien). Alternatif: Node.js + Prisma + S3-compatible storage.
- **Booking & ketersediaan**: cek jadwal realtime agar **tidak double-booking** (slot studio per jam, sewa alat per rentang tanggal, jadwal fotografer per tanggal).
- **Pembayaran**: integrasi gateway (QRIS/VA/kartu/e-wallet — boleh simulasi) dengan **DP (booking fee) + pelunasan**.
- **SEO & performa**: meta tag dinamis, Open Graph, sitemap.xml, schema.org (LocalBusiness/Service), skor Lighthouse tinggi.
- **Integrasi**: tombol/klik-to-chat **WhatsApp**, **Google Maps** embed, **Instagram feed** (opsional), Google Analytics.

## 3. Peta Halaman (Sitemap Publik) — ini inti website
Buat semua halaman berikut, semuanya **responsif mobile & tablet**:

1. **Beranda** — hero sinematik; ringkasan 3 layanan (Sewa Studio / Sewa Alat / Jasa Foto); **portofolio pilihan**; mengapa memilih kami (USP); testimoni; logo klien/partner; blok statistik (jumlah proyek, klien); CTA booking; teaser artikel.
2. **Tentang Kami** — cerita brand, tim/fotografer, visi, di balik layar studio.
3. **Layanan (halaman induk)** dengan sub-halaman detail:
   - **Sewa Studio** — foto ruang studio, fasilitas, kapasitas, tarif per jam, add-on (lighting/background/MUA/operator), tombol cek jadwal & booking.
   - **Sewa Alat/Kamera** — katalog unit (kamera, lensa, lighting, gimbal) dengan foto, spesifikasi, harga sewa/hari, deposit, status ketersediaan, tombol sewa.
   - **Jasa Fotografi** — kategori: **Wisuda, Prewedding, Wedding, Wedding Content Creator, Foto Produk, Keluarga/Lainnya**. Tiap kategori punya halaman: deskripsi, contoh hasil, **paket & harga**, FAQ, CTA booking.
4. **Portofolio / Galeri** — grid foto dengan **filter kategori**, lightbox, dan **video reel**; bisa buka album per proyek.
5. **Harga / Paket** — tabel paket semua layanan + add-on; di mobile jadi kartu bertumpuk yang mudah dibandingkan.
6. **Booking Online** — alur pemesanan (lihat Bagian 4).
7. **Testimoni / Review** — ulasan klien + rating + foto.
8. **Blog / Artikel** — tips foto wisuda/prewedding, persiapan wedding, dll (untuk SEO).
9. **FAQ** — pertanyaan umum (jadwal, pembayaran, revisi, pengiriman hasil, kebijakan sewa).
10. **Kontak** — form pesan, nomor WA, alamat + **Google Maps embed**, jam operasional, sosial media.
11. **Area Klien** (login) & **Panel Admin** — lihat Bagian 5 & 6.
12. **Footer global** di semua halaman + halaman **Syarat & Ketentuan** dan **Kebijakan Privasi**.

## 4. Alur Booking & Pembayaran (fungsi utama website)
1. Pengunjung pilih layanan (studio / alat / jasa foto).
2. **Cek ketersediaan**: pilih tanggal + slot jam (studio), rentang tanggal (alat), atau tanggal acara + fotografer (jasa). Slot/unit yang sudah terpakai otomatis tertutup (**anti double-booking**).
3. Pilih **paket & add-on**, lihat ringkasan biaya (termasuk promo/benefit member & pajak bila ada).
4. Isi data pemesan + detail acara/lokasi + catatan/brief.
5. Setujui **Syarat & Ketentuan** (dan deposit jaminan untuk sewa alat).
6. **Bayar DP (booking fee)** untuk mengunci jadwal → status "Terkonfirmasi". Pelunasan dilakukan sebelum/di hari-H.
7. Terima **konfirmasi** (email/WhatsApp) + nomor pesanan.
8. Setelah pengerjaan, klien **melihat galeri hasil** (preview watermark) dan **mengunduh file resolusi penuh setelah lunas** (link berbatas waktu).

Aturan: DP mengunci jadwal; jadwal batal bila DP tidak dibayar dalam batas waktu. Reschedule/cancel mengikuti kebijakan. Deposit sewa dikembalikan setelah alat kembali utuh & tepat waktu (denda keterlambatan/kerusakan dipotong dari deposit).

## 5. Area Klien (login ringan via email/OTP)
- **Dasbor klien**: daftar & status pesanan (Terkonfirmasi → Terjadwal → Pengerjaan → Siap → Selesai).
- **Galeri hasil**: preview, pilih foto favorit, ajukan **revisi** sesuai kuota paket, **unduh** file final.
- **Riwayat pembayaran**: DP, pelunasan, invoice (unduh PDF).
- **Membership & poin**: kartu member digital, poin loyalitas, voucher, harga khusus member.
- **Profil**: ubah data, simpan alamat & kontak.

## 6. Panel Admin Sederhana (pendukung, bukan fokus utama)
Cukup untuk menjalankan website sehari-hari:
- **Kelola booking masuk**: konfirmasi/tolak, jadwal ulang, tandai selesai; lihat **kalender ketersediaan** studio/alat/fotografer agar tidak bentrok.
- **Kelola pembayaran**: pantau DP & pelunasan, terbitkan/unduh invoice, kelola deposit & denda sewa.
- **Kelola konten website**: unggah/atur **portofolio & galeri**, kelola **paket & harga**, testimoni, artikel blog, dan FAQ.
- **Kelola katalog**: studio, unit alat (status tersedia/disewa/maintenance), profil & jadwal fotografer, **aktif/nonaktifkan** layanan/alat.
- **Kelola promo & membership**: voucher, tier, poin.
- **Kirim hasil**: unggah galeri hasil ke akun klien + atur hak unduh setelah lunas.

## 7. Membership, Promo & SEO (ringkas)
- **Membership**: tier (Silver/Gold/Platinum), poin loyalitas (earn/redeem), benefit diskon & prioritas, voucher ulang tahun — diterapkan otomatis saat checkout.
- **Promo**: banner promo di beranda, kode voucher di checkout.
- **SEO**: tiap halaman punya judul & meta deskripsi unik, URL rapi, gambar ber-alt text, schema LocalBusiness/Service, sitemap, dan halaman blog untuk kata kunci (mis. "jasa foto wisuda [kota]", "paket prewedding murah").

## 8. Kriteria Selesai (acceptance)
- Website punya seluruh halaman publik di Bagian 3 dan **semuanya responsif sempurna di mobile, tablet, dan desktop** (tidak ada elemen terpotong/menumpuk; menu jadi hamburger; galeri & tabel harga reflow).
- Portofolio tampil menarik dengan filter + lightbox + video; halaman layanan menampilkan paket & harga yang jelas.
- Pengunjung dapat menyelesaikan **booking online**: cek ketersediaan (anti double-booking) → pilih paket/add-on → isi data → **bayar DP** → terima konfirmasi.
- Klien dapat login, melacak status pesanan, melihat & **mengunduh hasil** (setelah lunas), dan melihat poin membership.
- Admin dapat mengelola booking, kalender ketersediaan, pembayaran, serta konten (portofolio, paket/harga, testimoni, blog) dan katalog alat/studio/fotografer.
- Website cepat (gambar teroptimasi) dan **SEO-friendly** (meta tag, sitemap). Sertakan **konten & data dummy** agar langsung bisa didemokan.

## 9. Konten Dummy
- Layanan/paket: Wisuda (Basic/Premium), Prewedding (Half/Full-day), Wedding (Full-day + WCC), WCC Reels, Foto Produk, Sewa Studio (per jam), Sewa Alat (Sony A7 IV, Canon R6, lensa 50mm, lighting Godox, gimbal).
- Portofolio: 12–20 foto contoh lintas kategori + 1–2 video reel; 4–6 testimoni; 3 artikel blog.
- Fotografer dummy: Rian (wedding), Dina (wisuda/WCC). Harga & jadwal contoh.

## 10. Urutan Pengerjaan yang Diminta
Mulai dari **design system + layout responsif** → **Beranda** → **halaman Layanan & detailnya** → **Portofolio/Galeri** → **Harga** → **alur Booking + Pembayaran DP** → **Area Klien (login, galeri hasil, unduh)** → **Panel Admin sederhana** → **Blog, FAQ, Kontak, footer, SEO**. Uji setiap halaman di lebar layar mobile, tablet, dan desktop sebelum dianggap selesai.
