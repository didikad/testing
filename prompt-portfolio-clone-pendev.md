# Prompt Pendev — Replika Persis Portofolio dari Video Referensi (Dark Monokrom Editorial)

> **Cara pakai:** Salin seluruh isi di bawah garis ini, tempel ke Pendev. Hasil harus **sevisual mungkin sama dengan video referensi**. Ganti field identitas (`{{...}}`) dengan datamu — default sudah diisi contoh agar hasil langsung mirip video. Website wajib **responsif penuh (mobile/tablet/desktop)**.
>
> **Catatan aset:** foto wajah & ilustrasi kerumunan orang pada video adalah aset pribadi/berlisensi. Jangan menyalin file aslinya — **buat padanan orisinal dengan gaya yang sama** (foto potret B&W-mu sendiri; ilustrasi line-art kerumunan orang baru). Tampilan akhir tetap identik.

---

Bangunkan sebuah **website portofolio personal satu halaman (one-page scroll) untuk Software Engineer / Full-Stack Developer** yang **MEREPLIKASI PERSIS** gaya, tata letak, tipografi, warna, section, dan interaksi berikut. Ini adalah **clone desain** — ikuti spesifikasi seketat mungkin.

## 0. GAYA VISUAL (wajib sama)
- **Tema gelap monokrom**: latar **near-black `#0A0A0A`/`#000`**, teks **putih `#FFFFFF`**, abu untuk teks sekunder. **Nyaris tanpa warna** — aksen hanya hitam/putih/abu. (Sediakan juga mode terang via toggle, latar krem/putih.)
- **Tipografi**:
  - **Display/Headline**: grotesk sangat tebal & sedikit kondensa — gunakan **"Anton"** atau **"Archivo Expanded/Black"** / **"Space Grotesk" Bold** untuk judul raksasa (mis. hero `< SOFTWARE ENGINEER />`). Uppercase, tracking rapat, line-height ~0.9.
  - **Body/UI**: sans bersih — **"Inter"** atau **"Geist"**.
  - **Monospace (label meta)**: **"JetBrains Mono"** / **"Geist Mono"** untuk label kecil seperti `©2026`, `{{ AI & FULL-STACK DEVELOPMENT }}`, `< />`, nama tag.
- **Layout**: banyak **ruang kosong**, **garis pemisah tipis** (1px, abu gelap), **grid rapi**, section dipisah label mono kecil di kiri atas.
- **Header sticky** tipis; ada **toggle tema (ikon matahari/bulan)** dan menu "**...**".
- **Micro-labels** gaya teknis di mana-mana (uppercase mono, dengan simbol `©`, `{{ }}`, `< />`, `↗`).
- Kesan keseluruhan: **editorial, brutalis-rapi, percaya diri, "developer banget"**.

### Design tokens (pakai persis)
```css
:root{ /* DARK (default) */
  --bg:#0A0A0A; --surface:#111111; --surface-2:#171717; --border:#242424;
  --text:#FFFFFF; --text-muted:#9A9A9A; --text-dim:#6B6B6B;
  --hair:#1E1E1E; /* garis */ --focus:#FFFFFF;
}
:root[data-theme="light"]{
  --bg:#F5F4F0; --surface:#FFFFFF; --surface-2:#ECEBE6; --border:#DCDBD5;
  --text:#0A0A0A; --text-muted:#5A5A5A; --text-dim:#8A8A8A; --hair:#E2E1DB; --focus:#0A0A0A;
}
/* Tipografi */
--font-display:"Anton","Archivo",sans-serif; --font-body:"Inter",sans-serif; --font-mono:"JetBrains Mono",monospace;
/* Spasi 8pt: 4 8 12 16 24 32 48 64 96 128 160 ; radius: sm6 md10 lg16 pill999 */
```
Skala hero: `clamp(44px, 12vw, 160px)`. H2 `clamp(28px,5vw,56px)`. Body 16–18. Mono label 11–13 uppercase, letter-spacing .08em.

## 1. SECTION & KONTEN (urut persis seperti video)

### 1.1 Header (sticky, tipis)
Kiri: wordmark **"{{HANDLE}}"** (default `Aswin.`). Kanan: tombol **Explore** (buka command/search), **Get in touch**, tampilan **email**, **toggle tema**, menu **"..."**. Di mobile → ringkas jadi wordmark + tombol menu.

### 1.2 Hero
- Label mono kiri-atas: **`©{{TAHUN}}`** (default `©2026`).
- Headline raksasa center/again: **`< SOFTWARE ENGINEER />`** (grotesk tebal, putih, pakai tanda `<` `/>` literal).
- Label mono kanan-bawah headline: **`{{ {{FOKUS}} }}`** (default `{{ AI & FULL-STACK DEVELOPMENT }}`).
- **Foto potret B&W** ({{FOTO_HERO}}) ditempatkan tumpang-tindih dengan teks (grayscale).
- Indikator scroll halus.

### 1.3 About — "Hi, I'm {{NAMA}}."
- Judul besar **"Hi, I'm {{NAMA}}."** (default `Aswin`).
- Subjudul: **"{{PERAN}}"** (default `AI Engineer & Full-Stack Developer.`).
- Paragraf: **"{{BIO}}"** (default `I build RAG pipelines and automate repetitive workflows, saving hours of manual work.`).
- Tombol **"Explore projects"**.
- Kartu foto ({{FOTO_ABOUT}}, B&W) + meta mono: **"{{PERUSAHAAN}} · {{JABATAN}} · {{LOKASI}}"** (default `JAKS & Associates · Software Developer & AI Intern · Kochi, India`).

### 1.4 Tech Stack — label kecil "The tools behind my work."
Tiga kolom, tiap kolom: judul + subjudul abu + deretan **tag/pill** (border tipis, mono). Isi **default (ganti sesuai dirimu)**:
- **AI & Machine Learning** — *RAG Pipelines, Embeddings & Semantic Search, Evaluation*: `LLMs` `Generative AI` `RAG` `Agentic Workflows` `LangChain` `LangGraph` `Prompt Engineering` `Sentence Transformers` `RAGAS`.
- **Languages & Frameworks** — *REST API Design, LLM Integration, Full-Stack Builds*: `Python` `TypeScript` `FastAPI` `Django` `React` `Next.js` `Tailwind CSS` `RESTful APIs`.
- **Tools, Databases & Cloud** — *Predictive Modeling, Data Processing, Deployment*: `PostgreSQL` `SQL` `Qdrant` `ChromaDB` `Pandas` `NumPy` `Scikit-learn` `Docker` `Git & GitHub` `Playwright` `Cloudflare` `Vercel`.

### 1.5 Featured Projects
Label + deskripsi: **"Independent projects and professional work. Open a folder to explore a project or case study."**
Tampilkan sebagai **kartu "folder"** dengan **mockup browser** kecil; tiap kartu: nama proyek, tag teknologi, tombol **"Read case study"**, link Demo/Repo. Default 4 proyek (ganti): **Workflow Automation**, **SmartOps**, **ResumeLens**, **CRIS**. Interaksi: klik folder → buka detail/case study (masalah → solusi → peran → hasil).

### 1.6 Experience (timeline berbentuk kurva/garis)
Judul **"Experience."**; render **timeline** (kurva garis di desktop, vertikal di mobile) dengan titik-titik. Default entri (ganti):
- **Software Developer & AI Intern** — JAKS & Associates, Kochi — *Ongoing* — "Working in software development and AI as an intern."
- **Freelance Web Developer** — Client projects — "Built and delivered websites for clients."
- **Master of Computer Applications** — Pondicherry University — "Graduated April 2026 / GPA 7.3".
- **Data Science Intern** — AI Variant, Remote — *Sep 2023 – Mar 2024* — "Completed a six-month data science internship."
- **Bachelor of Computer Applications** — Calicut University — "GPA 6.5".

### 1.7 Contact — "Let's talk."
- Judul besar **"Let's talk."**
- Subteks: **"Whether it's a full-time role or a freelance project, my inbox is open."**
- **Email** {{EMAIL}} (default `aswinpanengal@gmail.com`) + tombol **copy**.
- Tautan sosial: **LinkedIn · GitHub · Instagram · Upwork**.
- **Form**: *Your name* (placeholder "What should I call you?"), *Email address* (placeholder "you@company.com"), *What do you have in mind?* (placeholder "A little about your opportunity or project...") + tombol **"Create email draft ↗"** yang **menyusun email `mailto:` prefilled** dari isian form.

### 1.8 Footer — "the main character" (besar & berkesan)
- **Mini-nav**: About · Skills · Projects · Experience · Freelance · World of {{NAMA}} · Contact.
- Baris email + sosial.
- **Wordmark RAKSASA "{{NAMA_UPPER}}"** (default `ASWIN`) sebagai elemen grafis — outline/semi-transparan, memenuhi lebar.
- **Ilustrasi line-art kerumunan orang** (buat orisinal, gaya mono) sebagai band di bawah wordmark.
- Baris penutup: **"See you around."**
- Legal: **"©{{TAHUN}} {{NAMA_LENGKAP}}"** + tombol **"Back to top"**.

### 1.9 Floating — AI Assistant
Widget chat mengambang **"{{NAMA}}'s AI Assistant"** (default `Aswin's AI Assistant`): bisa jawab pertanyaan singkat tentang pemilik (skill, proyek, kontak). Boleh pakai jawaban preset bila tanpa backend. Opsional: **Command Palette ⌘K** untuk lompat antar-section.

## 2. INTERAKSI & MOTION (tiru nuansanya)
- Animasi masuk section: **fade + translate-y** dengan **stagger**; easing ease-out ekspresif (`cubic-bezier(.22,1,.36,1)`), 300–500ms.
- Hover kartu proyek: angkat + garis/aksen; folder "membuka".
- **Marquee** lambat pada wordmark/tag.
- **Toggle tema** (simpan di localStorage, hormati `prefers-color-scheme`).
- Smooth-scroll + "Back to top".
- Hormati **`prefers-reduced-motion`**.

## 3. TECH STACK PEMBANGUNAN
- **Next.js (App Router) + TypeScript**, **Tailwind CSS** dengan tokens di atas, **Framer Motion**, ikon **lucide-react**.
- Font self-host via `next/font` (Anton/Archivo + Inter + JetBrains Mono).
- Gambar via `next/image` (AVIF/WebP). Form kontak → `mailto:` prefilled (atau API route + Resend opsional).
- SEO: meta + Open Graph + sitemap + schema.org `Person`. Target Lighthouse ≥95.

## 4. RESPONSIF (wajib, uji di 3 ukuran)
- **Mobile ≤640**: 1 kolom; headline hero pakai `clamp()` agar muat; tech stack & projects menumpuk; nav → menu overlay; wordmark footer tetap besar tapi tidak overflow (sembunyikan luapan).
- **Tablet 641–1024**: 2 kolom untuk tech stack/projects.
- **Desktop >1024**: layout penuh seperti video (3 kolom tech stack, timeline kurva, hero besar).
- Tidak boleh ada **scroll horizontal** atau elemen terpotong.

## 5. MANIFEST ASET (simpan di `/public/assets/`)
| Aset | Path | Format | Catatan |
|---|---|---|---|
| Foto hero (B&W) | `profile/hero.webp` | WebP 4:5 | fotomu sendiri, filter grayscale |
| Foto about | `profile/about.webp` | WebP 1:1 | grayscale |
| Thumbnail proyek ×4 | `projects/{slug}.webp` | WebP 16:10 | mockup browser |
| Ilustrasi kerumunan (footer) | `illustration/crowd.svg` | SVG | **buat orisinal** line-art mono, JANGAN salin dari video |
| Favicon | `brand/favicon.svg` | SVG | inisial |
| OG image | `brand/og.png` | 1200×630 | judul + nama |
| Fonts | `/fonts/*.woff2` | WOFF2 | Anton/Archivo, Inter, JetBrains Mono |
| CV | `docs/{{NAMA}}-CV.pdf` | PDF | opsional |

## 6. FIELD IDENTITAS (ganti; default = seperti video)
```
{{NAMA}}=Aswin  {{NAMA_UPPER}}=ASWIN  {{NAMA_LENGKAP}}=Aswin Panengal  {{HANDLE}}=Aswin.
{{TAHUN}}=2026  {{PERAN}}=AI Engineer & Full-Stack Developer.
{{FOKUS}}=AI & FULL-STACK DEVELOPMENT
{{BIO}}=I build RAG pipelines and automate repetitive workflows, saving hours of manual work.
{{PERUSAHAAN}}=JAKS & Associates  {{JABATAN}}=Software Developer & AI Intern  {{LOKASI}}=Kochi, India
{{EMAIL}}=aswinpanengal@gmail.com  {{GITHUB}}=  {{LINKEDIN}}=  {{INSTAGRAM}}=  {{UPWORK}}=
Projects: Workflow Automation, SmartOps, ResumeLens, CRIS (ganti dengan proyekmu)
```
> Untuk menjadikannya portofoliomu: cukup ubah nilai di atas + unggah aset sesuai manifest. Struktur, gaya, dan layout tetap identik dengan video.

## 7. KRITERIA SELESAI
- Tampilan **sepersis mungkin dengan video**: dark monokrom, hero `< SOFTWARE ENGINEER />` grotesk raksasa, label mono, tech stack 3 kolom dengan tag, featured projects folder, experience timeline, "Let's talk" + **Create email draft**, footer wordmark raksasa + ilustrasi kerumunan + "See you around", AI assistant mengambang, toggle tema.
- **Responsif** sempurna di mobile/tablet/desktop; motion halus; `prefers-reduced-motion` dihormati.
- Aset mengikuti manifest (ilustrasi & foto **orisinal**, bukan salinan dari video). SEO & performa baik.

## 8. URUTAN PENGERJAAN
Tokens & tema → font → komponen (Nav, Button, Tag, FolderCard, Timeline, Input, Footer, ThemeToggle, AIAssistant) → Hero → About → Tech Stack → Featured Projects → Experience → Let's talk → Footer → AI assistant/⌘K → isi konten & aset → SEO → uji responsif (360/768/1280) & Lighthouse.
