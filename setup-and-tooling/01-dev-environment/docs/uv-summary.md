Paham banget. Kamu mau **peta workflow praktis** + **bedah istilah-istilah yang selama ini cuma lewat di kepala** (PyPI, dependency, lock, dll.). Aku susun berurutan, dari "wajib hafal" sampai "opsional".

---

## Bagian 1: Istilah yang kamu bilang "belum dalam" — aku bedah dulu

Ini penting dibersihkan dulu, karena semua workflow nanti pakai istilah ini.

**PyPI** = *Python Package Index*. Bayangkan **Google Play Store untuk Python**. Server di internet tempat semua package Python disimpan. Ketika kamu `uv pip install numpy`, uv pergi ke PyPI, cari package bernama `numpy`, unduh, pasang. Itu saja — PyPI hanyalah "toko online"-nya.

**Dependency** = **package lain yang dibutuhkan** sebuah package. Contoh: kamu install `matplotlib`, tapi matplotlib di dalamnya butuh `numpy`, `pillow`, `fonttools`, dll. Jadi `numpy` adalah *dependency* dari `matplotlib`. Saat install `matplotlib`, uv otomatis ikut memasang semua dependency-nya — kamu tidak perlu menyebutkannya satu per satu.

**Version pinning / lock** = "mengunci" versi persis supaya semua orang pakai versi yang sama. Analogi: kamu dan teman bikin project. Hari ini kamu install `numpy`, kebetulan dapat versi `2.1.0`. Tiga bulan kemudian temanmu install project yang sama, tapi PyPI sudah rilis `numpy 3.0` yang mengubah banyak hal → project jadi error. **Lock** menyimpan daftar *versi persis* yang sudah teruji jalan, supaya temanmu dapat `numpy 2.1.0` yang sama persis, bukan versi terbaru. File lock di uv bernama **`uv.lock`**.

**`pyproject.toml`** = file "kartu identitas" project. Berisi: nama project, versi Python yang dibutuhkan, dan daftar package yang dipakai. Ini yang kamu tulis (deklarasi *ingin apa*).

**`uv.lock`** = hasil "pembekuan" dari `pyproject.toml`. Berisi versi **persis** setiap package + semua dependency-nya (yang dihitung otomatis). Ini yang menjamin reproducible. Kamu **tidak menulisnya manual** — uv yang generate.

---

## Bagian 2: Workflow WAJIB (cukup 4 perintah, ini yang harus hafal)

Ini pola yang kamu pakai di **hampir semua project** kursus ini. Hafalkan alurnya:

```bash
# 1. Bikin virtual environment (sekali per project)
uv venv

# 2. Aktifkan (SETIAP kali buka terminal baru)
#    Linux/macOS/WSL2:
source .venv/bin/activate
#    Windows PowerShell:
.venv\Scripts\activate

# 3. Install package yang kamu butuh
uv pip install numpy matplotlib jupyter

# 4. Selesai kerja, matikan environment
deactivate
```

**Catatan penting soal step 2:** `activate` **tidak permanen**. Begitu kamu tutup terminal dan buka lagi, kamu harus `activate` lagi. Ini sumber error paling umum: *"sudah install kok import error?"* → hampir selalu karena lupa `activate`, jadi `python` yang kepanggil adalah Python sistem, bukan Python venv.

---

## Bagian 3: Workflow "project yang benar" (level lebih rapi, pakai pyproject + lock)

Kalau kamu mau project yang bisa dibagikan & reproducible (sesuai tujuan GitHub pribadimu), gunakan pola **dua file** ini. Ini yang membedakan "asal install" vs "project serius":

```bash
# Inisialisasi project baru (membuat pyproject.toml)
uv init nama-project
cd nama-project

# Tambah package (otomatis dicatat di pyproject.toml + update uv.lock)
uv add numpy matplotlib

# Jalankan script
uv run python main.py
```

Apa yang terjadi di balik `uv add numpy`:
1. uv tulis `numpy` ke `pyproject.toml` (deklarasi: "project ini butuh numpy")
2. uv hitung versi yang cocok + semua dependency → tulis hasilnya ke `uv.lock`
3. uv pasang package-nya

**Kapan pakai pola ini vs pola wajib?**
- Pola wajib (`uv pip install`) → cepat, untuk eksperimen/nyoba-nyoba.
- Pola `uv add` + `pyproject` → untuk project yang mau kamu simpan di GitHub dan bagikan.

Untuk **kursus ini**, repo-nya sudah punya struktur sendiri, jadi kamu kebanyakan pakai pola wajib. Tapi karena kamu mau bikin catatan di GitHub pribadi, pola `uv add` ini worth dipelajari.

---

## Bagian 4: Peta keputusan "kapan pakai apa"

```
Mulai kerja di project
   │
   ├─ Baru pertama kali / belum ada .venv?
   │     → uv venv
   │
   ├─ Buka terminal baru (lanjut kerja)?
   │     → source .venv/bin/activate   (WAJIB tiap sesi)
   │
   ├─ Mau install package tambahan?
   │     → uv pip install nama-package
   │
   ├─ Mau lihat apa saja yang sudah terinstall?
   │     → uv pip list
   │
   ├─ Project mau dibagikan di GitHub?
   │     → pakai uv init + uv add (bukan pip install)
   │
   └─ Selesai?
         → deactivate
```

---

## Bagian 5: Perintah lain yang sering kepakai (opsional, tahu saja)

```bash
uv pip list                    # lihat daftar package di venv ini
uv pip show numpy              # detail satu package (versi, lokasi)
uv python list                 # lihat semua versi Python yang uv punya
uv venv --python 3.12          # bikin venv dengan versi Python spesifik
uv pip install -r requirements.txt   # install dari daftar file
```

---

## Rangkuman efektif (3 hal yang harus kamu ingat)

1. **PyPI** = toko package online. **Dependency** = package yang dibutuhkan package lain. **Lock** = mengunci versi persis supaya reproducible.

2. **Pola wajib hafal:** `uv venv` → `activate` → `uv pip install` → `deactivate`. Ingat: **activate ulang setiap buka terminal baru**.

3. **Dua file project serius:** `pyproject.toml` (kamu deklarasikan *ingin apa*) → `uv.lock` (uv hitung *versi persis* otomatis). Kamu cuma nulis `pyproject`, sisanya uv yang urus.

---

Kalau kamu mau, aku bisa buatkan **satu file markdown ringkas** berisi cheat-sheet ini (istilah + workflow + tabel perintah) yang bisa langsung kamu taruh di GitHub pribadimu. Bilang saja.