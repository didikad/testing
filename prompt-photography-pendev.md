# Prompt Pendev — Aplikasi Web Ekosistem Bisnis Fotografi ("LensaKita")

> **Cara pakai:** Salin seluruh isi di bawah garis ini, lalu tempel ke Pendev sebagai prompt pembuatan aplikasi.

---

Bangunkan saya sebuah **aplikasi web untuk ekosistem bisnis fotografi** bernama kerja **"LensaKita"**. Satu platform untuk **tiga lini usaha**: (1) **sewa studio foto**, (2) **sewa kamera & alat**, dan (3) **booking jasa fotografer/videografer** untuk wisuda, prewedding, wedding, wedding content creator (WCC), foto produk, keluarga, dan kebutuhan fotografi lain. Seluruh antarmuka **berbahasa Indonesia**. Desain harus **modern, estetis, bersih, mudah dipahami, dan tidak menyulitkan pengguna**, namun fiturnya lengkap sesuai spesifikasi di bawah. Alur antar peran harus terstruktur dan rapi.

## 0. Latar Belakang Produk (bangun aplikasi berdasarkan ini)

### 0.1 Analisis Masalah (pain points yang diselesaikan)
Studio/vendor fotografi kecil–menengah umumnya menghadapi:
- **Booking manual & bentrok jadwal**: pemesanan via chat/DM, jadwal studio, fotografer, dan alat dicatat manual sehingga sering **double-booking** dan miskomunikasi tanggal.
- **Ketersediaan tidak transparan**: klien tidak tahu slot studio kosong, unit kamera yang masih tersedia, atau fotografer yang available pada tanggal tertentu.
- **Sewa alat berisiko**: tidak ada pelacakan unit, kondisi, serah-terima, deposit jaminan, dan **denda keterlambatan/kerusakan** yang jelas.
- **Pembayaran tidak rapi**: DP dan pelunasan tercecer, invoice manual, sulit melacak siapa sudah bayar berapa.
- **Pengiriman hasil berantakan**: file foto/video dibagikan lewat banyak link, sulit dilacak status editing dan revisi, klien bingung cara unduh.
- **Retensi klien rendah**: tidak ada program loyalitas/membership, klien wisuda/wedding jarang kembali.
- **Manajemen buta data**: pemilik sulit tahu layanan terlaris, okupansi studio, utilisasi alat, dan performa tiap fotografer.

### 0.2 Analisis Kebutuhan (apa yang harus disediakan aplikasi)
- **Kebutuhan fungsional**: katalog layanan & paket; **booking dengan cek ketersediaan realtime** (slot studio per jam, sewa alat per rentang tanggal, jadwal fotografer per tanggal); keranjang & add-on; DP + pelunasan + invoice; **kontrak & deposit jaminan sewa**; serah-terima alat (check-in/out + kondisi); manajemen pekerjaan (shoot → editing → revisi → delivered); **galeri hasil + link unduh aman**; program **membership & loyalitas**; promo/voucher; laporan & analitik; manajemen user & master data.
- **Kebutuhan non-fungsional**: **mudah dipakai** staf non-teknis, **cepat & realtime** (anti double-booking), **responsif** (mobile untuk klien, desktop/tablet untuk staf), aman (akses per peran, link unduh berbatas waktu), andal (data & file tidak hilang), dan dapat diskalakan.

### 0.3 Target Market & Persona Pengguna
- **Segmen bisnis**: studio foto mandiri, vendor fotografi/videografi wedding & wisuda, penyedia rental kamera, dan creative agency kecil–menengah di kota besar/menengah Indonesia.
- **Persona klien**:
  - **Mahasiswa wisuda** — cari paket foto wisuda terjangkau, booking cepat dari HP.
  - **Calon pengantin** — butuh paket prewedding/wedding + WCC, ingin lihat portofolio, jadwal, dan harga yang jelas.
  - **Content creator / UMKM** — sewa studio & alat untuk foto produk/konten.
  - **Hobiis/profesional** — sewa kamera/lensa/lighting harian.
- **Persona staf**: admin/CS yang kelola booking & pembayaran; fotografer/videografer/WCC yang kelola jadwal & hasil; kru studio/logistik yang kelola alat; editor; pemilik/manajer yang butuh laporan.
- **Positioning**: "Satu aplikasi untuk semua kebutuhan fotografi — **sewa studio, sewa alat, dan booking fotografer** — dengan ketersediaan transparan, pembayaran rapi, dan hasil yang mudah diakses."

## 1. Gaya Visual & UX
- Tema bisa **terang atau gelap elegan** dengan aksen berani (mis. **ungu/indigo `#6D28D9`** atau **oranye `#F97316`**) untuk kesan kreatif; tipografi modern (judul tegas + body bersih), banyak **ruang untuk foto** (portofolio tampil besar & tajam).
- **Halaman Klien mobile-first** (jelajah layanan + booking dari HP). Halaman staf optimal di desktop/tablet.
- **Layout dasbor operasional**: sidebar navigasi kiri, header berisi pencarian, notifikasi, dan profil user.
- Komponen kunci: **kalender ketersediaan** (studio/fotografer), **katalog alat dengan foto & status** (tersedia/disewa/maintenance), kartu paket layanan, **galeri hasil** (grid foto + pemutar video), progress tracker pekerjaan, dan badge status booking/pembayaran berwarna.
- Komponen konsisten: tombol, modal konfirmasi, toast, tabel, empty state ramah.

## 2. Rekomendasi Tech Stack
- **Frontend**: React + TypeScript, Tailwind CSS, komponen shadcn/ui, ikon lucide-react, state ringan (Zustand/React Query). Grafik: Recharts. Kalender: komponen date/slot picker.
- **Backend / BaaS**: **Supabase** (PostgreSQL + Auth + Realtime + Storage untuk foto/video hasil & foto alat). Alternatif: Node.js + Express + Prisma + S3-compatible storage.
- **Database**: PostgreSQL.
- **Realtime**: Supabase Realtime/websocket untuk ketersediaan slot & status booking agar **tidak double-booking**.
- **Auth + RBAC**: email/password + OTP nomor HP untuk klien; role-based access control.
- **Pembayaran**: integrasi gateway (QRIS/VA/kartu/e-wallet — simulasi) dengan dukungan **DP (down payment) + pelunasan**.
- **Pengiriman hasil**: **link unduh aman berbatas waktu**, watermark preview sebelum lunas, unduh resolusi penuh setelah lunas.
- **Cetak/kirim**: invoice, kontrak sewa, dan tanda terима serah-terima alat → PDF.

## 3. Peran Pengguna & Hak Akses (RBAC)
Setiap user login diarahkan ke dasbor sesuai perannya. Buat semua halaman, alur, dan state berikut.

### A. KLIEN / PELANGGAN (mobile-first)
- **Jelajah katalog**: lihat 3 kategori — **Sewa Studio**, **Sewa Alat**, **Jasa Fotografer** (Wisuda, Prewedding, Wedding, WCC, Produk, Keluarga, dll) lengkap foto, deskripsi paket, dan harga.
- **Lihat portofolio** tiap layanan/fotografer sebelum memesan.
- **Booking dengan cek ketersediaan realtime**:
  - *Studio*: pilih tanggal + **slot jam**, durasi, dan add-on (lighting, background, MUA, operator).
  - *Sewa alat*: pilih unit (kamera/lensa/lighting/gimbal) + **rentang tanggal** sewa; unit yang sedang disewa otomatis tak bisa dipilih.
  - *Jasa foto*: pilih paket (mis. wisuda/prewedding/wedding/WCC), tanggal acara, lokasi, dan fotografer (jika memilih).
- **Keranjang & checkout**: gabungkan beberapa item; lihat ringkasan biaya, add-on, pajak/diskon.
- **Lihat & pilih promo/paket & benefit member** sebelum bayar.
- **Pembayaran DP + pelunasan**: bayar DP untuk mengunci jadwal, lunasi sebelum/saat hari-H; lihat status pembayaran.
- **Kontrak & deposit**: setujui syarat sewa secara digital; bayar deposit jaminan untuk sewa alat.
- **Lacak pesanan**: status (Dikonfirmasi → Terjadwal → Pengerjaan/Shoot → Editing → Siap → Selesai).
- **Terima hasil**: lihat **galeri preview** (watermark), pilih foto favorit untuk revisi/cetak, lalu **unduh file resolusi penuh** setelah lunas.
- **Membership**: kartu member digital (tier, poin, QR), tukar poin/voucher, harga khusus member.
- **Reschedule / batalkan** sesuai kebijakan; ajukan **revisi** hasil sesuai kuota paket.

### B. ADMIN / CUSTOMER SERVICE (Front Office — desktop/tablet)
- **Dasbor booking**: semua pesanan masuk (studio/alat/jasa) dengan status & pembayaran; konfirmasi/tolak, **jadwal ulang**, tandai **no-show/batal**.
- **Kalender terpadu**: ketersediaan **studio**, **fotografer**, dan **alat** dalam satu tampilan untuk hindari bentrok.
- **Assign fotografer/videografer/WCC & editor** ke tiap job.
- **Kelola sewa alat**: cek stok & kondisi unit, proses **serah-terima (check-out/in)**, catat kondisi & kelengkapan, hitung **denda keterlambatan/kerusakan**, kelola deposit (tahan/kembalikan).
- **Kasir & invoice**: terima pembayaran tunai/non-tunai, **DP & pelunasan**, terapkan promo/benefit member, cetak invoice/kontrak/tanda terima.
- **Komunikasi**: catat brief klien, kirim pengingat jadwal & pelunasan.

### C. FOTOGRAFER / VIDEOGRAFER / WCC (Talent — mobile/tablet)
- **Lihat jadwal & job** yang di-assign (tanggal, lokasi, paket, brief klien, kontak).
- **Update status pekerjaan**: Terjadwal → On-location/Shoot → Selesai shoot → serahkan file ke editor.
- **Unggah hasil mentah** (atau tandai sudah diserahkan) dan catat jumlah file.
- **Ketersediaan diri**: atur tanggal available/blok tanggal agar tidak di-assign saat tidak bisa.
- Lihat ringkasan performa & jadwal mendatang.

### D. EDITOR (desktop)
- **Terima file** dari fotografer per job.
- **Kelola antrean editing** + tenggat; update status (Editing → Review → Revisi → Final).
- **Unggah hasil final** ke galeri klien; kelola kuota **revisi** sesuai paket.

### E. KRU STUDIO / LOGISTIK (tablet)
- **Siapkan studio** sesuai jadwal (lighting, background, properti) + checklist kesiapan.
- **Kelola inventaris alat**: tandai unit tersedia/disewa/**maintenance**, jadwalkan perawatan/kalibrasi, catat kerusakan.
- **Dukung serah-terima** alat bersama Admin (foto kondisi saat keluar & kembali).

### F. MANAJEMEN (desktop)
- **Terima semua laporan dari seluruh lini**: pendapatan per kategori (studio/alat/jasa) & per paket, **okupansi studio**, **utilisasi/ROI alat**, performa & jadwal tiap fotografer/editor, tingkat konversi booking, no-show, pemakaian promo, dan efektivitas membership.
- Dasbor **grafik & KPI** + filter rentang tanggal + ekspor CSV/PDF.
- Read-only operasional; fokus analitik agregat.

### G. ADMIN SISTEM (desktop)
- **Kelola user** & role (admin/CS, fotografer, editor, kru, manajemen).
- **Kelola master data**: layanan & **paket + tarif** (per kategori), **daftar alat/unit** (kamera, lensa, lighting, dll) + harga sewa & deposit, **data studio** (ruang, kapasitas, tarif/jam), **profil fotografer** + jadwal, serta **aktif/nonaktifkan** layanan/alat.
- **Kelola slot & kebijakan**: durasi slot studio, jam operasional, hari libur, kebijakan DP/refund/denda.
- **Kelola promo/paket & membership** (tier, poin, voucher).
- **Pengaturan bisnis** (nama, logo, pajak, info invoice/kontrak) + **toggle modul opsional** + **audit log**.

## 3b. Membership & Loyalitas (FITUR INTI)
Program untuk meningkatkan **retensi & repeat order**. Dikelola Admin, dipakai Admin/CS, dimiliki Klien.
- **Pendaftaran member** (gratis/berbayar) → **kartu member digital** (nomor unik + QR).
- **Tier** (mis. **Silver / Gold / Platinum**) berdasarkan total transaksi: benefit diskon sewa/jasa, prioritas jadwal, gratis add-on, atau free session berkala.
- **Poin loyalitas**: earn tiap transaksi, **redeem** jadi diskon/voucher/sewa gratis; atur rasio & kedaluwarsa.
- **Paket bundling/berlangganan** (mis. paket konten kreator bulanan untuk UMKM, paket wisuda grup/kampus, membership komunitas fotografer untuk sewa alat lebih murah).
- **Benefit ulang tahun & reaktivasi** (voucher otomatis, pengingat untuk klien lama).
- **Dasbor member** untuk klinik bisnis: daftar member, tier, poin, lifetime value, dan laporan efektivitas di Manajemen.
- **Integrasi**: diskon member otomatis di checkout; QR member mempercepat identifikasi di studio.

## 3c. Modul Tambahan yang Direkomendasikan (opsional, toggle di Admin)
- **Pengingat WhatsApp/email otomatis**: konfirmasi booking, pengingat H-1, pengingat pelunasan, dan notifikasi hasil siap diunduh.
- **Review & rating** klien terhadap fotografer/paket (tingkatkan kepercayaan + konten sosial).
- **Referral**: kode referral antar klien (dapat poin/diskon).
- **Cetak foto & merchandise**: pesan cetak/album/frame langsung dari galeri hasil.
- **Kontrak digital bertanda tangan** (e-signature) untuk jasa wedding/prewedding.
- **Kalender tim & Google Calendar sync** untuk fotografer.
- **Manajemen shift & kas** kasir harian.

## 4. Aturan Bisnis Penting (wajib)
1. **Anti double-booking**: satu slot studio / satu unit alat / satu jadwal fotografer hanya untuk satu pesanan pada waktu yang sama; yang sudah terpakai otomatis tertutup.
2. Sewa alat dihitung **per rentang tanggal**; unit kembali ke status "tersedia" setelah **check-in** dan pemeriksaan kondisi.
3. **DP mengunci jadwal**; jadwal dianggap batal bila DP tidak dibayar dalam batas waktu. Pelunasan wajib sebelum unduh hasil resolusi penuh.
4. **Deposit jaminan** untuk sewa alat ditahan dan dikembalikan setelah alat kembali utuh & tepat waktu; **denda keterlambatan/kerusakan** dipotong dari deposit.
5. Status pesanan konsisten realtime lintas peran: Dikonfirmasi → Terjadwal → Shoot → Editing → Review/Revisi → Siap → Selesai.
6. **Kuota revisi** mengikuti paket; revisi melebihi kuota dikenai biaya.
7. Preview hasil ber-**watermark**; **unduh penuh hanya setelah lunas**; link unduh berbatas waktu.
8. Perhitungan tagihan: **(Harga paket/sewa + add-on) − Diskon/Promo/benefit member + Pajak (bila ada) = Total**; DP = sebagian, sisa = pelunasan; deposit terpisah dari tagihan.
9. Reschedule/cancel punya kebijakan & tenggat yang tercatat untuk laporan.
10. Dokumen (invoice, kontrak, tanda terima alat) memuat identitas bisnis, klien, item, tanggal, dan rincian.

## 5. Model Data (entitas utama)
- `Users(role)`, `Clients(nama, kontak, alamat)`, `Photographers(spesialisasi, jadwal, portofolio)`, `Studios(nama, kapasitas, tarif_per_jam)`, `Equipment(nama, kategori, unit_code, harga_sewa, deposit, status)`, `Services(kategori, nama_paket, harga, durasi, kuota_revisi, is_active)`.
- `Bookings(client, tipe[studio/alat/jasa], tanggal, slot/rentang, status)`, `BookingItems(ref, add_on, qty, harga)`, `Assignments(booking, photographer, editor)`, `Availability(resource_id, tanggal, blok)`.
- `RentalHandovers(equipment_unit, checkout_time, checkin_time, kondisi, denda)`, `Deposits(booking, jumlah, status)`.
- `Jobs(booking, status, tenggat)`, `Deliverables(job, galeri/link, watermark, revisi_terpakai)`, `MediaAssets(file, tipe, resolusi)`.
- `Invoices(item, subtotal, diskon, pajak, total, dp, sisa, status)`, `Payments(metode, jumlah, tipe[dp/pelunasan/deposit])`, `Promotions(syarat, periode)`.
- **Membership**: `Members(client_id, nomor, tier, poin, status)`, `PointTransactions(member_id, poin, tipe, ref)`, `MembershipTiers(nama, syarat, benefit)`, `Vouchers(member_id, nilai, masa_berlaku, status)`.
- `Reviews(booking, rating, komentar)`, `AuditLogs(user, aksi, record, waktu)`, `Reports(agregasi/view)`.

## 6. Kriteria Selesai (acceptance)
- Klien bisa menjelajah 3 kategori, melihat portofolio, **booking studio (slot jam), sewa alat (rentang tanggal), atau jasa foto** dengan ketersediaan realtime, membayar **DP lalu pelunasan**, menyetujui kontrak + deposit, melacak status, dan **mengunduh hasil** setelah lunas.
- Admin/CS mengelola semua booking, kalender terpadu anti-bentrok, assign fotografer & editor, proses serah-terima alat + denda/deposit, dan invoice (DP/pelunasan).
- Fotografer/WCC melihat job & brief, update status shoot, dan menyerahkan file.
- Editor mengelola antrean editing, revisi sesuai kuota, dan mengunggah hasil final ke galeri klien.
- Kru/Logistik mengelola kesiapan studio dan status/maintenance alat.
- Manajemen melihat laporan agregat semua lini (pendapatan, okupansi studio, utilisasi alat, performa fotografer) dengan grafik + ekspor.
- Admin sistem mengelola user, master data (layanan/paket/tarif/alat/studio/jadwal), promo, membership, dan audit log.
- Akses sesuai peran; **tidak terjadi double-booking**. Sertakan **data contoh (seed)** agar aplikasi langsung bisa didemokan.

## 7. Urutan Pengerjaan yang Diminta
Mulai dengan: struktur navigasi & design system → **halaman Klien** (katalog 3 kategori + booking + checkout DP, mobile) → **Admin/CS** (kalender terpadu + booking + serah-terima alat + kasir) → **Fotografer/WCC** (jadwal + job) → **Editor** (antrean + galeri) → **Kru/Logistik** (studio + inventaris alat) → **Manajemen** (laporan) → **Admin sistem** (master data). Gunakan data dummy: studio (Studio A/B), alat (Sony A7 IV, Canon R6, lensa 50mm, lighting Godox, gimbal), fotografer (Rian - wedding, Dina - wisuda/WCC), paket (Wisuda Basic/Premium, Prewedding, Wedding Full-day, WCC Reels), serta beberapa klien & booking contoh.
