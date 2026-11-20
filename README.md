# NIKAH! — Rencana Nikah

Perencana pernikahan lengkap dalam satu halaman HP: estimasi budget per pos,
rencana nabung bulanan sampai hari-H, hitung mundur live + weton tanggal nikah,
dan checklist persiapan 24 tugas. Semua tersimpan di HP (localStorage) — tanpa
login, tanpa server, tanpa biaya.

> **Project harian "1 Hari 1 Project" — Sabtu, 21 November 2026.**
> Repo: https://github.com/junanda24/daily-nikah

## Kenapa ide ini dipilih

Orang pikir "kalkulator nikah" itu satu angka. NIKAH! membalik arah: **masukkan
budgetmu, aplikasinya yang bilang pestamu muat berapa tamu, kurang berapa, dan
harus nabung berapa per bulan** — plus tanggal nikahnya dicek wetonnya.

Data harga bukan karangan: riset dari undaku.id, duid.tech, kupinang.id,
weddingmarket.com, dan chubb.com (skala 2026: intimate 50–100 tamu Rp 25–75 jt;
sedang 200–300 tamu Rp 60–200 jt; besar 500+ tamu Rp 160 jt ke atas; catering
Rp 35–150 ribu/pax). Setiap angka dilabeli "Estimasi 2026 — kisaran pasar, cek
ke vendor". Weton dihitung deterministik dari anchor 1 Jan 1970 = Kamis Wage
(terverifikasi silang dengan 17 Agustus 1945 = Jumat Legi), bukan ditebak.

Bukan duplikat KondanganKu (project 12 Nov): itu mencatat uang tamu *setelah*
nikah; ini merencanakan budget *sebelum* nikah. Saling melengkapi.

## Fitur

- **Rencana (budget planner)** — 10 pos biaya (venue, catering, dekorasi,
  dokumentasi, busana & MUA, undangan & souvenir, hiburan & MC, administrasi &
  KUA, mahar & seserahan, wedding organizer), masing-masing 3 tier
  Hemat/Standar/Mewah + nominal manual + toggle on/off. Catering dihitung
  `tamu × harga/pax × 1,1` (cadangan porsi 10%). Dana cadangan 10% dan inflasi
  vendor 6%/tahun pro-rata sampai hari-H sebagai baris asumsi yang bisa
  dimatikan. Status **Cukup / Mepet / Kurang** dengan sisa/kekurangan rupiah
  dan saran pangkas dari pos terbesar. Breakdown per pos (bar + %), biaya per
  tamu, dan 3 preset sekali ketuk: Intimate (100 tamu), Standar (300 tamu),
  Grand (500 tamu).
- **Nabung** — target hari-H, tabungan sekarang, bulan tersisa, dan cicilan
  nabung per bulan. Menangani tabungan yang sudah cukup dan tanggal yang sudah
  lewat tanpa angka aneh.
- **Hari-H** — countdown live per detik + weton tanggal nikah (hari + pasaran +
  total neptu) dengan label tradisi Primbon Jawa.
- **Checklist** — 24 tugas dalam 5 fase (12–9 bulan, 6–3 bulan, 1 bulan,
  1 minggu, Hari H) dengan cincin progres dan confetti saat 100%.
- **Tips hemat dinamis** — 3 tips berdasarkan 3 pos biaya terbesarmu saat ini.
- **Delight** — angka total count-up, confetti saat status jadi "Cukup" dan
  saat checklist 100%, transisi tab halus.
- **Persistensi** — semua input, tier, dan centang tersimpan di localStorage
  dan pulih saat dibuka lagi.

## Cara pakai

1. Buka aplikasinya di HP.
2. Tab **Rencana**: isi tanggal nikah, jumlah tamu, dan budget. Pilih tier
   tiap pos atau ketik nominal sendiri. Coba preset Intimate / Standar / Grand.
3. Tab **Nabung**: isi tabungan sekarang — lihat berapa yang harus disisihkan
   tiap bulan.
4. Tab **Checklist**: centang tugas yang sudah beres, kejar 100%.
5. Tab **Hari-H**: lihat hitung mundur dan weton tanggal nikahmu.

## Cara menjalankan dari source

Tidak ada build step. Buka `src/index.html` langsung di browser, atau sajikan
dengan server statis apa pun:

```bash
cd src
python3 -m http.server 8000
# buka http://localhost:8000
```

## Tech stack

- HTML + CSS + JavaScript murni (tanpa framework, tanpa build step)
- Google Fonts: Cinzel (judul ukir), Great Vibes (aksen script), Manrope (isi)
- Motif kawung SVG prosedural (digambar sendiri, tanpa aset pihak ketiga)
- localStorage untuk persistensi; canvas prosedural untuk confetti

## Struktur folder

```
.
├── README.md
├── src/
│   └── index.html        # aplikasi lengkap (single-file)
└── openspec/
    └── changes/
        └── archive/
            └── 2026-11-21-nikah/
                ├── proposal.md
                ├── design.md
                ├── tasks.md
                └── specs/
                    └── nikah/
                        └── spec.md
```

## Link hasil

- Aplikasi (artifact): `nikah-rencana-nikah` (card widget
  `web-artifact-build-completed-0e90657c-96c5-42dc-9c24-a084835b9232`)
- Repo: https://github.com/junanda24/daily-nikah
- Rilis: 2026-11-21

## Catatan / temuan saat build

- Harga default = estimasi kisaran pasar 2026 dari riset (bukan penawaran
  vendor). Buffer 10% dan inflasi vendor 6%/tahun adalah asumsi ilustrasi
  yang dilabeli jelas dan bisa dimatikan user.
- Weton/neptu = tradisi Primbon Jawa (komputasi kalender deterministik),
  dilabeli sebagai tradisi, bukan jaminan.
- Tidak ada backend: semua logika deterministik dan client-side. Sengaja
  tidak dibuat fullstack — tidak ada data yang butuh server.
- Verifikasi: audit builder (Playwright headless, 0 console error, 0 overflow
  di 390px) + smoke test jsdom mandiri 14/14 PASS (preset, tier, toggle,
  nominal manual, countdown, weton Sabtu Pon neptu 16 untuk 5 Jun 2027,
  checklist 24 tugas → 13% setelah 3 centang, persistensi reload).
- Perbaikan setelah audit: toggle switch diganti ke `appearance-none` yang
  terlihat; tab bar diubah dari fixed-overlay ke app-shell flex agar tidak
  menutup kontrol; fungsi confetti diberi guard `if (!ctx) return` agar
  tidak melempar TypeError di environment tanpa canvas 2D.
- Yang sengaja tidak dibuat: ekspor PDF ringkasan, pengingat notifikasi, dan
  multi-bahasa — di luar scope satu sesi; state sudah lengkap di localStorage
  sehingga mudah ditambah nanti.
