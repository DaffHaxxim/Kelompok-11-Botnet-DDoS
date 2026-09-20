# Kelompok 11 - Botnet & DDoS (TCP SYN Flood)

Analisis PCAP untuk tugas **PCAP Traffic Analysis Challenge with Wireshark**
Mata kuliah **Keamanan Jaringan Komputer (A)** / Network Security (Praktik Keamanan Jaringan) - Week 3
Institut Teknologi Sepuluh Nopember (ITS)

Topik kelompok: **Botnet / DDoS**
Jenis serangan yang dianalisis: **TCP SYN Flood (spoofed, terdistribusi)**

---

## Anggota Kelompok

| No | Nama | NRP |
|----|------|-----|
| 1  | Sulthan Daffa Al Hasyimi | 5027251091 |
| 2  | Muhammad Yusuf | 5027251067 |
| 3  | Wildan Alfarezy | 5027251088 |

---

## Ringkasan

Repositori ini berisi analisis satu file PCAP berisi rekaman serangan **DDoS TCP SYN Flood**. Serangan ini masuk kategori topik **Botnet** pada materi Week 3: botnet dipakai untuk melancarkan DDoS dengan membanjiri korban memakai trafik berlebihan. File PCAP menunjukkan 37.623 alamat sumber palsu (spoofed) membanjiri satu korban `10.10.10.10` pada port `25565`.

Klasifikasi serangan: **DDoS berbasis protokol (Layer 4) - state exhaustion**, berbeda dari serangan amplifikasi/refleksi DNS yang juga dibahas di materi. Persamaannya hanya pada teknik IP spoofing.

---

## Struktur Repositori

```
Kelompok-11-Botnet-DDoS/
├── README.md                       Deskripsi proyek (file ini)
├── data/
│   ├── pkt.TCP.synflood.spoofed.pcap   File PCAP yang dianalisis
│   └── SUMBER.md                   Asal-usul dan lisensi file
├── analysis/
│   ├── PANDUAN-ANALISIS.md         Langkah + filter Wireshark + hasil yang diharapkan
│   └── hasil-tshark.txt            Bukti angka hasil tshark (terverifikasi)
├── screenshots/                    Bukti visual hasil Wireshark
│   ├── 01-protocol-hierarchy.jpg
│   ├── 02-filter-syn.jpg
│   ├── 03-conversations.jpg
│   └── 04-io-graph.jpg
└── report/
    └── LAPORAN.md                  Laporan analisis lengkap (final)
```

---

## Cara Reproduksi Analisis

Prasyarat: Wireshark 4.x (sudah terpasang di lingkungan lab).

```bash
# buka di GUI
wireshark data/pkt.TCP.synflood.spoofed.pcap &

# atau cek ringkasan via terminal
capinfos data/pkt.TCP.synflood.spoofed.pcap
```

Filter dan langkah lengkap ada di `analysis/PANDUAN-ANALISIS.md`.

---

## Status Pengerjaan

- [x] Pilih file PCAP
- [x] Analisis awal (triage + tshark)
- [x] Isi identitas anggota
- [x] Ambil screenshot bukti
- [x] Tulis laporan (`report/LAPORAN.md`)
- [x] Push ke GitHub

---

## Sumber

File PCAP: repositori publik [StopDDoS/packet-captures](https://github.com/StopDDoS/packet-captures) (bebas dipakai untuk edukasi). Detail di `data/SUMBER.md`.
