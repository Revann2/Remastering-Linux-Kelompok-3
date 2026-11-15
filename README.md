# DataMint-OS 1.0

DataMint-OS adalah distro Linux hasil remastering Linux Mint 22.3 XFCE yang dirancang untuk web scraping, riset, dan analisis data. Lingkungan Python, database, dan alat scraping sudah terpasang dan siap dipakai sejak boot pertama, tanpa konfigurasi dependensi yang rumit.

Proyek ini adalah Tugas Akhir mata kuliah Sistem Operasi (Remastering Sistem Operasi Linux), Kelompok 03, Rombel 03.

## Daftar Isi

- [Tentang Proyek](#tentang-proyek)
- [Fitur Unggulan](#fitur-unggulan)
- [Informasi Sistem](#informasi-sistem)
- [Unduh dan Verifikasi](#unduh-dan-verifikasi)
- [Isi Sistem](#isi-sistem)
- [Kustomisasi](#kustomisasi)
- [Cara Menggunakan](#cara-menggunakan)
- [Struktur Repository](#struktur-repository)
- [Membangun Ulang ISO](#membangun-ulang-iso)
- [Hasil Pengujian](#hasil-pengujian)
- [Kendala dan Solusi](#kendala-dan-solusi)
- [Batasan yang Diketahui](#batasan-yang-diketahui)
- [Etika Scraping](#etika-scraping)
- [Lisensi dan Atribusi](#lisensi-dan-atribusi)
- [Anggota Kelompok](#anggota-kelompok)

## Tentang Proyek

Data analyst dan peneliti sering menghabiskan waktu untuk mengonfigurasi lingkungan Python, database, serta alat scraping secara manual sebelum mulai bekerja. DataMint-OS hadir untuk memberikan ekosistem analisis data yang langsung siap pakai tanpa instalasi dependensi dari awal.

Sasaran pengguna adalah data analyst, data engineer, peneliti, akademisi, dan mahasiswa sains data. Desktop XFCE dipilih karena ringan, sehingga RAM dan CPU lebih banyak tersisa untuk pemrosesan data.

## Fitur Unggulan

**1. Pre-configured Data Environment.** Pustaka Python populer seperti Pandas, Polars, BeautifulSoup4, Scrapy, Selenium, dan Playwright sudah terpasang pada satu virtual environment bersama, lengkap dengan JupyterLab dan kernel bernama DataMint Python.

**2. Integrated Mini-Database.** DuckDB dan SQLite tersedia langsung di terminal untuk kueri cepat pada dataset berukuran besar, tanpa memasang server database.

**3. Data Workflow Helper Script.** Tiga skrip bawaan mempercepat pekerjaan sehari-hari.

| Skrip | Fungsi |
|---|---|
| `datamint-new nama-proyek` | Membuat proyek analisis data baru lengkap dengan folder, virtual environment, dan template notebook |
| `datamint-scrape nama-proyek` | Membuat proyek web scraping lengkap dengan template Scrapy, BeautifulSoup, Selenium, Playwright, dan DuckDB |
| `datamint-selftest` | Memeriksa bahwa seluruh komponen DataMint-OS terpasang dengan benar |

## Informasi Sistem

| Item | Keterangan |
|---|---|
| Nama | DataMint-OS 1.0 |
| Distro dasar | Linux Mint 22.3 XFCE (Zena), berbasis Ubuntu 24.04 LTS (noble) |
| Kernel | Linux 6.14.0-37-generic |
| Arsitektur | amd64 (64-bit) |
| Desktop | XFCE |
| Mode boot | BIOS dan UEFI (ISO hibrida) |
| Alat remastering | chroot manual, squashfs-tools, xorriso |
| Berkas ISO | DataMint-OS-1.0.iso |
| Ukuran ISO | 3,6 GB (Linux Mint asli 2,8 GB) |
| Judul volume | DataMint-OS 1.0 |
| Jumlah paket sistem | 2058 (awal 1965, ditambah 102, dihapus 9) |
| Bahasa dan zona waktu | Locale id_ID.UTF-8 dan zona waktu Asia/Jakarta |

## Unduh dan Verifikasi

Berkas ISO diunggah ke penyimpanan daring karena ukurannya melebihi batas GitHub.

**Tautan unduhan** ISI_TAUTAN_GOOGLE_DRIVE_ATAU_ONEDRIVE

**Checksum SHA256**

```
66e0f8e6eafed752a1678ceb4397f42d0bee5a1dcefe464a72da8118f252fdc5  DataMint-OS-1.0.iso
```

Memverifikasi di Linux.

```bash
sha256sum DataMint-OS-1.0.iso
```

Memverifikasi di Windows (PowerShell).

```powershell
Get-FileHash DataMint-OS-1.0.iso -Algorithm SHA256
```

Hasilnya harus sama persis dengan checksum di atas. Jika berbeda, berkas rusak saat diunduh atau telah diubah.

## Isi Sistem

### Aplikasi inti yang ditambahkan

| Kelompok | Aplikasi |
|---|---|
| Bahasa dan analisis | Python 3 (dengan pip dan venv), JupyterLab, R-Base |
| Basis data | SQLite3, DB Browser for SQLite, DuckDB |
| Editor | VSCodium (ekstensi Python dan Jupyter sudah terpasang) |
| Web scraping | Scrapy, Selenium, geckodriver, Playwright (dengan browser Chromium dan Firefox miliknya) |
| Alat bantu terminal | csvkit, jq, tmux, htop, tree |

VSCodium dipilih sebagai pengganti VS Code karena berlisensi bebas sehingga aman didistribusikan ulang, sedangkan biner VS Code dari Microsoft tidak berlisensi demikian.

### Pustaka Python utama

Pandas, Polars, NumPy, SciPy, Matplotlib, Seaborn, scikit-learn, OpenPyXL, PyArrow, SQLAlchemy, tqdm, Requests, HTTPX, BeautifulSoup4, lxml, Scrapy, scrapy-playwright, Selenium, Playwright, DuckDB, JupyterLab, dan ipykernel. Seluruhnya dipasang pada virtual environment `/opt/datamint-venv`. Daftar lengkap beserta dependensinya ada pada `bukti/pip-paket.txt`.

### Aplikasi yang dihapus

Tujuh aplikasi (sembilan paket) yang tidak berhubungan dengan tema dihapus, membebaskan sekitar 323 MB ruang disk.

| Paket | Fungsi semula |
|---|---|
| celluloid | Pemutar video |
| drawing | Aplikasi menggambar |
| hypnotix | Televisi daring |
| rhythmbox, rhythmbox-plugins, rhythmbox-plugin-tray-icon | Pemutar musik |
| thunderbird | Klien email |
| transmission-gtk | Klien torrent |
| warpinator | Berbagi berkas lokal |

Daftar paket yang ditambah dan dihapus secara lengkap ada pada folder `bukti`.

## Kustomisasi

| Kategori | Perubahan |
|---|---|
| Identitas distro | Nama dan versi pada `/etc/os-release`, `/etc/lsb-release`, `/etc/issue`, `/etc/issue.net`, dan `/etc/linuxmint/info` diganti menjadi DataMint-OS 1.0 |
| Wallpaper | Wallpaper bawaan XFCE diganti wallpaper DataMint |
| Boot splash | Tema Plymouth baru bernama datamint (logo heksagon dan bar progres) menggantikan mint-logo |
| Menu boot | Teks dan gambar latar menu ISOLINUX (BIOS) dan GRUB (UEFI) diganti, serta judul volume ISO |
| Installer | Teks pada pemasang dan slideshow instalasi diganti menjadi DataMint-OS |
| Ikon menu | Ikon tombol menu aplikasi diganti logo DataMint |
| Mint Welcome | Dinonaktifkan dan disembunyikan dari menu |
| Locale dan zona waktu | id_ID.UTF-8 dan Asia/Jakarta |
| Environment otomatis | `/etc/profile.d/datamint.sh` menambahkan virtual environment ke PATH dan mengatur lokasi browser Playwright |
| Skrip helper | `datamint-new`, `datamint-scrape`, dan `datamint-selftest` dipasang di `/usr/local/bin` |

## Cara Menggunakan

### Menjalankan di VirtualBox

1. Buat mesin virtual baru, pilih tipe Linux dan versi Ubuntu (64-bit), lalu arahkan ke berkas `DataMint-OS-1.0.iso`.
2. Beri memori minimal 4096 MB, 2 sampai 4 CPU, disk virtual 40 GB, dan video memory 128 MB.
3. Jalankan mesin virtual. Sistem akan masuk ke sesi live tanpa perlu instalasi.
4. Untuk memasang ke disk, buka pemasang Install DataMint-OS di desktop dan ikuti langkahnya.

### Perintah dasar

```bash
datamint-selftest
```

```bash
datamint-new analisis-penjualan
```

```bash
datamint-scrape riset-harga
```

### Contoh alur kerja scraping dan analisis

```bash
datamint-scrape riset-harga
```

```bash
cd riset-harga
```

```bash
source .venv/bin/activate
```

```bash
python scrapers/contoh_bs4.py
```

```bash
python scrapers/simpan_duckdb.py
```

```bash
duckdb output/hasil.duckdb
```

```bash
jupyter lab
```

Alur ini membuat proyek, mengambil data dari situs, menyimpannya ke DuckDB, memeriksanya dengan SQL, lalu menganalisisnya di notebook. Panduan perintah lengkap ada di `docs/PANDUAN-PEMAKAIAN.md`.

## Struktur Repository

```
DataMint-OS/
  README.md
  scripts/
    datamint-new
    datamint-scrape
    datamint-selftest
  plymouth/datamint/
    datamint.plymouth
    datamint.script
    datamint-splash-logo.png
    datamint-splash-bar.png
  assets/
    datamint-wallpaper.png
    datamint-wallpaper.jpg
    datamint-logo.png
    datamint-logo-128.png
    splash.png
    splash800x600.png
  docs/
    PANDUAN-PEMAKAIAN.md
    LANGKAH-DI-KALI.md
    DATA-HASIL-REMASTERING.md
  bukti/
    pkg-before.txt
    pkg-after.txt
    pkg-ditambah.txt
    pkg-dihapus-semua.txt
    pkg-dihapus.txt
    pip-paket.txt
    branding-before.txt
    boot-params.txt
```

## Membangun Ulang ISO

Seluruh proses dilakukan dengan cara manual (chroot, squashfs-tools, dan xorriso) di Kali Linux pada WSL. Setiap perintah dijalankan sebagai root, dan setiap baris adalah satu perintah.

### Prasyarat

- Linux dengan ruang disk kosong minimal 30 GB dan koneksi internet.
- Berkas `linuxmint-22.3-xfce-64bit.iso` di folder kerja `/root/distro/datamint`.
- Salinan repository ini, dengan lokasinya disimpan pada variabel `REPO`.

```bash
apt install squashfs-tools xorriso rsync
```

```bash
REPO=/path/ke/DataMint-OS
```

### Tahap 1. Membongkar ISO

```bash
cd /root/distro/datamint
```

```bash
mkdir -p /mnt/mint
```

```bash
mount -o loop linuxmint-22.3-xfce-64bit.iso /mnt/mint
```

```bash
unsquashfs -d squashfs-root /mnt/mint/casper/filesystem.squashfs
```

```bash
umount /mnt/mint
```

### Tahap 2. Menyiapkan chroot dan menyalin berkas

```bash
rm -f squashfs-root/etc/resolv.conf
```

```bash
printf "nameserver 8.8.8.8\nnameserver 1.1.1.1\n" > squashfs-root/etc/resolv.conf
```

```bash
mount --bind /dev squashfs-root/dev
```

```bash
mount -t proc proc squashfs-root/proc
```

```bash
mount -t sysfs sys squashfs-root/sys
```

```bash
mount -t devpts devpts squashfs-root/dev/pts
```

```bash
cp $REPO/scripts/datamint-new $REPO/scripts/datamint-scrape $REPO/scripts/datamint-selftest squashfs-root/usr/local/bin/
```

```bash
mkdir -p squashfs-root/usr/share/datamint
```

```bash
cp $REPO/assets/datamint-wallpaper.png $REPO/assets/datamint-wallpaper.jpg $REPO/assets/datamint-logo.png $REPO/assets/datamint-logo-128.png squashfs-root/usr/share/datamint/
```

```bash
mkdir -p squashfs-root/usr/share/plymouth/themes/datamint
```

```bash
cp $REPO/plymouth/datamint/* squashfs-root/usr/share/plymouth/themes/datamint/
```

### Tahap 3. Masuk ke chroot dan memasang paket

```bash
chroot squashfs-root /bin/bash
```

Seluruh perintah berikut dijalankan di dalam chroot.

```bash
export DEBIAN_FRONTEND=noninteractive
```

```bash
VENV=/opt/datamint-venv
```

```bash
PWB=/opt/playwright-browsers
```

```bash
dpkg-query -W -f='${Package}\n' | sort > /root/pkg-before.txt
```

```bash
printf '#!/bin/sh\nexit 101\n' > /usr/sbin/policy-rc.d
```

```bash
chmod +x /usr/sbin/policy-rc.d
```

```bash
apt-get update
```

```bash
apt-get install -y python3 python3-pip python3-venv python3-dev git curl wget unzip ca-certificates gnupg sqlite3 sqlitebrowser r-base firefox jq tmux htop tree csvkit
```

```bash
apt-get install -y libnss3 libnspr4 libatk1.0-0t64 libatk-bridge2.0-0t64 libcups2t64 libdrm2 libxkbcommon0 libxcomposite1 libxdamage1 libxfixes3 libxrandr2 libgbm1 libasound2t64 libpango-1.0-0 libcairo2 || true
```

geckodriver dan DuckDB.

```bash
GV=$(curl -fsSL https://api.github.com/repos/mozilla/geckodriver/releases/latest | grep -m1 '"tag_name"' | cut -d'"' -f4 || true)
```

```bash
[ -z "$GV" ] && GV=v0.36.0
```

```bash
curl -fsSL -o /tmp/gd.tgz "https://github.com/mozilla/geckodriver/releases/download/${GV}/geckodriver-${GV}-linux64.tar.gz"
```

```bash
tar -xzf /tmp/gd.tgz -C /usr/local/bin
```

```bash
chmod +x /usr/local/bin/geckodriver
```

```bash
curl -fsSL -o /tmp/duckdb.zip https://github.com/duckdb/duckdb/releases/download/v1.5.6/duckdb_cli-linux-amd64.zip
```

```bash
unzip -o /tmp/duckdb.zip -d /usr/local/bin
```

```bash
chmod +x /usr/local/bin/duckdb
```

VSCodium dan ekstensinya.

```bash
wget -qO- https://gitlab.com/paulcarroty/vscodium-deb-rpm-repo/raw/master/pub.gpg | gpg --dearmor -o /usr/share/keyrings/vscodium-archive-keyring.gpg
```

```bash
echo 'deb [arch=amd64 signed-by=/usr/share/keyrings/vscodium-archive-keyring.gpg] https://download.vscodium.com/debs vscodium main' > /etc/apt/sources.list.d/vscodium.list
```

```bash
apt-get update
```

```bash
apt-get install -y codium
```

```bash
mkdir -p /etc/skel/.vscode-oss/extensions
```

```bash
codium --no-sandbox --user-data-dir /tmp/codium-tmp --extensions-dir /etc/skel/.vscode-oss/extensions --install-extension ms-python.python
```

```bash
codium --no-sandbox --user-data-dir /tmp/codium-tmp --extensions-dir /etc/skel/.vscode-oss/extensions --install-extension ms-toolsai.jupyter
```

Virtual environment Python dan browser Playwright.

```bash
python3 -m venv $VENV
```

```bash
$VENV/bin/pip install --upgrade pip wheel
```

```bash
$VENV/bin/pip install --no-cache-dir pandas polars numpy scipy matplotlib seaborn scikit-learn openpyxl pyarrow sqlalchemy tqdm requests httpx beautifulsoup4 lxml scrapy scrapy-playwright selenium playwright duckdb jupyterlab ipykernel
```

```bash
$VENV/bin/python -m ipykernel install --prefix /usr/local --name datamint --display-name "DataMint Python"
```

```bash
export PLAYWRIGHT_BROWSERS_PATH=$PWB
```

```bash
export PLAYWRIGHT_HOST_PLATFORM_OVERRIDE=ubuntu24.04-x64
```

```bash
$VENV/bin/playwright install chromium firefox
```

```bash
chmod -R a+rX $PWB
```

### Tahap 4. Environment otomatis dan skrip helper

```bash
echo 'export PATH=/opt/datamint-venv/bin:$PATH' > /etc/profile.d/datamint.sh
```

```bash
echo 'export PLAYWRIGHT_BROWSERS_PATH=/opt/playwright-browsers' >> /etc/profile.d/datamint.sh
```

```bash
echo 'export PLAYWRIGHT_HOST_PLATFORM_OVERRIDE=ubuntu24.04-x64' >> /etc/profile.d/datamint.sh
```

```bash
grep -q datamint.sh /etc/bash.bashrc || echo '. /etc/profile.d/datamint.sh' >> /etc/bash.bashrc
```

```bash
sed -i 's/\r$//' /usr/local/bin/datamint-new /usr/local/bin/datamint-scrape /usr/local/bin/datamint-selftest
```

```bash
chmod +x /usr/local/bin/datamint-new /usr/local/bin/datamint-scrape /usr/local/bin/datamint-selftest
```

```bash
source /etc/profile.d/datamint.sh
```

```bash
datamint-selftest
```

### Tahap 5. Menghapus paket dan mengatur locale

```bash
DEL=$(dpkg -l | grep -E '^ii +(thunderbird|hexchat|transmission-gtk|hypnotix|warpinator|celluloid|drawing|rhythmbox) ' | awk '{print $2}')
```

```bash
apt-get -s purge $DEL | grep -E '^(Remv|Purg)'
```

```bash
apt-get purge -y $DEL
```

```bash
apt-get autoremove -y --purge
```

```bash
apt-get install -y locales language-pack-id
```

```bash
locale-gen id_ID.UTF-8
```

```bash
update-locale LANG=id_ID.UTF-8
```

```bash
ln -sf /usr/share/zoneinfo/Asia/Jakarta /etc/localtime
```

```bash
echo 'Asia/Jakarta' > /etc/timezone
```

### Tahap 6. Branding

```bash
chmod 644 /usr/share/datamint/*
```

```bash
ln -sf /usr/share/datamint/datamint-wallpaper.jpg /usr/share/backgrounds/linuxmint/default_background.jpg
```

```bash
ln -sf /usr/share/datamint/datamint-wallpaper.jpg /usr/share/xfce4/backdrops/linuxmint.jpg
```

```bash
chmod 644 /usr/share/plymouth/themes/datamint/*
```

```bash
update-alternatives --install /usr/share/plymouth/themes/default.plymouth default.plymouth /usr/share/plymouth/themes/datamint/datamint.plymouth 200
```

```bash
update-alternatives --set default.plymouth /usr/share/plymouth/themes/datamint/datamint.plymouth
```

```bash
printf 'PRETTY_NAME="DataMint-OS 1.0"\nNAME="DataMint-OS"\nVERSION_ID="1.0"\nVERSION="1.0"\nVERSION_CODENAME=noble\nID=datamint\nID_LIKE="ubuntu debian"\nUBUNTU_CODENAME=noble\n' > /usr/lib/os-release
```

```bash
printf 'DISTRIB_ID=DataMint\nDISTRIB_RELEASE=1.0\nDISTRIB_CODENAME=noble\nDISTRIB_DESCRIPTION="DataMint-OS 1.0"\n' > /etc/lsb-release
```

```bash
printf 'DataMint-OS 1.0 \\n \\l\n\n' > /etc/issue
```

```bash
printf 'DataMint-OS 1.0\n' > /etc/issue.net
```

```bash
echo "<svg xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' width='128' height='128' viewBox='0 0 128 128'><image width='128' height='128' xlink:href='data:image/png;base64,$(base64 -w0 /usr/share/datamint/datamint-logo-128.png)'/></svg>" > /usr/share/pixmaps/xfce4-menu-mint.svg
```

```bash
rm /etc/xdg/autostart/mintwelcome.desktop
```

```bash
sed -i '/^\[Desktop Entry\]/a NoDisplay=true' /usr/share/applications/mintwelcome.desktop
```

```bash
sed -i 's/Linux Mint/DataMint-OS/g' /etc/xdg/autostart/mintupdate.desktop
```

```bash
sed -i 's/^DESCRIPTION=.*/DESCRIPTION="DataMint-OS 1.0"/' /etc/linuxmint/info
```

```bash
sed -i 's/^GRUB_TITLE=.*/GRUB_TITLE=DataMint-OS 1.0/' /etc/linuxmint/info
```

```bash
find /usr/share/ubiquity-slideshow/slides -name "*.html" -exec sed -i 's/Linux Mint/DataMint-OS/g' {} +
```

```bash
grep -rIl "Linux Mint" /usr/share/applications | xargs -r sed -i 's/Linux Mint/DataMint-OS/g'
```

```bash
grep -rIl "Linux Mint" /usr/share/ubiquity/gtk | xargs -r sed -i 's/Linux Mint/DataMint-OS/g'
```

Berkas kode `.py` pada pemasang sengaja tidak diubah karena kata Linux Mint di dalamnya bisa dipakai untuk logika pendeteksian.

### Tahap 7. Initramfs dan pembersihan

```bash
update-initramfs -u -k all
```

```bash
lsinitramfs /boot/initrd.img-6.14.0-37-generic | grep -c datamint
```

Sebelum pembersihan, salin berkas bukti dari `/root` di dalam chroot ke luar chroot. Lalu bersihkan.

```bash
rm -f /usr/sbin/policy-rc.d
```

```bash
apt-get clean
```

```bash
rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /root/.cache /root/.bash_history
```

```bash
rm -f /root/*.txt
```

```bash
find /var/log -type f -exec truncate -s 0 {} +
```

```bash
rm -f /etc/resolv.conf
```

```bash
ln -s ../run/systemd/resolve/stub-resolv.conf /etc/resolv.conf
```

```bash
exit
```

### Tahap 8. Membangun ISO

Setelah keluar dari chroot, lepas semua mount.

```bash
umount squashfs-root/dev/pts squashfs-root/dev squashfs-root/proc squashfs-root/sys
```

Menyalin isi ISO asli, kecuali sistem berkas lama.

```bash
mount -o loop linuxmint-22.3-xfce-64bit.iso /mnt/mint
```

```bash
mkdir -p iso
```

```bash
rsync -a --exclude=/casper/filesystem.squashfs /mnt/mint/ iso/
```

```bash
umount /mnt/mint
```

```bash
chmod -R u+w iso
```

Mengganti initrd, ukuran sistem, dan daftar paket.

```bash
cp squashfs-root/boot/initrd.img-6.14.0-37-generic iso/casper/initrd.lz
```

```bash
du -sx --block-size=1 squashfs-root | cut -f1 > iso/casper/filesystem.size
```

```bash
dpkg-query --admindir=squashfs-root/var/lib/dpkg -W --showformat='${Package} ${Version}\n' > iso/casper/filesystem.manifest
```

Mengganti teks dan gambar menu boot serta informasi ISO.

```bash
sed -i 's/Linux Mint 22.3/DataMint-OS 1.0/g; s/Linux Mint/DataMint-OS/g' iso/isolinux/live.cfg
```

```bash
sed -i 's/Linux Mint 22.3 Xfce 64-bit/DataMint-OS 1.0 64-bit/g' iso/boot/grub/grub.cfg
```

```bash
printf 'DataMint-OS 1.0 - Release amd64 20261111\n' > iso/.disk/info
```

```bash
sed -i 's/Linux Mint 22.3 "Zena" - Release amd64/DataMint-OS 1.0 - Release amd64/' iso/.disk/README.diskdefines
```

```bash
sed -i 's/Linux Mint/DataMint-OS/g' iso/.disk/mkisofs
```

```bash
cp $REPO/assets/splash.png iso/isolinux/splash.png
```

```bash
cp $REPO/assets/splash800x600.png iso/isolinux/splash800x600.png
```

Membuat sistem berkas terkompresi baru.

```bash
mksquashfs squashfs-root iso/casper/filesystem.squashfs -comp xz -b 1M -noappend
```

Memperbarui daftar checksum di dalam ISO.

```bash
(cd iso && find . -type f ! -name md5sum.txt ! -path './isolinux/boot.cat' -print0 | xargs -0 md5sum > md5sum.txt)
```

Mengambil parameter boot dari ISO asli, lalu membungkus ISO.

```bash
xorriso -indev linuxmint-22.3-xfce-64bit.iso -report_el_torito as_mkisofs 2>/dev/null > boot-params.txt
```

```bash
rm -f iso/isolinux/boot.cat
```

```bash
xorriso -as mkisofs -r -J -joliet-long -V 'DataMint-OS 1.0' -o DataMint-OS-1.0.iso -isohybrid-mbr --interval:local_fs:0s-15s:zero_mbrpt,zero_gpt,zero_apm:'linuxmint-22.3-xfce-64bit.iso' -partition_cyl_align on -partition_offset 16 -partition_hd_cyl 181 -partition_sec_hd 32 --mbr-force-bootable -apm-block-size 2048 -iso_mbr_part_type 0x00 -c '/isolinux/boot.cat' -b '/isolinux/isolinux.bin' -no-emul-boot -boot-load-size 4 -boot-info-table -eltorito-alt-boot -e '/boot/grub/efi.img' -no-emul-boot -isohybrid-gpt-basdat -isohybrid-apm-hfsplus iso
```

Membuat checksum SHA256.

```bash
sha256sum DataMint-OS-1.0.iso | tee DataMint-OS-1.0.iso.sha256
```

### Ringkasan hasil pembangunan

| Item | Nilai |
|---|---|
| Berkas yang dibongkar | 322.456 berkas, 22.900 direktori, 162.239 tautan simbolik |
| Ukuran sistem tidak terkompresi | sekitar 9,4 GB |
| Ukuran squashfs (xz, blok 1 MB) | 3.079,83 MB, yaitu 31,91 persen dari ukuran asli |
| Catatan boot El Torito | BIOS (`isolinux.bin`) dan UEFI (`efi.img`) |
| Isi manifest | 2058 paket |
| Isi md5sum.txt | 1298 baris |

## Hasil Pengujian

| Pengujian | Hasil |
|---|---|
| Boot live pada VirtualBox | Berhasil, sistem dimuat dari ISO sampai sesi live |
| Instalasi pada disk virtual | Berhasil melalui pemasang bawaan yang bermerek DataMint-OS, dan sistem hasil instalasi berjalan |
| Paket utama | `datamint-selftest` menampilkan 13 komponen berstatus OK, yaitu Python3, SQLite3, DuckDB CLI, R-Base, Firefox, geckodriver, VSCodium, modul Python, JupyterLab, kernel DataMint Python, browser Playwright, dan dua skrip helper |
| VSCodium | Terbuka tanpa instalasi tambahan, dengan ekstensi Python dan Jupyter beserta komponen pendukungnya |

### Lingkungan uji

| Item | Keterangan |
|---|---|
| Prosesor | AMD Ryzen 7 7445HS |
| Memori | 16 GB DDR5-4800 |
| Penyimpanan | 512 GB M.2 NVMe PCIe 3.0 SSD |
| Grafis | NVIDIA GeForce RTX 3050 Laptop GPU |
| Mesin virtual Linux Mint dan DataMint-OS | 6 CPU, memori 8192 MB, video memory 128 MB (identik) |

### Perbandingan sebelum dan sesudah remastering

| Item | Linux Mint 22.3 XFCE | DataMint-OS 1.0 |
|---|---|---|
| Ukuran ISO | 2,8 GB | 3,6 GB |
| Total memori | 7,8 GiB | 7,8 GiB |
| RAM terpakai saat idle | 865 MiB | 825 MiB |
| Memori bebas saat idle | 6,6 GiB | 6,7 GiB |

Ukuran ISO bertambah karena tambahan Python, R, JupyterLab, VSCodium, serta browser Chromium dan Firefox milik Playwright. Penggunaan RAM saat idle tidak bertambah karena aplikasi baru hanya memakai memori ketika dijalankan.

## Kendala dan Solusi

| Kendala | Solusi |
|---|---|
| Paket `cubic` pada snap ternyata Cubic VM, bukan pembuat ISO | Beralih ke cara manual dengan chroot, squashfs-tools, dan xorriso |
| Folder kerja berada di WSL sehingga berkas Windows diakses lewat `/mnt/c` | Berkas disalin dari folder Downloads Windows menggunakan jalur `/mnt/c/Users/...` |
| `python3-venv` belum terpasang sehingga pembuatan virtual environment gagal | Menjalankan ulang pemasangan paket sistem lalu membuat ulang venv |
| Unduhan DuckDB dari alamat latest memberi galat 404 | Memakai alamat dengan nomor versi tetap v1.5.6 |
| Penghapusan Mint Welcome ikut menyeret `mint-meta-xfce` dan `mint-meta-core` | Mint Welcome hanya dinonaktifkan dan disembunyikan, tidak dihapus |
| Tema menu UEFI merujuk `splash800x600.png` yang tidak ada di ISO | Gambar tersebut dibuat dan ditambahkan ke folder `isolinux` |
| Sandbox Firefox dibatasi di dalam chroot | Pengujian browser dilakukan di VirtualBox |
| Pemilihan editor dengan lisensi yang boleh didistribusikan ulang | Memakai VSCodium sebagai pengganti VS Code |

## Batasan yang Diketahui

- Gambar tangkapan layar di dalam slideshow pemasang masih berlogo Linux Mint, karena hanya teksnya yang diganti.
- Berkas kode pemasang (`install.py` dan `plugininstall.py`) tidak diubah agar pemasang tetap stabil, sehingga kata Linux Mint masih ada di dalam kode.
- Berkas penanda internal `iso/.disk/mint_iso` dipertahankan.
- Kernel tidak diubah dan tetap 6.14.0-37-generic.
- Aktivitas scraping memerlukan koneksi internet.

## Etika Scraping

Pastikan situs yang diambil datanya mengizinkan scraping. Periksa berkas `robots.txt` dan syarat layanan situs tersebut, beri jeda antar permintaan agar tidak membebani server, dan jangan mengambil data pribadi tanpa izin. Alamat quotes.toscrape.com pada contoh disediakan khusus untuk latihan.

## Lisensi dan Atribusi

DataMint-OS adalah proyek akademik turunan dari Linux Mint dan Ubuntu, dan bukan produk resmi Linux Mint maupun Canonical. Nama dan logo Linux Mint telah diganti dengan identitas DataMint-OS sesuai kebijakan merek dagang distro asal. Seluruh perangkat lunak pihak ketiga di dalam ISO tetap berada di bawah lisensinya masing-masing, termasuk Linux Mint, Ubuntu, XFCE, VSCodium, Python, R, DuckDB, SQLite, Scrapy, Selenium, dan Playwright. Skrip dan berkas konfigurasi pada repository ini dibuat untuk keperluan akademik.

## Anggota Kelompok

Kelompok 03, Rombel 03.

| No | Nama | NIM | Peran |
|---|---|---|---|
| 1 | Revan Aditya Kurniawan | 2604130109 | Ketua |
| 2 | Mikail Adrian Aozora | 2604130062 | Anggota |
| 3 | Caesar Abrisam Ghanim Abbad | 2604130063 | Anggota |
| 4 | Ahmad Nabiel Zawawi | 2604130107 | Anggota |
