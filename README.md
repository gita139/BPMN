graph TD
    %% Pool Pelanggan
    subgraph Pelanggan
        A1[Mulai] --> A2[Pesan Produk]
        A5[Terima Produk] --> A6[Selesai]
    end

    %% Pool Toko Online
    subgraph "Toko Online"
        B1[Terima Pesanan] --> B2[Verifikasi Pembayaran]
        B3{Pembayaran Valid?}
        B2 --> B3
        B3 -- Ya --> B4[Proses Pesanan]
        B3 -- Tidak --> B6[Gagal, Hubungi Pelanggan]
    end

    %% Pool Gudang
    subgraph Gudang
        C1{Produk Tersedia?}
        C2[Kemas Produk] --> C3[Kirim Produk]
        C1 -- Ya --> C2
        C1 -- Tidak --> C4[Lapor Stok Habis]
    end

    %% Aliran antar pool
    A2 --> B1
    B4 --> C1
    C3 --> A5
    B6 -.-> A2
    C4 -.-> B6
