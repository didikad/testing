# Prompt Pendev — Aplikasi Web Operasional & Rekam Medis Klinik Gigi ("DentaKita")

> **Cara pakai:** Salin seluruh isi di bawah garis ini, lalu tempel ke Pendev sebagai prompt pembuatan aplikasi.

---

Bangunkan saya sebuah **aplikasi web operasional & rekam medis untuk klinik gigi sederhana** bernama kerja **"DentaKita"**. Seluruh antarmuka **berbahasa Indonesia**. Desain harus **rapi, modern, bersih, menenangkan, mudah dipahami, dan tidak menyulitkan pengguna**, namun fiturnya lengkap sesuai spesifikasi di bawah. Alur antar peran harus terstruktur, dan **privasi data pasien** dijaga ketat (akses sesuai peran).

## 0. Latar Belakang Produk (bangun aplikasi berdasarkan ini)

### 0.1 Analisis Masalah (pain points yang diselesaikan)
Klinik gigi kecil–menengah umumnya menghadapi:
- **Antrean & jadwal kacau**: booking lewat telepon/WA manual, sering bentrok slot, pasien menunggu lama, dan **tingkat no-show tinggi** karena tak ada pengingat.
- **Rekam medis berserakan**: catatan di kertas/kartu status mudah hilang, sulit dicari, riwayat & odontogram tidak terdokumentasi rapi, dan rawan masalah privasi.
- **Pembayaran & tarif tidak konsisten**: tindakan tidak otomatis masuk tagihan, rekap pendapatan manual, klaim asuransi/BPJS ribet.
- **Stok bahan & obat tidak terpantau**: bahan habis pakai dan obat sering kehabisan atau kedaluwarsa tanpa peringatan.
- **Pasien tidak kembali (retensi rendah)**: tak ada pengingat kontrol rutin (scaling 6 bulan, kontrol behel), tak ada program loyalitas, sehingga pasien lari ke klinik lain.
- **Manajemen buta data**: pemilik sulit tahu tindakan terlaris, performa dokter, jam sibuk, dan tren pendapatan untuk mengambil keputusan.

### 0.2 Analisis Kebutuhan (apa yang harus disediakan aplikasi)
- **Kebutuhan fungsional**: pendaftaran & booking online dengan slot per dokter; manajemen antrean realtime; **rekam medis elektronik (EMR) + odontogram**; pencatatan diagnosa–tindakan yang otomatis jadi tagihan; resep & alur apotek; kasir tunai/non-tunai + promo + asuransi; **program membership & loyalitas**; pengingat otomatis; manajemen stok bahan/obat; laporan & analitik; manajemen user & master data.
- **Kebutuhan non-fungsional**: aman & menjaga **privasi data pasien** (akses per peran + audit log), **mudah dipakai** staf non-teknis, **cepat & realtime**, **responsif** (mobile untuk pasien, desktop/tablet untuk staf), dapat diskalakan, dan andal (data tidak hilang).
- **Kebutuhan tiap peran** diterjemahkan menjadi dasbor & hak akses pada Bagian 3.

### 0.3 Target Market & Persona Pengguna
- **Segmen bisnis**: klinik gigi mandiri / praktik dokter gigi kecil–menengah (1–5 dokter) dan jaringan klinik gigi di kota besar/menengah Indonesia yang ingin digitalisasi operasional tanpa sistem rumah sakit yang mahal.
- **Persona pasien**: usia 18–45, melek HP, ingin **booking praktis tanpa telepon**, tidak suka antre lama, dan menghargai pengingat jadwal serta transparansi biaya. Termasuk orang tua yang mem-booking untuk anak.
- **Persona staf**: resepsionis yang butuh alat cepat untuk kelola antrean & kasir; dokter gigi yang butuh EMR/odontogram efisien; perawat yang mengelola stok; pemilik/manajer yang butuh laporan.
- **Nilai jual (positioning)**: "Sistem klinik gigi yang **lengkap tapi sederhana** — dari booking pasien sampai rekam medis, pembayaran, membership, dan laporan, dalam satu aplikasi."

## 1. Gaya Visual & UX
- Tema terang (light), bersih dan higienis dengan **aksen biru-tosca medis** (mis. teal `#0EA5A4` / biru `#2563EB`), latar putih/abu sangat muda, sudut kartu membulat, bayangan lembut, banyak ruang kosong.
- **Layout dasbor operasional**: sidebar navigasi kiri (ikon + label), header atas berisi pencarian pasien, lonceng notifikasi, tanggal/jam, dan profil user ("Halo, drg. [Nama]").
- **Halaman Pasien mobile-first** (daftar & booking dari HP). Halaman staf (resepsionis/dokter/manajemen/admin) optimal di desktop/tablet.
- Komponen konsisten: tombol, **badge status** berwarna (antrean/janji/pembayaran), modal konfirmasi, toast notifikasi, tabel data yang mudah dibaca, dan empty state yang ramah.
- Komponen klinis khusus: **odontogram interaktif** (diagram 32 gigi dewasa + 20 gigi anak yang bisa diklik untuk menandai kondisi/tindakan), kartu antrean, kalender jadwal dokter, dan timeline rencana perawatan.

## 2. Rekomendasi Tech Stack
- **Frontend**: React + TypeScript, Tailwind CSS, komponen shadcn/ui, ikon lucide-react, state ringan (Zustand/React Query). Grafik laporan: Recharts.
- **Backend / BaaS**: **Supabase** (PostgreSQL + Auth + Realtime + Storage untuk foto klinis/rontgen). Alternatif: Node.js + Express + Prisma.
- **Database**: PostgreSQL.
- **Realtime**: Supabase Realtime/websocket agar antrean & status janji ter-update langsung di layar resepsionis dan dokter.
- **Auth + RBAC**: email/password + role-based access control. Pasien bisa daftar/booking via nomor HP (OTP). Data medis hanya bisa diakses dokter/perawat terkait.
- **Cetak**: resep, kwitansi/struk, surat rujukan, dan surat keterangan → print-friendly + simpan PDF.
- **Keamanan**: audit log untuk akses rekam medis, enkripsi data sensitif, dan informed consent tersimpan.

## 3. Peran Pengguna & Hak Akses (RBAC)
Setiap user login diarahkan ke dasbor sesuai perannya. Buat semua halaman, alur, dan state berikut.

### A. PASIEN (mobile-first; bisa tanpa login via OTP, atau akun)
- **Pendaftaran online**: isi data diri (nama, tgl lahir, NIK opsional, no. HP, alamat, keluhan utama/riwayat singkat).
- **Booking janji temu**: pilih **layanan/poli** (mis. Pemeriksaan, Scaling, Tambal, Cabut, Behel/Ortho, Pemutihan), pilih **dokter**, lalu pilih **tanggal & slot jam** yang tersedia (slot penuh otomatis tertutup).
- **Lihat nomor antrean & estimasi** pada hari kunjungan (update realtime).
- **Isi kuesioner pra-kunjungan** (riwayat alergi, penyakit, obat yang diminum) sebelum datang.
- **Lihat riwayat perawatan & resep** sendiri, serta **rencana perawatan** berikutnya (mis. kontrol behel bulan depan).
- **Lihat & pilih promo/paket** yang tersedia (mis. paket scaling, promo pemeriksaan gratis) sebelum bayar.
- **Membership**: daftar/menjadi member, lihat **kartu member digital** (tier, nomor, QR), saldo **poin**, dan voucher/benefit yang bisa ditukar.
- **Pembayaran**: tunai di kasir atau non-tunai (QRIS/transfer/kartu — simulasi gateway), lihat tagihan & status lunas.
- **Pengingat otomatis**: notifikasi H-1 janji temu dan pengingat jadwal kontrol.
- **Reschedule / batalkan** janji (dengan aturan batas waktu).

### B. RESEPSIONIS / FRONT OFFICE (desktop/tablet)
- **Dasbor antrean hari ini**: daftar pasien check-in, status (menunggu → dipanggil → ditangani → selesai), dan slot kosong.
- **Registrasi pasien baru** & cari pasien lama (hindari duplikat by no. HP/NIK).
- **Konfirmasi/kelola booking**: terima, jadwal ulang, atau batalkan; tandai **no-show**.
- **Check-in pasien** → terbitkan nomor antrean → arahkan ke dokter/poli.
- **Notifikasi**: ingatkan bila pasien menunggu terlalu lama, atau slot dokter bentrok.
- **Kasir**: terima pembayaran tunai & non-tunai, hitung kembalian, terapkan promo/paket, **kelola klaim asuransi/BPJS** (opsional), **cetak kwitansi/struk & rincian tindakan**.
- Melihat jadwal semua dokter (read) untuk mengarahkan pasien walk-in.

### C. DOKTER GIGI (desktop/tablet)
- **Lihat jadwal & antrean** pasien hari ini; panggil pasien berikutnya.
- **Akses rekam medis elektronik (EMR)** pasien: riwayat, alergi, kunjungan sebelumnya.
- **Odontogram interaktif**: klik gigi untuk mencatat kondisi (karies, tambalan, hilang, dll) dan **tindakan** yang dilakukan.
- **Input diagnosa & tindakan** (pakai kode/ nama tindakan + tarif otomatis masuk tagihan).
- **Buat resep** obat (nama, dosis, aturan pakai) → terkirim ke apotek/farmasi & pasien.
- **Rencana perawatan (treatment plan)** multi-kunjungan + jadwalkan kontrol berikutnya.
- **Unggah foto klinis/rontgen** ke rekam medis pasien.
- **Surat rujukan** ke spesialis bila perlu.

### D. PERAWAT / ASISTEN (tablet)
- **Siapkan ruang & alat** sesuai jadwal tindakan; checklist kesiapan.
- **Bantu input** data/vital sign ringan dan dokumentasi sebelum/sesudah tindakan.
- **Kelola stok bahan & alat habis pakai** (anestesi, bahan tambal, sarung tangan, dll); tandai pemakaian per tindakan dan **peringatan stok menipis**.
- **Tracking sterilisasi** alat (opsional).

### E. APOTEK / FARMASI (opsional; desktop)
- **Terima resep** dari dokter secara realtime.
- **Kelola stok obat** + peringatan kedaluwarsa & stok menipis.
- **Serahkan obat** ke pasien dan tandai selesai; biaya obat masuk tagihan.

### F. MANAJEMEN (desktop)
- **Terima semua laporan dari seluruh sektor**: pendapatan (harian/mingguan/bulanan), jumlah kunjungan, **tindakan terbanyak**, performa & okupansi per dokter, rata-rata waktu tunggu, tingkat no-show, pemakaian promo, serta laporan stok bahan & obat.
- Dasbor **grafik & KPI** + filter rentang tanggal + ekspor CSV/PDF.
- Read-only terhadap data klinis pasien (fokus analitik agregat, bukan rekam medis individual).

### G. ADMIN (desktop)
- **Kelola user**: tambah/edit/nonaktifkan akun, atur role (dokter, perawat, resepsionis, apotek, manajemen).
- **Kelola master data**: daftar **dokter** + jam praktik/jadwal, **layanan/poli & tarif tindakan**, daftar **obat**, dan **aktif/nonaktifkan layanan** sesuai kebutuhan klinik.
- **Kelola jadwal & slot** (durasi per slot, kuota per dokter, hari libur).
- **Kelola promo/paket** (syarat, masa berlaku).
- **Kelola membership**: atur tier & benefit, rasio & kedaluwarsa poin, paket langganan, dan voucher.
- **Pengaturan klinik** (nama, logo, jam buka, pajak, info kwitansi) dan **toggle modul opsional**; pantau **audit log** akses rekam medis.

## 3b. Membership & Loyalitas (FITUR INTI)
Program untuk meningkatkan **retensi pasien** dan kunjungan rutin. Dikelola Admin, dipakai Resepsionis/Dokter, dimiliki Pasien.
- **Pendaftaran member**: pasien menjadi member (gratis atau berbayar). Terbit **kartu member digital** (nomor unik + QR untuk check-in cepat).
- **Tier keanggotaan** (mis. **Silver / Gold / Platinum**) berdasarkan total kunjungan/belanja, dengan benefit berbeda: diskon tindakan, prioritas jadwal, gratis pemeriksaan/scaling berkala.
- **Poin loyalitas**: dapat poin tiap transaksi/tindakan; poin bisa **ditukar** jadi diskon, voucher, atau layanan gratis. Atur rasio poin & aturan kedaluwarsa poin.
- **Paket berlangganan perawatan** (mis. paket behel bulanan, paket scaling 2×/tahun, paket pemutihan) dengan penjadwalan kontrol otomatis dan harga khusus member.
- **Benefit ulang tahun & reaktivasi**: voucher ulang tahun otomatis, dan pengingat untuk member yang lama tidak berkunjung.
- **Dasbor member untuk klinik**: daftar member, tier, poin, nilai seumur hidup (lifetime value), dan laporan efektivitas program di Manajemen.
- **Integrasi**: harga/diskon member otomatis diterapkan di kasir; QR member mempercepat check-in di Resepsionis.

## 3c. Modul Tambahan yang Direkomendasikan (opsional, toggle di Admin)
- **Pengingat WhatsApp/SMS otomatis** untuk janji temu & jadwal kontrol (kurangi no-show).
- **Teledentistry**: konsultasi awal via video + unggah foto keluhan.
- **Klaim Asuransi/BPJS**: alur verifikasi peserta, rujukan, dan rekap klaim.
- **Informed consent digital**: pasien tanda tangan persetujuan tindakan di layar sebelum prosedur.
- **Manajemen inventaris lanjutan**: purchase order ke supplier + auto-potong stok per tindakan (resep bahan).
- **Rating & umpan balik pasien** setelah kunjungan; terekap di dasbor Manajemen.
- **Manajemen shift & kas** (opening/closing balance kasir per hari).

## 4. Aturan Bisnis Penting (wajib)
1. Satu slot jam per dokter = satu pasien; slot penuh otomatis tidak bisa dipilih.
2. Nomor antrean terbit saat check-in; status antrean konsisten realtime lintas peran: Terdaftar → Check-in → Menunggu → Dipanggil → Ditangani → Selesai → (Lunas).
3. Pengingat otomatis H-1 janji temu dan pada jadwal kontrol.
4. **Rekam medis & odontogram hanya dapat diakses dokter/perawat yang menangani**; setiap akses tercatat di audit log.
5. Tindakan yang dicatat dokter otomatis menambah item tagihan sesuai tarif master.
6. Resep dari dokter otomatis mengalir ke apotek dan ke riwayat pasien.
7. Perhitungan tagihan: **(Biaya tindakan + biaya obat) − Diskon/Promo + Pajak (bila ada) − Tanggungan asuransi = Total yang dibayar pasien**.
8. No-show & pembatalan punya aturan batas waktu dan tercatat untuk laporan.
9. Dokumen cetak (resep, kwitansi, rujukan) memuat identitas klinik, pasien, dokter, tanggal, dan rincian.

## 5. Model Data (entitas utama)
- `Users(role)`, `Patients(nama, tgl_lahir, kontak, alergi, riwayat)`, `Doctors(spesialisasi, jadwal)`, `Services(nama, kategori/poli, tarif, durasi, is_active)`, `Appointments(pasien, dokter, layanan, tanggal, slot, status)`, `Queues(nomor, status, waktu)`, `MedicalRecords(diagnosa, catatan, foto/rontgen)`, `Odontogram(record_id, kode_gigi, kondisi, tindakan)`, `TreatmentPlans(langkah, kunjungan, status)`, `Prescriptions(obat, dosis, aturan)`, `Medicines(stok, kedaluwarsa)`, `InventoryItems(stok_bahan, low_stock_threshold)`, `Invoices(item, subtotal, diskon, pajak, total, status)`, `Payments(metode, jumlah, kembalian)`, `Promotions(syarat, periode)`, `Consents(tindakan, ttd, waktu)`, `AuditLogs(user, aksi, record, waktu)`, `Reports(agregasi/view)`.
- **Membership**: `Members(patient_id, nomor, tier, status, tgl_gabung)`, `PointTransactions(member_id, poin, tipe earn/redeem, ref, waktu)`, `MembershipTiers(nama, syarat, benefit, diskon)`, `SubscriptionPackages(nama, layanan, harga_member, periode)`, `Vouchers(member_id, tipe, nilai, masa_berlaku, status)`.

## 6. Kriteria Selesai (acceptance)
- Pasien bisa daftar → booking dokter & slot → isi kuesioner → lihat nomor antrean realtime → bayar → lihat riwayat & jadwal kontrol.
- Resepsionis bisa registrasi/cari pasien, kelola booking & antrean, tandai no-show, menerima pembayaran tunai/non-tunai, menerapkan promo, dan mencetak kwitansi.
- Dokter bisa membuka EMR, mengisi **odontogram**, mencatat diagnosa & tindakan (otomatis ke tagihan), membuat resep, menyusun rencana perawatan, dan menjadwalkan kontrol.
- Perawat bisa menyiapkan ruang/alat dan mengelola stok bahan dengan peringatan menipis.
- Apotek (jika aktif) menerima resep, mengelola stok obat, dan menyerahkan obat.
- Manajemen melihat laporan agregat semua sektor dengan grafik + ekspor.
- Admin mengelola user, master data (dokter/layanan/tarif/obat/jadwal), promo, **membership (tier, poin, paket langganan, voucher)**, dan melihat audit log.
- Pasien bisa menjadi member, memiliki kartu digital + poin, dan benefit/diskon member otomatis diterapkan di kasir.
- Akses data sesuai peran (privasi terjaga). Sertakan **data contoh (seed)** agar aplikasi langsung bisa didemokan.

## 7. Urutan Pengerjaan yang Diminta
Mulai dengan: struktur navigasi & design system → halaman **Login** (deteksi/pemilihan role) → halaman **Pasien** (daftar + booking + antrean, mobile) → **Resepsionis** (antrean + kasir) → **Dokter** (EMR + odontogram) → **Perawat** (stok/persiapan) → **Apotek** → **Manajemen** → **Admin**. Gunakan data dummy klinik gigi: dokter (drg. Sari, drg. Budi), layanan (Pemeriksaan, Scaling, Tambal Gigi, Cabut Gigi, Behel, Pemutihan), tarif contoh, beberapa pasien & janji temo, serta stok bahan/obat.
