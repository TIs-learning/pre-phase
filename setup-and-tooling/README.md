# Phase 0: Setup & Tooling

> Get your environment ready for everything that follows.

## Penjelasan
Disini terdapat 12 folder untuk melakukan setup, saya merasa tidak perlu untuk melakukan semua. Saya akan menjabarkan apa saja yang perlu untuk dilakukan

* 1. 01-dev-environment: Lakukan persiapan hanya untuk bahasa python, **Node.js dan Typescript** Bisa dilakukan setelah menyelesaikan roadmap. 
* 2. 02-git-and-collaboration: Wajib dilakukan, setidaknya pahami walaupun masih bekerja sendiri.
* 3. 03-gpu-setup-and-cloud: Bisa dilakukan ketika mau memasuki **deep learning**.
* 4. 04-apis-and-keys: Bisa ditunda sampai berurusan dengan api seperti untuk memanggil LLM.
* 5. 05-jupyter-notebooks: Wajib dilakukan.
* 6. 06-python-environments: Wajib dilakukan.
* 7. 07-docker-for-ai: bisa dilakukan setelah ingin deployment model
* 8. 08-editor-setup: wajib dilakukan
* 9. 09 sampai 12 mereka sama sama monitoring cpu gpu ssh training model, saya pikir bisa dilakukan ketika belajar deep learning, karena algoritma machine learning tidak perlu seperti itu.

## Kesimpulan
Tidak usah bingung dengan 10 folder, saya akan jelaskan kapan dipersiapkan (f = folder):
- f1: Sekarang. Tentu kita semua perlu pengenalan saran saya fokus ke python dulu atau dengan julia.
- f5: wajib no debat.
- f6: wajib.
- f2: Setelah belajar python. git dan github akan banyak dipelajari ketika bekerja sama dalam project.
- f7: Ketika belajar deployment
- f8: Ketika membuat proyek ai.
- f4: Ketika ingin belajar generative ai (LLM) atau berkaitan dengan api.
- f3: Sebelum masuk ke neural network (deep learning) / pytorch / tensorflow.
- f10-f12: ketika pembelajaran / proyek neural network 

## Start this phase on GitHub

**Prerequisites:** None. You need Git and Python 3.11 or newer to begin. Other
tools are installed only when your route needs them.

**First lesson:** [Dev Environment](01-dev-environment/)

From the repository root, run the route-aware preflight:

```bash
python3 phases/00-setup-and-tooling/01-dev-environment/code/verify.py --route beginner
```

Keep the command, repository-root working directory, exit code, required check
results, and the printed `Next:` command. Optional misses are not failures.

**Next action:** Fix every required failure, rerun until the command exits 0,
then continue to [Git and Collaboration](02-git-and-collaboration/).

Browse the [full Phase 0 lesson list](../../README.md#phase-0) or the
[cross-phase roadmap](../../ROADMAP.md).
