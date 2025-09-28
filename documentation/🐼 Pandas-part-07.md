## a. Menggabungkan Data 🔗

### a.1 `merge` — Join berbasis kolom / key 🧩

- **Sintaks dasar:**
    

```python
df1.merge(df2, how='inner', on='kolom')
)
```

- Penjelasan
	- `how='inner'`  
    Tipe join: **inner join** → hanya baris yang memiliki **nilai kunci yang sama di kedua DataFrame** yang disertakan (irisan).
    
	- `on='kolom'`  
    Menentukan **kolom kunci** yang dipakai untuk mencocokkan baris. Bisa berupa string (satu kolom) atau list (multi-key). Kolom tersebut **harus ada di kedua** DataFrame.

		
		



- **Contoh Kasus & Contoh Kode:**


```python
# Data pelanggan & transaksi digabung berdasarkan customer_id
df1.merge(df2, how='inner', on='nama')
```

-  **Macam - macam `how`:**
	![[join-or-merge-in-python-pandas-1 3.png]]

    🧩 **inner** → hanya baris yang ada di kedua tabel (irisan).
    ```python
    merged_inner = df1.merge(df2, how='inner', on='nama')
    ```
        
    🔀 **outer** → semua baris dari kedua tabel, isi yang kosong diisi NaN (union).
    ```python
    merged_left = df1.merge(df2, how='left', on='nama')
    ```

    🧭 **left** → semua baris dari kiri + matching dari kanan.
    ```python
    merged_right = df1.merge(df2, how='right', on='nama')
    ```
        
    ↩️ **right** → semua baris dari kanan + matching dari kiri.
    ```python
    merged_inner = df1.merge(df2, how='inner', on='nama')
    ```
    ✖️**cross** → cross join (cartesian product) — setiap baris kiri dikalikan setiap baris kanan.
    ```python
    merged_cross = df1.merge(df2, how='cross')
    ```



    ---
    
    

- **Kapan Gunakan `merge`?**
    
    - Saat ada kolom _key_ yang jelas (ID, kode, tanggal).
        
    - Ketika butuh kontrol jenis join (left/right/inner/outer).
        
    - Ketika ingin memvalidasi relasi (pakai `validate`).
        
---

### a.2 `concat` — Gabungkan baris atau kolom secara cepat ➕➖

- **Sintaks dasar:**
    

```python
pd.concat([df1, df2], axis=0, join='outer', ignore_index=False)
```

- **Penjelasan:**  
    `concat` dipakai untuk **menumpuk** DataFrame. Default `axis=0` (gabung baris). Kalau `axis=1` → gabung kolom (tempelkan kolom dari DF lain).  
    **Intinya:** `concat` tidak mencocokkan berdasarkan kolom kunci — ia hanya menyusun DataFrame menurut axis dan index/kolom.
    
- **Parameter penting:**
    
    - `axis=0` → vertikal (tambah baris).
        
    - `axis=1` → horizontal (tambah kolom).
        
    - `join='outer'` (default) → gabungkan semua label (union).
        
        - Kalau `axis=0`: semua kolom dari kedua DF akan muncul; kolom yang tidak ada di salah satu akan `NaN`.
            
        - Kalau `axis=1`: semua index dari kedua DF akan muncul; baris yang tidak ada di salah satu akan `NaN`.
            
    - `ignore_index=True` → reset index baru (0..n-1).
    - `keys=[...]` → memberi label sumber dan membuat MultiIndex (berguna untuk melacak asal baris).
        
- **Contoh Penggunaan:**
    

```python
# Gabungkan 2 DF dengan kolom sama (tambah baris)
combined = pd.concat([df1, df2], ignore_index=True)

# Gabungkan 2 DF berdampingan (gabung kolom)
wide = pd.concat([left_df, right_df], axis=1)

# Tandai sumber data (keys)
combined = pd.concat([df1, df2], keys=['a','b'])
```

- **Kapan Gunakan `concat`?**
    
    - Menggabungkan banyak file CSV (mis. data per hari) → pakai `concat` axis=0.
        
    - Menyatukan fitur dari dua DataFrame dengan index sama → pakai `concat` axis=1.
        
    - Saat butuh performa cepat untuk stacking sederhana.
        
- **Catatan:**
    
    - Sintaks benar: `pd.concat([df1, df2])` (bukan `pd.concat([df1], [df2])`).
        
    - Untuk gabungan baris, pastikan kolom konsisten; kalau tidak, hasil akan berisi NaN di kolom yang hilang.

---

### a.3 `append` — Deprecated ⚠️ (jangan dipakai)

- **Contoh lama:** `df1.append(df2)`
    
- **Status:** Sudah _deprecated_ di pandas modern (versi terbaru menghapusnya).
    
- **Ganti dengan:** `pd.concat([df1, df2], ignore_index=True)`
    

