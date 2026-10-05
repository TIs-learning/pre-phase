# Git & Collaboration

> Version control is not optional. Every experiment, every model, every lesson you build here gets tracked.

**Type:** Learn
**Languages:** --
**Prerequisites:** Phase 0, Lesson 01
**Time:** ~30 minutes

## Learning Objectives

- Configure git identity and use the daily workflow of add, commit, and push
- Create and merge branches for isolated experiments without breaking main
- Write a `.gitignore` that excludes model checkpoints and large binary files
- Navigate the commit history with `git log` to understand project evolution

## The Problem

You're about to write hundreds of code files across 20 phases. Without version control you will lose work, break things you can't undo, and have no way to collaborate with others.

Git is the tool. GitHub is where the code lives. This lesson covers what you need for this course and nothing more.

## The Concept

```mermaid
sequenceDiagram
    participant WD as Working Directory
    participant SA as Staging Area
    participant LR as Local Repo
    participant R as Remote (GitHub)
    WD->>SA: git add
    SA->>LR: git commit
    LR->>R: git push
    R->>LR: git fetch
    LR->>WD: git pull
```
### Penjelasan
**Tempat**
- Working Directory (WD)
Folder project kamu di VS Code. Segala perubahan di sini belum dicatat git sama sekali. File baru di sini disebut untracked; file lama yang diedit disebut modified.

- Staging Area (SA) — nama aslinya index
"Keranjang" berisi perubahan yang kamu pilih untuk masuk ke commit berikutnya. First principle: kenapa tempat ini harus ada? Supaya commit bisa terkurasi — kamu boleh mengedit 5 file, tapi hanya menyimpan 2 yang saling berhubungan dulu. Commit yang rapi > commit tumpukan campuran.

- Local Repo (LR) - hidden
Folder .git/ di dalam project-mu. Ini database riwayat: semua commit yang pernah kamu buat, tersimpan permanen dan bisa diakses offline. Inilah alasan git bisa "kembali ke versi minggu lalu".

- Remote (GitHub)
Salinan repo di server milik orang lain (GitHub). Fungsinya dua: backup dan titik temu kolaborasi. Local repo = wilayahmu sendiri; remote = tempat semua orang menyamakan versi.

**Perintah**
| Perintah | Arah | Digunakan untuk | Contoh |
|---|---|---|---|
| `git add <file>` | WD → SA | Memilih perubahan untuk masuk commit berikutnya | `git add pengertian.md contoh.md` |
| `git add .` | WD → SA | Memilih **semua** perubahan sekaligus | `git add .` |
| `git commit -m "pesan"` | SA → LR | Membekukan isi staging area jadi satu snapshot permanen + label | `git commit -m "Tambah penjelasan staging area"` |
| `git push origin main` | LR → R | Mengunggah commit lokal ke GitHub | `git push origin main` |
| `git fetch` | R → LR | Mengunduh commit baru dari GitHub **tanpa** menyentuh file di WD | `git fetch` (aman, cuma "intip") |
| `git pull` | R → WD | `fetch` + gabungkan sekaligus; commit baru langsung masuk file-mu | `git pull` (biasanya sebelum mulai kerja) |
| `git switch -c nama-branch` | — | Bikin branch baru + langsung pindah ke sana (untuk eksperimen) | `git switch -c experiment` |
| `git merge experiment` | branch → branch sekarang | Menggabungkan hasil eksperimen ke branch utama | `git merge experiment` |

**Perintah Analistik**
git status              # file apa yang berubah, dan ada di tempat mana (WD atau SA)
git log --oneline       # riwayat commit, ringkas
git diff                # detail perubahan di WD yang BELUM di-add
git diff --staged       # detail perubahan yang SUDAH di-add (siap commit)

Three things to remember:
1. Save often (`git commit`)
2. Push to remote (`git push`)
3. Branch for experiments (`git checkout -b experiment`)

```figure
s0-commit-dag
```

## Build It

### Step 1: Configure git

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

### Step 2: The daily workflow

```bash
git status
git add file.py
git commit -m "Add perceptron implementation"
git push origin main
```

### Step 3: Branching for experiments

```bash
git checkout -b experiment/new-optimizer

# ... make changes, commit ...

git checkout main
git merge experiment/new-optimizer
```

### Step 4: Working with this course repo

You can't push to the course repo itself — only maintainers have write access. Fork it on GitHub first (the Fork button, top right) so `origin` points at your own copy:

```bash
git clone https://github.com/YOUR-USERNAME/ai-engineering-from-scratch.git
cd ai-engineering-from-scratch

git checkout -b my-progress
# work through lessons, commit your code
git push origin my-progress
```

## Use It

For this course, you need exactly these commands:

| Command | When |
|---------|------|
| `git clone` | Get the course repo |
| `git add` + `git commit` | Save your work |
| `git push` | Back it up to GitHub |
| `git checkout -b` | Try something without breaking main |
| `git log --oneline` | See what you've done |

That's it. You don't need rebase, cherry-pick, or submodules for this course.

## Exercises

1. Fork this repo, clone your fork, create a branch called `my-progress`, make a file, commit it, push it
2. Create a `.gitignore` that excludes model checkpoint files (`.pt`, `.pth`, `.safetensors`)
3. Look at the commit history of this repo with `git log --oneline` and read how lessons were added

## Key Terms

| Term | What people say | What it actually means |
|------|----------------|----------------------|
| Commit | "Saving" | A snapshot of your entire project at a point in time |
| Branch | "A copy" | A pointer to a commit that moves forward as you work |
| Merge | "Combining code" | Taking changes from one branch and applying them to another |
| Remote | "The cloud" | A copy of your repo hosted somewhere else (GitHub, GitLab) |
