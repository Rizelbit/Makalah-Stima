# Makalah IF2211 Strategi Algoritma

## Application of the Divide-and-Conquer Approach to the Fragmentation and Reassembly of IPv4 Packets Based on MTU in a Network Simulator

**Penulis:** Reinhard Alfonzo Hutabarat (13524056)  
**Mata Kuliah:** IF2211 Strategi Algoritma, Semester II 2025/2026  
**Institusi:** Program Studi Teknik Informatika, STEI ITB

---

## Overview

Makalah ini menganalisis mekanisme fragmentasi dan reassembly paket IPv4 sebagai penerapan paradigma algoritma **Divide-and-Conquer (D&C)**. Ketika ukuran paket IPv4 melebihi Maximum Transmission Unit (MTU) dari sebuah link jaringan, protokol IPv4 memecah paket menjadi fragmen-fragmen yang lebih kecil, mengirimkan masing-masing fragmen secara independen, dan menyusun kembali di host tujuan.

Tiga fase D&C dipetakan secara eksplisit ke tahapan transmisi paket:

- **Divide** — Payload dipecah menjadi fragmen berukuran MTU-aligned menggunakan constraint alignment 8-byte: $m = \lfloor(M - H)/8\rfloor \times 8$, menghasilkan $k = \lceil N/m \rceil$ sub-masalah.
- **Conquer** — Setiap fragmen ditransmisikan secara independen melalui jaringan, dengan kemungkinan re-fragmentasi rekursif di router perantara jika link downstream memiliki MTU yang lebih kecil.
- **Combine** — Host tujuan mengumpulkan fragmen menggunakan field Identification sebagai grouping key dan Fragment Offset sebagai mekanisme ordering, kemudian melakukan verifikasi kontiguitas untuk merekonstruksi datagram asli.

Eksperimen dilakukan menggunakan **MAGI System**, sebuah network simulator berbasis C++ yang dibangun secara custom. Dalam topologi multi-hop (H1 → R1 → H2) dengan nilai MTU 300 dan 100 bytes, payload sebesar 508 bytes berhasil difragmentasi menjadi 2 fragmen di H1, di-re-fragmentasi secara rekursif menjadi 7 sub-fragmen di R1, dan direassembly dengan sempurna di H2 tanpa kehilangan data.

## Struktur Makalah

| Section | Isi |
|---|---|
| I. Introduction | Latar belakang, motivasi, dan kontribusi makalah |
| II. Theoretical Basis | Struktur header IPv4, definisi MTU, paradigma D&C, dan pemetaan fragmentasi IPv4 ke D&C |
| III. Algorithm Analysis | Analisis algoritma fragmentasi (Divide) dan reassembly (Combine) beserta kompleksitasnya |
| IV. Implementation and Experiment Design | Deskripsi MAGI System, desain topologi, dan skenario eksperimen |
| V. Results and Discussion | Hasil eksperimen untuk setiap fase D&C, analisis overhead dan efisiensi |
| VI. Conclusion | Kesimpulan dan arah pekerjaan masa depan |

## Source Code

Source code program network simulator (MAGI System) yang digunakan dalam eksperimen makalah ini dapat diakses di:

**https://github.com/labsister23/tugas-besar-jarkom-the-ping-girans**

## Referensi Utama

- [RFC 791] J. Postel, "Internet Protocol," 1981.
- [RFC 815] D. D. Clark & J. Reed, "A Fragmentation Control Protocol for Internet Datagrams," 1982.
- [CLRS] T. H. Cormen et al., *Introduction to Algorithms*, 3rd ed., MIT Press, 2009.
- [Munir] R. Munir, "Algoritma Divide and Conquer," Bahan Kuliah IF2211 Strategi Algoritma, STEI ITB, 2026.
- [Kurose] J. F. Kurose & K. W. Ross, *Computer Networking: A Top-Down Approach*, 8th ed., Pearson, 2021.
