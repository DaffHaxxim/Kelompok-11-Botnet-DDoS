# Laporan Analisis PCAP - DDoS TCP SYN Flood

**Mata Kuliah:** Keamanan Jaringan Komputer (A) / Network Security (Praktik Keamanan Jaringan)
**Tugas:** PCAP Traffic Analysis Challenge with Wireshark - Week 3
**Kelompok:** 11
**Topik:** Botnet / DDoS

| No | Nama | NRP |
|----|------|-----|
| 1  | Sulthan Daffa Al Hasyimi | 5027251091 |
| 2  | Muhammad Yusuf | 5027251067 |
| 3  | Wildan Alfarezy | 5027251088 |

---

## 1. Pendahuluan

_(Tujuan analisis dan deskripsi singkat file PCAP. Sebutkan nama file, sumber, ukuran, dan dugaan awal jenis serangan.)_

- File yang dianalisis: `pkt.TCP.synflood.spoofed.pcap`
- Sumber: _(isi, lihat data/SUMBER.md)_
- Dugaan jenis serangan: DDoS TCP SYN Flood

---

## 2. Dasar Teori Singkat

_(Jelaskan konsep dengan bahasa kelompok sendiri.)_

- TCP three-way handshake: SYN -> SYN-ACK -> ACK.
- SYN Flood: penyerang membanjiri korban dengan paket SYN, tidak pernah menyelesaikan handshake, sehingga koneksi half-open menumpuk dan resource korban habis.
- DoS vs DDoS: _(isi - pembeda ada di jumlah sumber.)_
- Kaitan ke topik Botnet: _(isi - botnet melancarkan DDoS dengan membanjiri korban.)_

---

## 3. Metodologi

_(Langkah analisis yang dilakukan. Lihat analysis/PANDUAN-ANALISIS.md.)_

1. Triage dengan capinfos dan menu Statistics.
2. Filter konfirmasi jenis serangan.
3. Pengambilan bukti (screenshot + output tshark).

Tools: Wireshark 4.2.2, tshark, capinfos.

---

## 4. Temuan - Jenis Serangan: TCP SYN Flood (DDoS)

_(Isi dengan hasil analisis kelompok. Sisipkan screenshot dari folder screenshots/.)_

### 4.1 Komposisi trafik
_(Protocol Hierarchy - screenshot dan penjelasan.)_

![Protocol Hierarchy](../screenshots/01-protocol-hierarchy.png)

### 4.2 Bukti distribusi (banyak sumber -> satu korban)
_(Conversations / Endpoints - screenshot dan penjelasan. Sebutkan jumlah IP sumber dan korbannya.)_

![Conversations](../screenshots/02-conversations.png)

### 4.3 Bukti pola SYN Flood
_(Filter SYN vs SYN-ACK. Jelaskan kenapa SYN-ACK = 0 adalah bukti kuat.)_

| Filter | Jumlah paket |
|---|---|
| `tcp.flags.syn==1 && tcp.flags.ack==0` | _(isi)_ |
| `tcp.flags.syn==1 && tcp.flags.ack==1` | _(isi)_ |

### 4.4 Bukti lonjakan trafik
_(I/O Graph - screenshot dan penjelasan burst.)_

![I/O Graph](../screenshots/03-io-graph.png)

### Ringkasan bukti terverifikasi

| Metrik | Nilai |
|---|---|
| Total paket | 37.841 |
| IP sumber unik (spoofed) | 37.623 |
| Korban | 10.10.10.10 |
| Port target | 25565 |
| Paket SYN-ACK | 0 |

---

## 5. Kesimpulan

_(Ringkas temuan.)_

- Jenis serangan: _(isi)_
- Korban dan port: _(isi)_
- Sifat terdistribusi: _(isi - jumlah sumber palsu.)_
- Klasifikasi: DDoS berbasis protokol / state exhaustion (Layer 4), bukan amplifikasi.
- Tingkat keyakinan: _(isi.)_

---

## 6. Mitigasi

_(Teknik pencegahan/penanganan.)_

- SYN Cookies
- Backlog tuning dan timeout koneksi
- Rate limiting / firewall filtering
- Anti-spoofing (ingress filtering / BCP38)
- Layanan mitigasi DDoS / reverse proxy

---

## 7. Referensi

- File PCAP: StopDDoS/packet-captures - https://github.com/StopDDoS/packet-captures
- Materi kelas: 03 Common Network Attacks (Week 3)
- Wikipedia: SYN flood
- _(tambahkan referensi lain.)_
