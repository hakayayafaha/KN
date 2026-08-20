# Test Credentials — Kain Nusantara (WMS/ERP)

> Ditulis ulang tiap clone: berkas ini **di-.gitignore**, jadi kontainer baru selalu datang kosong.
> Semua akun berasal dari `python seed_realistic.py` (data demo). **Password sama untuk semua:**
> `demo12345`

| Peran | Email | Catatan |
|---|---|---|
| Admin | `admin@kainnusantara.id` | Budi Santoso — akses penuh (Pengaturan · Master · semua modul) |
| Manajer | `manager@kainnusantara.id` | Dewi Rahayu — persetujuan, laporan, **penyetuju permintaan desain** |
| Admin Sales | `salesadmin@kainnusantara.id` | Rina Kusumawati — Meja Admin Sales; **boleh membuat Permintaan Desain** |
| Finance | `finance@kainnusantara.id` | Hendra Wijaya — Meja Finance (uang masuk, pajak) |
| Sales | `sales@kainnusantara.id` | Ayu Permatasari (juga `sales2@`, `sales3@`) |
| Gudang | `warehouse@kainnusantara.id` | Eko Prasetyo (juga `warehouse2@`) |
| **Desainer (peran ke-7 · FASE D)** | **`designer@kainnusantara.id`** | **Sari Melati** — wilayah SENGAJA SEMPIT: papan Permintaan Desain (beranda perannya) + Desain & Pattern + Galeri Desain + Profil Saya. Tidak boleh membuat/menugaskan/ACC/minta-revisi. |
| Sales **berpagar lini printing** (FASE L) | `dewi.printing@kainnusantara.id` | `allowed_line_codes=["printing"]` — hanya melihat pekerjaan lini printing |
| Manajer warisan (uji "cek kenyataan peran") | `adminsales.lama@kainnusantara.id` | peran `manager` tetapi jejaknya Admin Sales |

Akun ber-home **CV Kanda Suka** adalah **`sales3@`** (bukan `sales2@`/`warehouse2@`
seperti tertulis di catatan lama).

## Catatan penting untuk agen uji
* Layar masuk: `data-testid="login-email-input"`, `login-password-input`,
  `login-submit-button` (lihat `frontend/src/components/LoginScreen.jsx`).
* Setelah masuk, **pilih badan usaha** dulu (PT Kain Suka Cita "KSC" / CV Kanda Suka).
  Mode "Semua Entitas" sengaja **hanya-lihat** — aksi tulis dijawab **409** dengan kalimat
  menuntun. Jalan tercepat: klik pita `data-testid="scope-pick-ent_ksc"`.
* **Navigasi BUKAN hash-routing.** Aplikasi ini TIDAK PERNAH memakai `#/view`; satu-satunya
  jalur URL adalah `/verify-document/:id`. Klik `nav-{id}` di sidebar (atau
  `nav-group-{groupId}` → `nav-{id}`), lalu tab hub `hub-tab-{view}`.
* **`KNSelect` merender placeholder SEBAGAI OPSI** (`{testId}-option-empty`, mis.
  "Pilih desainer"). Memilihnya **mengosongkan** pilihan sehingga tombol simpan mati.
  Selalu pakai testid kanonik **`{testId}-option-{value}`** — jangan `[role="option"]`
  generik. Pola ini sudah memproduksi satu laporan bug palsu (2026-08-20).
* Pop-up **alasan wajib** memakai `confirm-modal`: isi `confirm-modal-reason` lalu
  `confirm-modal-confirm`. Tombol itu **DISABLED selama alasan kosong** — DISENGAJA.
* `allowed_line_codes: []` berarti **SEMUA lini** (bukan "tidak boleh apa pun").
* Basis data uji: `test_database` (lihat `backend/.env`).
* **Pulihkan data demo**: `python seed_realistic.py` lalu `python seed_e9_chain_demo.py`.
* Pelanggan demo **"Toko Kain Sejahtera" TERBLOKIR KREDIT** — untuk uji pembuatan pesanan
  pakai "Butik Bali Indah" / "Fashion Bandung Kencana" / "Tekstil Medan Jaya".

## Keadaan awal FASE D (sesudah seed bersih)
`design_requests` **4 dokumen**: `KSC/DSR-00001` submitted (belum ditugaskan) ·
`KSC/DSR-00002` in_progress · `KSC/DSR-00003` delivered (menunggu keputusan) ·
`KSC/DSR-00004` approved — tiga terakhir ditugaskan ke **Sari Melati**.
`design_gallery` 2 artwork: `DSG-PARANG-01` approved · `DSG-PARANG-02` pending_approval.
Manajer melihat **4**, desainer hanya **3** (DSR-00001 belum ditugaskan kepadanya) —
selisih itu adalah **pagar kepemilikan yang bekerja**, bukan bug.

## Jangan diuji oleh agen otomatis
Drag-and-drop · unggah berkas fisik / kamera / scan RFID · suara.
Dan jangan melaporkan "NaN" dari pencarian **case-insensitive**: kata Indonesia ber-"nan"
(mis. "Pena**nan**ganan") sering tertangkap — cari `NaN` **case-sensitive**.
