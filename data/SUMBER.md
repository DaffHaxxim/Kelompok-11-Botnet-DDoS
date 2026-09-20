# Sumber File PCAP

| Atribut | Nilai |
|---|---|
| Nama file | `pkt.TCP.synflood.spoofed.pcap` |
| Ukuran | ~2,8 MB (2.875.940 byte) |
| Repositori sumber | StopDDoS/packet-captures |
| URL | https://github.com/StopDDoS/packet-captures |
| Lisensi | Bebas dipakai untuk membangun/menguji sistem proteksi DDoS. Atribusi tidak wajib tapi dihargai. |
| Jenis serangan | TCP SYN Flood dengan IP spoofing (DDoS terdistribusi) |

## Cara unduh ulang (jika perlu)

```bash
curl -L -o pkt.TCP.synflood.spoofed.pcap \
  https://raw.githubusercontent.com/StopDDoS/packet-captures/main/pkt.TCP.synflood.spoofed.pcap
```

## Verifikasi keaslian

File adalah PCAP asli (bukan pointer Git LFS), diawali magic number `d4 c3 b2 a1`. Semua paket berformat TCP dan lolos parsing Wireshark/tshark 4.2.2.
