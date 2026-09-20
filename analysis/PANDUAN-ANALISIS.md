# Panduan Analisis - TCP SYN Flood

Langkah analisis file `data/pkt.TCP.synflood.spoofed.pcap` di Wireshark. Angka "hasil yang diharapkan" bisa dicek ulang di `hasil-tshark.txt`.

---

## Langkah 1 - Triage

```bash
capinfos data/pkt.TCP.synflood.spoofed.pcap
```

Lalu di Wireshark buka:
- **Statistics > Protocol Hierarchy** - komposisi protokol (100% TCP).
- **Statistics > Conversations** (tab IPv4) - bukti utama: banyak sumber ke satu korban.
- **Statistics > Endpoints** - banyaknya alamat sumber.
- **Statistics > I/O Graph** - lonjakan trafik mendadak (burst).

---

## Langkah 2 - Filter Konfirmasi

| Filter Wireshark | Hasil diharapkan | Fungsi |
|---|---|---|
| `tcp.flags.syn==1 && tcp.flags.ack==0` | 37.841 (semua paket) | Membuktikan semua paket adalah SYN |
| `tcp.flags.syn==1 && tcp.flags.ack==1` | 0 | Tidak ada handshake yang selesai |
| `ip.dst==10.10.10.10` | 37.841 | Hanya satu korban |
| `tcp.port==25565` | 37.841 | Satu port target (default Minecraft) |

Kunci diagnosis: banyak SYN, tapi SYN-ACK = 0 dan ACK = 0. Trafik normal tidak pernah begini.

---

## Langkah 3 - Bukti yang Diambil (screenshot ke folder ../screenshots/)

1. **Protocol Hierarchy** - menunjukkan isi 100% TCP.
2. **Conversations tab IPv4** (urut jumlah paket) - ribuan sumber -> `10.10.10.10`.
3. **I/O Graph** - garis datar lalu spike tajam.
4. **Satu paket SYN**, panel detail dibuka pada bagian TCP Flags (SYN aktif).
5. Hasil filter `tcp.flags.syn==1 && tcp.flags.ack==1` = 0 paket.

Beri nama screenshot yang jelas, contoh: `01-protocol-hierarchy.png`, `02-conversations.png`, dst.

---

## Fakta Terverifikasi (ringkas)

| Metrik | Nilai |
|---|---|
| Total paket | 37.841 |
| Semua SYN, SYN-ACK = 0 | ya |
| IP sumber unik | 37.623 (spoofed) |
| Korban | 10.10.10.10 |
| Port target | 25565 |
| Durasi | 23,68 s (burst di detik ke-0 dan ke-3) |
| Ukuran paket | 60 byte (minimal, tanpa payload) |

Detail angka: lihat `hasil-tshark.txt`.
