# Proposal — NIKAH! Rencana Nikah

**Tanggal:** 2026-11-21 | **Slug:** `nikah` | **Bentuk:** web app (frontend-only, static artifact) | **Backend:** tidak

## Apa ini
NIKAH! adalah perencana pernikahan lengkap dalam satu halaman HP: **estimasi budget per pos** (venue, catering per pax, dekorasi, dokumentasi, busana+MUA, undangan & souvenir, hiburan, administrasi KUA, mahar, WO) dengan 3 tier harga, **rencana nabung bulanan** sampai hari-H (dengan buffer 10% + inflasi vendor 6%/tahun sebagai asumsi yang dilabeli jelas), **hitung mundur live + weton tanggal nikah** (pasaran & neptu, komputasi deterministik dari anchor 1970-01-01 = Kamis Wage, terverifikasi via 17 Agu 1945 = Jumat Legi), dan **checklist timeline** 24 tugas dari 12 bulan sampai hari-H. Semua tersimpan di localStorage.

## Kenapa ide ini mengejutkan
- Orang pikir "kalkulator nikah" = satu angka. Ini membalik arah: **masukkan budgetmu → aplikasinya bilang pestamu muat berapa tamu, kurang berapa, dan nabung berapa per bulan** — plus tanggalnya dicek wetonnya.
- Data harga BUKAN karangan: riset pagi ini dari undaku.id, duid.tech, kupinang.id, weddingmarket, chubb (skala 2026: intimate 50–100 tamu Rp 25–75 jt; sedang 200–300 tamu Rp 60–200 jt; besar 500+ tamu Rp 160 jt+; catering Rp 35–150rb/pax). Setiap angka dilabeli "estimasi 2026, verifikasi ke vendor".
- Weton dihitung, bukan ditebak: anchor epoch terverifikasi silang dengan Proklamasi.
- Bukan duplikat KondanganKu (12 Nov): itu mencatat uang tamu SETELAH nikah; ini merencanakan budget SEBELUM nikah. Saling melengkapi.

## Kenapa bentuk ini (web app, tanpa backend)
- Semua logika deterministik & client-side: hitung budget, nabung, weton, checklist. Tidak ada data yang butuh server, login, atau API berbayar. Backend hanya menambah biaya tanpa nilai.
- Dipakai pasangan di HP, kapan saja — artifact static langsung dibuka, state tersimpan lokal.

## Uji bar "receh"
Bukan kalkulator satu fungsi: 4 fitur saling nyambung (budget → nabung → countdown → checklist), state bertahan, alur end-to-end, ada keputusan yang dibantu (status cukup/mepet/kurang + tips pangkas dinamis). Selevel patokan (Sampai Gajian!, WARIS!), bukan kata-angka/Berani Resign. **LOLOS.**

## Anti-AI-slop
Copy Bahasa Indonesia natural, spesifik ("tiap 10 tamu ≈ Rp X"), tanpa kata-kata generik ("rencanakan pernikahan impianmu dengan mudah"). Angka selalu dengan konteks & sumber.

## IP check
Semua aset original: pola kawung digambar sebagai SVG prosedural, tanpa foto/stock pihak ketiga, tanpa karakter berlisensi. Tidak ada disclaimer fan-made yang diperlukan.

## Skill ledger (aturan build: analisis skill dulu)
- **Dipakai:** openspec-web-builder (protokol + ARCHITECTURE.md + CODE_STANDARDS.md), local-impeccable (arah visual + craft-floor; launcher `context` dijalankan; concept-seed/decision-page TIDAK dijalankan — run ini detached tanpa user, scheduler memberi otoritas penuh tanpa gate approval; arah diputuskan & dicatat di design.md sebagai direction contract, code-led), local-ui-ux-pro-max-skill (file-nya hanya catatan recovery kosong — tidak ada isi yang bisa diterapkan, dicatat jujur).
- **Diskip:** skill game (bukan game), skill npm/Flutter (bukan package), skill belanja/tiket/dll (tidak relevan).
- **Asumsi yang dilabeli:** harga = estimasi pasar 2026 dari riset (bukan penawaran vendor); buffer 10% & inflasi vendor 6%/tahun = asumsi ilustrasi yang bisa dimatikan user; weton/neptu = tradisi Primbon Jawa, bukan jaminan.
