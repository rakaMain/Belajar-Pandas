# a. Mengubah format isi kolom & dasar `datetime` 🕰️

### a.1 `pd.to_datetime()` Parsing tanggal

- **Sintaks dasar:** `df['kolom_dt'] = pd.to_datetime(df['kolom_tanggal'])`
    
- **Penjelasan:** Mengubah kolom bertipe `object`/string menjadi tipe `datetime64[ns]` agar bisa dipakai `.dt` accessor, filtering tanggal, resample, dll.
    
- **Contoh Penggunaan:**
    

```python
# biasa
data_orang["tanggal_lahir"] = pd.to_datetime(data_orang['tanggal_lahir'])

```

- **Kapan Gunakan?**
    
    - Saat kolom tanggal masih string dan mau digunakan sebagai tanggal.
        
    - Bila butuh operasi berbasis waktu (ekstraksi tahun, filtering, dsb).
        

---

# b. Membuat kolom Tahun 📅

### b.1 `.dt.year` — Ambil tahun

- **Sintaks dasar:** `df['tahun'] = df['kolom_datetime'].dt.year`
    
- **Contoh Penggunaan:**
    

```python
data_orang['Tahun_lahir'] = data_orang['tanggal_lahir'].dt.year
```

- **Kapan Gunakan?**
    
    - Saat ingin agregasi/perbandingan berdasarkan tahun (mis. jumlah per tahun, filter kelahiran 2000-an).
        

---

# c. Membuat kolom Bulan 🗓️

### c.1 `.dt.month` & `.dt.month_name()` — Nomor & Nama bulan

- **Sintaks dasar:**
    
    - `df['bulan'] = df['kolom_datetime'].dt.month`
        
    - `df['bulan_nama'] = df['kolom_datetime'].dt.month_name()`
        
- **Contoh Penggunaan:**
    

```python
data_orang['Bulan_lahir'] = data_orang['tanggal_lahir'].dt.month            # 1..12
data_orang['Bulan_nama'] = data_orang['tanggal_lahir'].dt.month_name()     # 'January', dsb.
```

- **Kapan Gunakan?**
    
    - Analisis musiman, grouping per bulan, membuat label laporan.
        

---

# d. Membuat kolom Hari & Hari dalam Minggu 📆

### d.1 `.dt.day`, `.dt.weekday`, `.dt.day_name()`

- **Sintaks dasar:**
    
    - `df['hari'] = df['kolom_datetime'].dt.day` # tanggal dalam bulan (1..31)
        
    - `df['weekday'] = df['kolom_datetime'].dt.weekday` # 0=Senin .. 6=Minggu
        
    - `df['hari_nama'] = df['kolom_datetime'].dt.day_name()`
        
- **Contoh Penggunaan:**
    

```python
data_orang['Hari_tanggal'] = data_orang['tanggal_lahir'].dt.day
data_orang['Hari_ke_minggu'] = data_orang['tanggal_lahir'].dt.weekday
data_orang['Hari_nama'] = data_orang['tanggal_lahir'].dt.day_name()
```

- **Kapan Gunakan?**
    
    - Saat butuh analisa berdasarkan hari (mis. hari lahir terbanyak, pola weekday/weekend).
        

---

# e. Menyimpan file baru 💾

### e.1 `to_csv()` — Simpan hasil ke file

- **Sintaks dasar:** `df.to_csv(path, index=False)
    
- **Penjelasan:** `index=false` tidak menyimpan index DataFrame ke file CSV. Hasil CSV hanya berisi kolom-kolom DataFrame biasa (default yang paling sering dipakai).
    
- **Contoh Penggunaan:**
    

```python

data_orang.to_csv('./data_orang_date.csv', index=False)

```

- **Kapan Gunakan?**
    
    - Setelah preprocessing selesai dan ingin menyimpan dataset baru untuk pipeline/rekaman.
        
---
