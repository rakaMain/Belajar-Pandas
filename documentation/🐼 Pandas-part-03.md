## Sorting dengan `.sort_values` 🎯

### `.sort_values` – Pengurutan 🔢

- **Sintaks dasar:** `dataOrang.sort_values(by, ascending=True, inplace=False)`
    
- **Penjelasan:** Mengurutkan baris DataFrame berdasarkan nilai di satu atau beberapa kolom.
    
- **Catatan penting:**
    
    - `by` bisa berupa string (kolom tunggal) atau list of strings (multi‑kolom).
        
    - `ascending=True` untuk urut menaik; `False` untuk urut menurun.
        
    - Untuk multi‑kolom, `ascending` dapat berupa list boolean sejajar dengan `by`.
        
- **Contoh Penggunaan:**
    
    ```python
    # 1. Urut menaik berdasarkan "tinggi_badan"
    dataOrang.sort_values("tinggi_badan")
    
    # 2. Urut menurun berdasarkan "tinggi_badan"
    dataOrang.sort_values("tinggi_badan", ascending=False)
    
    # 3. Urut menurun berdasarkan "tinggi_badan" lalu "berat_badan"
    dataOrang.sort_values(
        ["tinggi_badan", "berat_badan"],
        ascending=False
    )
    
    # 4. Urut menaik "tinggi_badan" dan menurun "berat_badan"
    dataOrang.sort_values(
        ["tinggi_badan", "berat_badan"],
        ascending=[True, False]
    )
    ```
    
- **Kapan Gunakan `.sort_values`?**
    
    - Menampilkan daftar produk/record terlaris atau terlaku.
        
    - Menyiapkan data untuk analisis yang membutuhkan urutan nilai.
        
    - Memprioritaskan baris dengan kriteria tertentu (terbesar/terkecil).
        
