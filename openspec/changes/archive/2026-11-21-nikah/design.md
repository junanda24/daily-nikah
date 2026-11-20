# Design — NIKAH! Rencana Nikah

## Direction contract (impeccable, code-led — diputuskan mandiri karena run detached, tanpa decision page)
- **THESIS:** Undangan pernikahan Jawa sebagai alat kerja, bukan kartu ucapan. Halaman ini adalah "undangan yang bisa dihitung": dunia visual undangan (maroon dalam, emas foil, kertas krem, motif kawung) dipakai untuk tugas operate — merencanakan budget. Menolak default kategori: kalkulator putih polos dengan kartu-kartu seragam.
- **OWN-WORLD:** Maroon pekat #6B1F2A sebagai lapangan (hero, tab bar, status), emas #C9A227 sebagai garis & angka penting, kertas krem #FAF5EC sebagai ground. Huruf ukir kapital Cinzel untuk judul, script Great Vibes untuk aksen nama, Manrope untuk isi & angka tabular. Motif kawung SVG prosedural (digambar sendiri) sebagai tekstur halus di hero & footer. Tanpa gradient dekoratif, tanpa kicker/eyebrow, tanpa kartu ikon generik.
- **STORY:** Pasangan membuka, langsung melihat "berapa totalnya & cukup tidak" dalam satu viewport, lalu turun ke rincian, rencana nabung, dan checklist. Percaya karena angka berlabel sumber & asumsi.
- **FIRST VIEWPORT:** Hero maroon: "NIKAH!" ukir emas, tanggal + countdown ringkas, kartu kertas krem berisi total estimasi besar + status Cukup/Mepet/Kurang + sisa/kurang rupiah. Di bawahnya: 3 preset sekali ketuk. Tab bar bawah (Rencana/Nabung/Checklist/Hari-H).
- **FORM:** Single-page app mobile-first, kolom 480px di tengah, bottom tab bar. Seed: n/a (code-led, tanpa concept-seed — run scheduled tanpa user).
- **FINISH:** unreviewed and undocumented is unfinished; this build ends with the finish review, the verdict, DESIGN.md, and every shipping raster carrying its provenance.

## Stack
Static artifact: `index.html` + `styles.css` + `app.js` (pola ARCHITECTURE.md §1: satu objek state, data terpisah dari logic, render() murni, event handler tipis, satu modul store untuk localStorage, IIFE scope). Tanpa framework, tanpa build step. Font via Google Fonts CDN (Cinzel, Great Vibes, Manrope). Confetti: canvas prosedural sendiri (tanpa library).

## State — lima keranjang (ARCHITECTURE.md)
- **Lokal:** semua state aplikasi (inputs, tier per pos, edit manual, tabungan, checklist, tab aktif) — satu objek `state`, persist localStorage key `nikah-state-v1`.
- **URL:** tidak dipakai (bukan shareable state).
- **Server state:** tidak ada (tanpa backend).
- **Global client UI:** tab aktif + toast — di state yang sama (app kecil, satu store sah).
- **Form:** input terkontrol via event handler tipis → update state → render().

## Data harga (estimasi 2026, riset 2026-11-21)
Sumber: undaku.id, duid.tech, kupinang.id, weddingmarket.com, chubb.com. Default tier Hemat/Standar/Mewah:
| Pos | Hemat | Standar | Mewah | Cara hitung |
|---|---|---|---|---|
| Venue | 3.000.000 | 12.000.000 | 60.000.000 | flat |
| Catering | 50.000/pax | 85.000/pax | 150.000/pax | × tamu × 1,1 |
| Dekorasi | 4.000.000 | 12.000.000 | 30.000.000 | flat |
| Dokumentasi | 2.500.000 | 10.000.000 | 25.000.000 | flat |
| Busana & MUA | 3.500.000 | 10.000.000 | 25.000.000 | flat |
| Undangan & souvenir | 1.500.000 | 5.000.000 | 12.000.000 | flat |
| Hiburan & MC | 1.500.000 | 5.000.000 | 15.000.000 | flat |
| Administrasi & KUA | 600.000 | 1.000.000 | 2.000.000 | flat |
| Mahar & seserahan | 3.000.000 | 8.000.000 | 20.000.000 | flat |
| Wedding organizer | 0 | 15.000.000 | 30.000.000 | toggle, default OFF |
| Dana cadangan | 10% subtotal | | | toggle, default ON |
| Inflasi vendor | 6%/tahun pro-rata | | | toggle, default ON |

## Animasi & delight
- Angka total beranimasi menghitung (count-up) saat berubah.
- Confetti canvas sekali saat status berubah ke "Cukup" dan saat checklist 100%.
- Cincin progres checklist beranimasi; countdown berdetak tiap detik.
- Transisi tab: fade+geser halus (200ms, ease-out eksponensial).

## Struktur file
```
index.html   # struktur + mounting point + tab bar
styles.css   # token :root → komponen → responsive
app.js       # DATA (harga, checklist, tips) → STATE → render() → EVENTS → INIT
```
