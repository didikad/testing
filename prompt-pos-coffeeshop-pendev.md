# Prompt Pendev — Aplikasi Web POS & Operasional Coffee Shop ("KopiKita POS")

> **Cara pakai:** Salin seluruh isi di bawah garis ini, lalu tempel ke Pendev sebagai prompt pembuatan aplikasi.

---

Bangunkan saya sebuah **aplikasi web Point of Sale (POS) & operasional untuk coffee shop sederhana** bernama kerja **"KopiKita POS"**. Seluruh antarmuka **berbahasa Indonesia**. Desain harus **rapi, modern, bersih, mudah dipahami, dan tidak menyulitkan pengguna**, namun fiturnya lengkap sesuai spesifikasi di bawah. Alur antar peran harus terstruktur dan konsisten.

## 1. Gaya Visual & UX
- Tema terang (light) dengan **warna aksen hijau** (mis. emerald `#16A34A`), latar putih/abu sangat muda, sudut kartu membulat (rounded-2xl), bayangan lembut.
- **Layout dasbor operasional**: sidebar navigasi di kiri (ikon + label), header atas berisi kolom pencarian, lonceng notifikasi, dan profil user ("Halo, [Nama]").
- Konten utama di tengah: daftar **kategori** sebagai chip/tab horizontal, lalu **grid kartu produk** (foto menu, nama, harga, tombol hijau "+ Tambah").
- Untuk layar kasir: **panel "Pesanan Berjalan" di kanan** berisi nomor meja/tipe order, daftar item + qty, kolom catatan, lalu **Ringkasan**: Subtotal, Diskon, Pajak (PPN 11%), Total, dan tombol besar **"Simpan"** serta **"Bayar / Terima Pembayaran"**.
- Responsif: desktop (kasir/admin/manajemen), tablet (barista/kasir/runner), dan **mobile-first untuk halaman Pelanggan** (diakses dari HP via QR).
- Komponen konsisten: tombol, badge status (warna berbeda per status pesanan), modal konfirmasi, toast notifikasi, dan empty state yang ramah.

## 2. Rekomendasi Tech Stack
- **Frontend**: React + TypeScript, Tailwind CSS, komponen shadcn/ui, ikon lucide-react, state ringan (Zustand/React Query).
- **Backend / BaaS**: **Supabase** (PostgreSQL + Auth + Realtime + Storage). Alternatif: Node.js + Express.
- **Database**: PostgreSQL.
- **Realtime**: gunakan Supabase Realtime/websocket agar pesanan baru & perubahan status langsung muncul di layar Barista, Kasir, dan Pelanggan tanpa refresh.
- **Auth + RBAC**: email/password dengan role-based access control. Pelanggan boleh akses tanpa login (sesi tamu via QR); login opsional untuk poin/riwayat.
- **Cetak struk**: render struk HTML → print-friendly (ukuran 58mm/80mm) + opsi simpan PDF.
- **QR**: generator QR per meja yang mengarah ke URL `.../meja/{kode_meja}`.

## 3. Peran Pengguna & Hak Akses (RBAC)
Setiap user login diarahkan ke dasbor sesuai perannya. Buat semua halaman, alur, dan state berikut.

### A. PELANGGAN (via QR di meja, mobile-first)
Alur: scan QR di meja → halaman menu meja tersebut terbuka.
- **Booking meja otomatis**: saat scan QR, meja berstatus "terisi/aktif" dan pelanggan menempatinya; tampilkan nomor meja yang sedang dipakai.
- **Lihat & cari menu** per kategori (Kopi, Non-Kopi, Makanan/Snack, Dessert) dengan foto, deskripsi, harga. Menu habis/di-nonaktifkan tampil "Habis" dan tidak bisa dipesan.
- **Pesan**: tambah ke keranjang, atur qty, tambah catatan (mis. "less sugar"), lalu kirim pesanan.
- **Lihat & pilih diskon/promo** yang tersedia (voucher/promo aktif) sebelum bayar; sistem memvalidasi syarat promo.
- **Pembayaran**: pilih bayar di kasir (tunai) atau bayar digital (e-wallet/QRIS/kartu — cukup simulasi gateway). Tampilkan status pesanan realtime: Menunggu konfirmasi → Diproses → Siap → Selesai.
- Mode order: **Dine-in** (default via QR), serta opsi **Takeaway**.
- Riwayat pesanan sederhana (opsional jika login).

### B. KASIR (desktop/tablet)
- **Dasbor pelanggan aktif**: daftar meja terisi + ringkasan pesanan tiap meja, dan **daftar meja kosong**.
- **Notifikasi otomatis**: jika sebuah meja sudah scan/booking **>10 menit tetapi belum memesan**, munculkan alert ke kasir agar bisa menghampiri.
- **Terima pembayaran tunai & non-tunai**; hitung kembalian untuk tunai; tandai pesanan "Lunas".
- **Ubah/edit pesanan** bila pelanggan minta (tambah/hapus item, ubah qty, ubah catatan) — perubahan terkirim ke Barista.
- **Cetak struk** saat diminta pelanggan; serta **cetak struk untuk order Takeaway/Delivery**.
- **Menu ulang tahun (Birthday Treats)**: tambahkan item/promo ulang tahun ke pesanan pelanggan yang berulang tahun, **dengan syarat verifikasi KTP** (konfirmasi tanggal lahir sesuai KTP + centang "KTP sudah diverifikasi" sebelum promo bisa diterapkan; catat ke audit log).
- Membuat pesanan baru manual (walk-in), selain yang masuk dari pelanggan.

### C. DAPUR / BARISTA (tablet, layar antrean)
- **Terima informasi pesanan masuk** realtime (kartu order: item, qty, catatan, nomor meja/tipe).
- **Setujui/terima pesanan** lalu ubah status: Diterima → Dibuat → Siap. Pelanggan & kasir melihat perubahan.
- **Atur jumlah stok** menu yang tersedia.
- **Update ketersediaan menu**: tandai "Tersedia / Tidak Tersedia / Habis"; langsung memengaruhi tampilan menu pelanggan.

### D. MANAJEMEN (desktop)
- **Terima semua laporan dari seluruh sektor**: penjualan harian/mingguan/bulanan, menu terlaris, pendapatan tunai vs non-tunai, rata-rata waktu layanan, pemakaian promo/diskon, laporan stok, performa per kasir/barista.
- Dasbor berisi **grafik & KPI** (total omzet, jumlah transaksi, rata-rata nilai order) + filter rentang tanggal + ekspor CSV/PDF.
- Read-only terhadap operasional (tidak mengubah pesanan); fokus analitik.

### E. ADMIN (desktop)
- **Kelola user**: tambah/edit/nonaktifkan akun, atur role tiap user.
- **Kelola menu & kategori**: tambah/edit/hapus menu (nama, foto, harga, kategori, deskripsi), dan **aktifkan/nonaktifkan menu** sesuai kebutuhan toko.
- **Kelola meja & QR**: buat meja, generate QR per meja.
- **Kelola promo/diskon**: buat voucher, atur syarat, masa berlaku, termasuk konfigurasi promo ulang tahun.
- Pengaturan toko (nama, pajak/PPN, jam buka, info struk) dan **toggle modul opsional**.

### F. PELAYAN / RUNNER (opsional, direkomendasikan) — tablet/HP
Berguna di coffee shop yang mengantar pesanan ke meja.
- Melihat daftar pesanan berstatus **"Siap"** dari Barista.
- Menandai **"Sedang diantar" → "Terkirim ke meja"**; status ikut update ke pelanggan & kasir.
- Melihat daftar meja sebagai tujuan antar, dan menandai meja perlu **dibersihkan** setelah pelanggan pergi (lalu meja kembali "kosong/siap dipakai").
- Jika toko kecil (self-pickup), role ini bisa dimatikan; tugasnya ditangani Barista + Kasir.

## 3b. Modul Tambahan yang Direkomendasikan (opsional, toggle di Admin)
- **Program Loyalitas / Member**: daftar nomor HP → kumpul poin tiap transaksi → tukar reward. Terhubung ke promo ulang tahun (deteksi member berulang tahun otomatis).
- **Manajemen Inventaris & Supplier**: stok bahan baku (biji kopi, susu, sirup), **low-stock alert**, pencatatan purchase order ke supplier, dan auto-kurangi stok bahan saat menu terjual (resep/bill of materials sederhana).
- **Rating & Umpan Balik Pelanggan**: setelah selesai, pelanggan beri rating/komentar singkat; terekap di dasbor Manajemen.
- **Manajemen Shift & Kehadiran**: clock-in/out karyawan, buka–tutup kasir (opening/closing balance), rekap kas per shift.
- **Supervisor / Shift Leader** (sub-role): wewenang **void/refund transaksi**, menyetujui diskon manual besar, dan menutup kasir harian — dipisah dari kasir biasa.
- **Kitchen Display System (KDS)** layar besar untuk antrean dapur + **cetak label cup** (nama pelanggan + varian).
- **Mode Offline ringan**: tetap bisa catat order & cetak struk saat internet putus, sinkron saat kembali online.

## 4. Aturan Bisnis Penting (wajib)
1. QR tiap meja → URL unik → booking + pesan dalam satu alur.
2. Timer 10 menit per meja: terisi tapi belum ada pesanan → notifikasi kasir.
3. Status pesanan konsisten lintas role (realtime): Baru → Dikonfirmasi Barista → Dibuat → Siap → Diantar/Diambil → Selesai → (Lunas).
4. Menu "Tidak Tersedia/Habis" otomatis tidak bisa dipesan pelanggan.
5. Promo ulang tahun hanya aktif setelah **verifikasi KTP** oleh kasir (ada jejak audit).
6. Perhitungan: **Subtotal − Diskon + Pajak (PPN 11%) + (Ongkir jika delivery) = Total**.
7. Struk memuat: nama toko, tanggal/jam, nomor order, kasir, item+qty+harga, ringkasan, metode bayar, kembalian, tipe order (dine-in/takeaway/delivery).

## 5. Model Data (entitas utama)
- `Users(role)`, `Tables(meja, status, qr_code)`, `Categories`, `MenuItems(harga, stok, is_available)`, `Orders(tipe, status, table_id, customer_id, total)`, `OrderItems(qty, catatan, harga)`, `Payments(metode, jumlah, kembalian, status)`, `Promotions(syarat, periode, tipe termasuk birthday)`, `AuditLogs(mis. verifikasi KTP)`, `Reports(agregasi/view)`.
- **Opsional** (jika modul diaktifkan): `Members(hp, poin, tgl_lahir)`, `Ingredients/Inventory(stok_bahan, low_stock_threshold)`, `Recipes(menu→bahan)`, `Suppliers & PurchaseOrders`, `Feedback(rating, komentar)`, `Shifts(open/close balance, kehadiran)`.

## 6. Kriteria Selesai (acceptance)
- Pelanggan bisa scan QR → pesan → pilih promo → bayar, dan melihat status realtime.
- Kasir melihat meja aktif/kosong, menerima notifikasi 10 menit, memproses pembayaran tunai & non-tunai, edit pesanan, cetak struk, dan menambah promo ulang tahun dengan verifikasi KTP.
- Barista menerima & menyetujui pesanan, mengatur stok & ketersediaan menu.
- Manajemen melihat laporan agregat dari semua sektor dengan grafik + ekspor.
- Admin mengelola user, menu (aktif/nonaktif), meja/QR, dan promo.
- Navigasi antar role jelas, konsisten, dan sesuai hak akses.
- Sertakan **data contoh (seed)** agar aplikasi langsung bisa didemokan.

## 7. Urutan Pengerjaan yang Diminta
Mulai dengan: struktur navigasi & design system → halaman **Login** (deteksi/pemilihan role) → halaman **Pelanggan** (mobile) → **Kasir** → **Barista** → **Manajemen** → **Admin** → (opsional) **Runner**. Gunakan data dummy coffee shop: Espresso, Americano, Latte, Cappuccino, Caramel Macchiato, Matcha Latte, Chocolate, Teh, Croissant, Donut, Cheesecake, dll.
