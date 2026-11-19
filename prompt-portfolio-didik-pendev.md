# Prompt Pendev — Website Portofolio Personal "Didik" (Full-Stack Developer)

> **Cara pakai:** Salin seluruh isi di bawah garis ini, tempel ke Pendev. Lengkapi semua `{{PLACEHOLDER}}` dan unggah aset sesuai **Manifest Aset** (Bagian 7). Website wajib **responsif penuh (mobile, tablet, desktop)** dan **bilingual (Indonesia + English)** dengan toggle bahasa.

---

Bangunkan sebuah **website portofolio personal satu halaman (one-page, multi-section) untuk seorang Software Engineer / Full-Stack Developer** bernama **{{NAMA}}** (brand/handle: **{{HANDLE}}**, mis. "didik."). Gaya **editorial–modern, bold, dan ekspresif**, terinspirasi semangat portofolio dev kelas atas (tipografi besar berkarakter, banyak ruang kosong, grid rapi, dan **footer yang kuat sebagai penutup berkesan**) — tetapi dengan **identitas visual orisinal** (palet, layout, dan ilustrasi milik sendiri; BUKAN menyalin karya orang lain). Konten **bilingual ID/EN** dengan toggle. Target audiens: **rekruter, calon klien, dan sesama developer**. Tujuan utama: pengunjung memahami siapa {{NAMA}}, melihat proyek, lalu **menghubungi / mengunduh CV**.

## 1. Tujuan & Prinsip
- **Clarity first**: dalam 5 detik pengunjung tahu peran, keahlian inti, dan cara menghubungi.
- **Show, don't tell**: proyek nyata dengan hasil/metrik, bukan sekadar daftar skill.
- **Berkarakter tapi profesional**: ekspresif secara tipografi & motion, tetap mudah dibaca & cepat.
- **Konversi**: CTA jelas (Hubungi / Unduh CV / Lihat Proyek) hadir di hero dan footer.

## 2. Analisis Referensi & Arah Desain (acuan, bukan untuk ditiru mentah)
Dari referensi, yang **DIAMBIL SEMANGATNYA**:
- Tipografi **display besar & berkarakter** sebagai elemen utama hero + **label meta monospace** (mis. `©2026`, `{{ FULL-STACK · WEB · AI }}`, `< ROLE />`).
- Alur section yang mengalir: **Hero → Tentang → Tech Stack (tag) → Featured Projects (kartu) → Experience (timeline) → Footer besar**.
- **Footer sebagai "main character"**: area penutup besar dengan CTA kontak + wordmark raksasa + ilustrasi/tekstur khas + "See you around / Sampai jumpa".
- Sentuhan **interaktif**: micro-interaction hover, animasi scroll halus, opsi **command palette (⌘K)** / asisten tanya-jawab.
Yang **DIBUAT ORISINAL** (wajib beda dari referensi): **palet warna**, **pasangan font**, **gaya ilustrasi/aset**, **komposisi layout**, dan copywriting. Jangan memakai nama, foto, atau ilustrasi milik referensi.

## 3. Arsitektur Informasi / Section (urut dari atas)
Semua section responsif (mobile/tablet/desktop) & tersedia ID/EN.
1. **Header (sticky)**: wordmark `{{HANDLE}}` di kiri; nav (Tentang/About, Keahlian/Skills, Proyek/Projects, Pengalaman/Experience, Kontak/Contact); **toggle bahasa ID/EN**; **toggle tema (dark/light)**; tombol kecil "Hubungi/Get in touch". Di mobile → menu hamburger full-screen.
2. **Hero**: label meta mono (`< SOFTWARE ENGINEER />`, `©{{TAHUN}}`, `{{ FULL-STACK DEVELOPMENT }}`); headline display raksasa (nama/peran); subjudul 1 kalimat `{{ROLE_TAGLINE}}`; CTA ganda ("Lihat Proyek" + "Unduh CV"); foto profil (boleh diperlakukan duotone/grayscale saat idle, warna saat hover); indikator scroll.
3. **Tentang / About**: "Hi, I'm {{NAMA}}" + paragraf `{{BIO_ID}}` / `{{BIO_EN}}`; highlight ringkas (peran saat ini `{{ROLE_NOW}}`, lokasi `{{LOKASI}}`, status ketersediaan "Open to work/Freelance"); kartu foto; tombol "Explore projects".
4. **Tech Stack / Keahlian**: dikelompokkan — **Languages & Frameworks**, **Tools, Databases & Cloud**, **AI & Automation** (opsional) — ditampilkan sebagai **tag/pill** yang rapi; boleh animasi marquee lembut.
5. **Featured Projects**: grid kartu proyek (`{{PROJEK_1..n}}`) — tiap kartu: thumbnail/mockup, nama, deskripsi singkat, **tag teknologi**, link **Demo** & **Repo**, dan (opsional) halaman/panel **detail case study** (masalah → solusi → peran → hasil/metrik). Sertakan state hover yang menonjol.
6. **Experience & Education**: **timeline** vertikal (mobile) / kurva atau horizontal (desktop) berisi `{{EXP_*}}` & `{{EDU_*}}` (posisi, tempat, tahun, ringkas). 
7. **(Opsional) Testimoni / Highlights / Writing**: kutipan klien, atau statistik (jumlah proyek, tahun pengalaman), atau artikel.
8. **Footer besar ("main character")**: headline ajakan (`{{CTA_HEADLINE}}` mis. "Punya ide? Mari bikin."); **input email + tombol "Buat draft email"** (prefilled mailto) atau tombol WhatsApp; daftar tautan sosial (GitHub, LinkedIn, Instagram, X/Twitter, Email); **wordmark raksasa** `{{NAMA}}`; ilustrasi/tekstur khas; baris penutup "Sampai jumpa / See you around"; baris legal `©{{TAHUN}} {{NAMA}}` + "Back to top".
9. **(Opsional) Floating**: tombol **Command Palette (⌘K)** untuk navigasi cepat, atau **AI assistant** mini tanya-jawab tentang {{NAMA}}.

## 4. DESIGN SYSTEM (KOMPLIT)

### 4.1 Prinsip & Kepribadian
Confident · editorial · teknis-rapi · hangat. Kontras tinggi, hirarki jelas, whitespace berani, detail monospace sebagai "tanda tangan teknis".

### 4.2 Warna (palet orisinal — **dark-first**, sediakan light)
Gunakan sebagai **design tokens** (CSS variables). Contoh palet "Ink & Signal" (silakan sesuaikan, hindari meniru referensi):
```css
:root {               /* DARK (default) */
  --bg:        #0B0C0E;   /* near-black, sedikit biru */
  --surface:   #121419;   /* kartu/section */
  --surface-2: #1A1D24;   /* elevasi lebih tinggi */
  --border:    #262A32;   /* garis/divider */
  --text:      #F2F3F5;   /* teks utama */
  --text-muted:#A0A6B0;   /* teks sekunder */
  --accent:    #C6FF3D;   /* AKSEN signature (lime/electric) — ganti sesuai selera */
  --accent-ink:#0B0C0E;   /* teks di atas accent */
  --success:   #3DD68C;
  --warning:   #FFB020;
  --danger:    #FF5C5C;
  --focus:     #7AA2FF;   /* cincin fokus */
}
:root[data-theme="light"] {
  --bg:#FAFAF8; --surface:#FFFFFF; --surface-2:#F2F2EE; --border:#E4E4DF;
  --text:#121419; --text-muted:#5B616B; --accent:#1F6FEB; --accent-ink:#FFFFFF;
  --success:#1F9D63; --warning:#B6791A; --danger:#D23F3F; --focus:#1F6FEB;
}
```
Aturan: **satu warna aksen** dominan untuk CTA/highlight; sisanya netral. Pastikan kontras teks **≥ WCAG AA** (4.5:1 teks normal). Jangan pakai aksen untuk blok teks panjang.

### 4.3 Tipografi
- **Display/Heading**: grotesk tebal berkarakter — mis. *Clash Display*, *Space Grotesk*, *Anton* (untuk hero ekstra besar), atau *Neue Montreal*. Pilih **satu** untuk konsistensi.
- **Body/UI**: sans bersih — *Inter* / *Geist* / *Satoshi*.
- **Mono (label/meta/kode)**: *JetBrains Mono* / *Geist Mono* / *Space Mono*.
- **Skala tipe** (desktop; skala turun ~0.8× di mobile), rasio ~1.25–1.333:
  - Display XL (hero): clamp(48px, 10vw, 140px), weight 700–900, tracking -0.02em, line-height 0.95.
  - H1 64 · H2 40 · H3 28 · H4 20 (weight 600–700).
  - Body L 18 · Body 16 · Small 14 · Caption/Mono 12–13 (uppercase, letter-spacing 0.08em).
- Penggunaan mono: label section, meta, tag, angka/tahun, dan micro-copy teknis.

### 4.4 Spacing, Grid & Breakpoint
- **Skala spasi (8pt)**: 4, 8, 12, 16, 24, 32, 48, 64, 96, 128, 160.
- **Grid**: 12 kolom desktop, 8 tablet, 4 mobile; gutter 24px (16 di mobile); **container max** 1280–1440px; padding tepi 16 (mobile) / 24 (tablet) / 48+ (desktop).
- **Breakpoint**: `sm 640 · md 768 · lg 1024 · xl 1280 · 2xl 1536`. Mobile-first.
- Section spacing vertikal: 80–160px desktop, 56–96px mobile.

### 4.5 Radius, Border, Elevasi
- Radius: `sm 6 · md 10 · lg 16 · xl 24 · pill 999`.
- Border: 1px `--border`; gunakan garis tipis sebagai pemisah section (estetika editorial).
- Shadow (halus, hemat): `0 1px 2px rgba(0,0,0,.4)` (sm), `0 8px 30px rgba(0,0,0,.35)` (lg). Di dark, elevasi lebih mengandalkan `--surface-2` + border daripada shadow.

### 4.6 Ikon & Imagery
- **Ikon**: lucide-react (stroke 1.5–2px), konsisten ukuran 20/24.
- **Foto**: perlakuan **grayscale/duotone** saat idle → warna/hover; sudut membulat `lg`; rasio 4:5 (potret), 16:9 (mockup).
- **Ilustrasi/tekstur**: buat orisinal — mis. line-art, grid/dot texture, noise halus, atau blob/gradient. Konsisten 1 gaya.
- **Mockup proyek**: bingkai browser/perangkat sederhana; rasio 16:10.

### 4.7 Motion
- Durasi: 150ms (hover) · 300–500ms (masuk section). Easing: `cubic-bezier(0.22,1,0.36,1)` (ease-out ekspresif).
- Pola: fade+translate-y pada scroll (stagger kartu), hover scale 1.02 + garis aksen, marquee lambat untuk tag/wordmark, cursor-follow halus (opsional).
- **Hormati `prefers-reduced-motion`**: matikan animasi besar.

### 4.8 Komponen (spesifikasi + state)
Buat komponen reusable; semua punya state **default/hover/focus/active/disabled** dan versi dark/light:
- **Button**: *Primary* (bg `--accent`, teks `--accent-ink`), *Secondary* (outline `--border`), *Ghost* (teks + hover bg `--surface-2`). Tinggi 44/48, radius md/pill, ikon opsional, focus ring `--focus`.
- **Header/Nav + Language & Theme Toggle**: sticky, blur-backdrop; aktif-state underline aksen; mobile = overlay menu.
- **Tag/Pill**: mono uppercase, border `--border`, hover isi aksen tipis.
- **ProjectCard**: thumbnail + judul + desc + tags + link; hover mengangkat + garis aksen; klik → detail.
- **InputField** (footer email) + tombol **"Buat draft email"**: label, placeholder, validasi, state error; aksi menyusun `mailto:` prefilled.
- **Timeline item**: titik/garis, tahun (mono), judul, tempat, ringkas.
- **Meta label / Badge**: mono kecil, uppercase, dengan simbol (`©`, `{{ }}`, `< />`).
- **Marquee / Wordmark raksasa**: teks sangat besar (nama) sebagai elemen grafis footer.
- **Footer**: multi-kolom (nav, sosial, CTA) → bertumpuk di mobile.
- **CommandPalette (⌘K)** / **Chatbot** (opsional): modal, daftar aksi/jawaban, keyboard-accessible.
- **ThemeToggle**: simpan preferensi (localStorage), hormati `prefers-color-scheme`.

### 4.9 Aksesibilitas
Kontras AA; focus-visible ring di semua interaktif; navigasi keyboard penuh (termasuk menu & ⌘K); `alt` deskriptif untuk semua gambar; `aria-label` untuk ikon; target sentuh ≥44px; heading berurutan (satu `<h1>`); toggle bahasa meng-update `lang`.

## 5. Tech Stack
- **Next.js (App Router) + TypeScript**, **Tailwind CSS** + design tokens (CSS variables di atas), komponen **shadcn/ui**, ikon **lucide-react**, animasi **Framer Motion**.
- **Bilingual**: i18n (mis. `next-intl` atau route `/id` & `/en`) dengan toggle; semua copy disimpan sebagai pasangan `{{..._ID}}`/`{{..._EN}}`.
- **Gambar**: `next/image` (AVIF/WebP, lazy, responsive sizes). **Font**: `next/font` (self-host).
- **Form kontak**: mailto prefilled atau API route + layanan email (mis. Resend) — opsional.

## 6. SEO, Performa & Responsif (wajib)
- Meta title/description per bahasa, Open Graph + Twitter Card (OG image di manifest), `sitemap.xml`, `robots.txt`, schema.org `Person`.
- Target Lighthouse ≥ 95 (Performance/SEO/Best-practices/Accessibility); gambar teroptimasi; font preloaded; minim JS.
- **Responsif penuh**: uji setiap section di 360px (mobile), 768px (tablet), 1280px+ (desktop) — tidak boleh ada scroll horizontal, elemen terpotong, atau teks tertumpuk. Hero display memakai `clamp()` agar skala mulus.

## 7. MANIFEST & DOKUMENTASI ASET (untuk Pendev)
Simpan semua aset di `/public/assets/` dengan struktur & penamaan konsisten. **Gunakan placeholder dulu**, lalu ganti dengan aset asli. Setiap gambar wajib punya **alt-text**.

**Struktur folder:**
```
/public/assets/
  brand/      (logo, wordmark, favicon, og)
  profile/    (foto diri)
  projects/   (thumbnail & mockup per proyek)
  illustration/ (ilustrasi & tekstur footer)
  icons/      (ikon sosial bila custom)
  docs/       (CV/Resume PDF)
/fonts/        (file font self-host)
```

**Tabel aset (lengkapi & unggah di Pendev):**
| Key aset | Path | Format | Ukuran/Rasio | Alt-text (ID/EN) | Status |
|---|---|---|---|---|---|
| Logo/Wordmark | `brand/wordmark.svg` | SVG | tinggi ~32px | "{{HANDLE}} logo" | placeholder |
| Favicon | `brand/favicon.svg` (+ico 48px) | SVG/ICO | 48×48 | — | placeholder |
| OG Image | `brand/og-image.png` | PNG/WebP | 1200×630 | "Portofolio {{NAMA}}" | placeholder |
| Foto profil (hero) | `profile/portrait.webp` | WebP | 4:5, ≥1000px | "Foto {{NAMA}}" | placeholder |
| Foto about | `profile/about.webp` | WebP | 1:1 | "{{NAMA}} sedang bekerja" | placeholder |
| Thumbnail proyek 1..n | `projects/{{slug}}-thumb.webp` | WebP | 16:10, ≥1200px | "Pratinjau {{PROJEK_n}}" | placeholder |
| Mockup detail proyek | `projects/{{slug}}-mockup.webp` | WebP | 16:9 | "Tangkapan layar {{PROJEK_n}}" | placeholder |
| Ilustrasi footer | `illustration/footer-art.svg` | SVG | lebar-penuh | "Ilustrasi penutup" | placeholder |
| Tekstur/grain | `illustration/grain.png` | PNG | tileable | — (dekoratif) | opsional |
| Ikon sosial (jika custom) | `icons/{github,linkedin,instagram,x}.svg` | SVG | 24×24 | nama platform | pakai lucide default |
| CV / Resume | `docs/{{NAMA}}-CV.pdf` | PDF | A4 | — | placeholder |
| Font Display | `/fonts/{{display}}.woff2` | WOFF2 | — | — | placeholder |
| Font Body | `/fonts/{{body}}.woff2` | WOFF2 | — | — | placeholder |
| Font Mono | `/fonts/{{mono}}.woff2` | WOFF2 | — | — | placeholder |

**Konvensi:** nama file `kebab-case`, slug proyek konsisten dengan data; sediakan versi `@1x`/`@2x` bila perlu; semua foto diekspor WebP/AVIF; ikon & logo SVG; tulis `alt` di data, bukan hardcode.

## 8. Konten Placeholder (lengkapi di Pendev)
```
{{NAMA}}            = Didik ...
{{HANDLE}}          = didik.
{{TAHUN}}           = 2026
{{ROLE_TAGLINE_ID}} = "Saya membangun aplikasi web end-to-end dan mengotomasi pekerjaan berulang."
{{ROLE_TAGLINE_EN}} = "I build end-to-end web apps and automate repetitive work."
{{BIO_ID}} / {{BIO_EN}} = 2–3 kalimat tentang kamu, fokus & nilai.
{{ROLE_NOW}}        = posisi/kesibukan sekarang ; {{LOKASI}} = kota, negara
{{SKILL_LANG}}      = [JavaScript, TypeScript, PHP, Python, ...]
{{SKILL_FRAMEWORK}} = [React, Next.js, Laravel, Node.js, Tailwind, ...]
{{SKILL_TOOLS}}     = [PostgreSQL, MySQL, Supabase, Git, Docker, Vercel, ...]
{{PROJEK_n}}        = { nama, slug, deskripsi_id, deskripsi_en, tags[], demo_url, repo_url, hasil/metrik }
{{EXP_n}}           = { posisi, tempat, periode, ringkas_id, ringkas_en }
{{EDU_n}}           = { gelar/jurusan, kampus, periode }
{{EMAIL}} = didik...@... ; {{WA}} = +62... ; {{GITHUB}} ; {{LINKEDIN}} ; {{INSTAGRAM}} ; {{X}}
{{CTA_HEADLINE_ID}} = "Punya proyek? Mari wujudkan." ; {{CTA_HEADLINE_EN}} = "Got a project? Let's build."
```

## 9. Kriteria Selesai (acceptance)
- Semua section Bagian 3 ada, **responsif sempurna** di mobile/tablet/desktop, dan **bilingual** (toggle ID/EN mengubah seluruh copy + atribut `lang`).
- **Design system diterapkan konsisten** via tokens (warna, tipografi, spasi, radius) + **dark/light toggle** berfungsi & tersimpan.
- Hero tipografi besar memakai `clamp()`; footer "besar" dengan CTA kontak + wordmark + ilustrasi orisinal.
- Featured Projects tampil dengan kartu + tag + link (+ detail case study bila diaktifkan); hover/motion halus & `prefers-reduced-motion` dihormati.
- **Aset mengikuti manifest** (folder, penamaan, alt-text); semua masih placeholder jelas yang mudah diganti.
- SEO (meta/OG/sitemap/schema Person) & performa baik; aksesibilitas AA.
- Desain **orisinal** (tidak menyalin referensi) — hanya mengambil semangat editorial/bold/footer kuat.

## 10. Urutan Pengerjaan
1. Setup proyek + **design tokens & tema (dark/light)** + font + grid responsif.
2. **Komponen dasar** (Button, Nav+toggle bahasa/tema, Tag, Card, Input, Timeline, Footer).
3. **Header + Hero** (bilingual, clamp typography) → **About** → **Tech Stack** → **Featured Projects** → **Experience** → **Footer besar**.
4. Opsional: Command Palette/Chatbot, halaman detail proyek.
5. Isi placeholder + aset sesuai manifest → SEO/OG/sitemap → uji responsif (360/768/1280) & Lighthouse → selesai.
```
```
