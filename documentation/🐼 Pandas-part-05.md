
# Menambah & Mengelola Kolom pada DataFrame 🧩

---

## a. Menambahkan Kolom ➕

### a.1 Cara paling langsung — assign literal / nilai tunggal

- **Sintaks dasar:** `df['KolomBaru'] = nilai`
    
- **Penjelasan:** Menambahkan kolom baru yang nilainya sama untuk semua baris.
    
- **Contoh Penggunaan:**
    

```python
# menambahkan kolom Harga dengan nilai 5000 (gunakan 5000, bukan "5.000")
mie['harga_baru'] = 5000
```

- **Kapan gunakan?**
    
    - Saat ingin menambahkan metadata tetap (mis. tarif tetap, label kategori default).
        
    - Saat membuat kolom placeholder untuk diisi nanti.
        

---

### a.2 Kondisional dengan `numpy.where` — buat nilai berbeda berdasarkan kondisi ⚖️

- **Sintaks dasar:** `df['KolomBaru'] = np.where(kondisi_boolean, nilai_if_true, nilai_if_false)`
    
- **Penjelasan:** Membuat kolom baru yang nilainya bergantung pada kondisi yang dievaluasi per baris.
    
- **Contoh Penggunaan:**
    

```python
# contoh (asumsi DataFrame bernama 'kopi' dan kolom 'Tipe Kopi' ada)
import numpy as np

mie["Harga_baru"] = np.where(mie['Tipe_mie'] == 'mie ayam', 20.0, 30.0)
```

> ✨ _Catatan:_ perhatikan penulisan nya dan jangan typo

- **Contoh tambahan (lebih dari 2 kondisi menggunakan `np.select`):**
    

```python
# jika ada lebih dari dua kondisi, gunakan np.select untuk readability
conditions = [
    mie['tipe_mie'] == 'mie baso',
    mie['tipe_mie'] == 'mie ayam',
    mie['tipe_mie'] == 'mie bangladesh'
]
choices = [35.0, 32.0, 31.0]
mie['Harga_baru'] = np.select(conditions, choices, default=29.0)
```

- **Kapan gunakan?**
    
    - Saat nilai ditentukan oleh kondisi sederhana (binary/ternary).
        
    - Cepat dan efisien untuk kondisi yang tidak kompleks.
        

---

## b. Menghapus Kolom ❌

### b.1 `.drop()` — hapus kolom fleksibel

- **Sintaks dasar:** `df.drop(columns=['Kolom1','Kolom2'], inplace=True/False)`
    
- **Penjelasan:** Menghapus satu atau lebih kolom; `inplace=True` merubah DataFrame itu sendiri.
    
- **Contoh Penggunaan:**
    

```python
# menghapus kolom Harga dari DataFrame kopi
mie.drop(columns=['harga'], inplace=True)
```


- **Kapan gunakan?**
    
    - Menghilangkan kolom sensitif, duplikat, atau yang tidak diperlukan sebelum analisis.
        
    - Saat ingin mengurangi memori/ukuran output.
        

---

### b.2 Tip: Hati-hati dengan `inplace`

- `inplace=True` sering dipakai tapi mengembalikan `None`. Untuk workflow yang lebih aman, gunakan assignment:
    

```python
mie = mie.drop(columns=['harga'])
```


---

## c. Membuat Kolom menggunakan kolom lain 🔗

### c.1 Operasi aritmetika antar kolom

- **Sintaks dasar:** `df['KolomBaru'] = df['A'] * df['B']`
    
- **Penjelasan:** Buat kolom hasil perhitungan (mis. total, revenue).
    
- **Contoh Penggunaan:**
    

```python
mie['Penghasilan'] = mie['terjual'] * mie['harga']
```

- **Kapan gunakan?**
    
    - Hitung metrik agregat per-baris (pendapatan, total biaya, margin kasar).
        

---

### c.2 Ekstraksi string & transformasi teks

- **Sintaks dasar:** `df['KolomBaru'] = df['KolomTeks'].str.<method>`
    
- **Penjelasan:** Gunakan `.str` untuk split, lower, contains, dll.
    
- **Contoh Penggunaan:**
    

```python
# mengambil nama depan dari kolom Nama (split spasi lalu ambil indeks 0)
bios_new['Nama_pertama'] = bios_new['Nama'].str.split(' ').str[0]

# mengambil nama belakang dari kolom Nama (split spasi lalu ambil indeks 0)
bios_new['Nama_pertama'] = bios_new['Nama'].str.split(' ').str[1]

```

- **Kapan gunakan?**
    
    - Saat butuh ekstraksi bagian teks (nama depan, domain email, kode pos).
        
    - Pra-proses untuk grouping atau pencocokan.
        

---

## d. Mengubah Nama Kolom ✏️

### d.1 `.rename()` — ubah nama satu/lebih kolom

- **Sintaks dasar:** `df.rename(columns={'lama':'baru'}, inplace=True/False)`
    
- **Penjelasan:** Ganti nama kolom tertentu; sangat berguna untuk menyelaraskan nama sebelum export/visualisasi.
    
- **Contoh Penggunaan:**
    

```python
# mengganti beberapa nama kolom
mie.rename(columns={'Harga_baru': 'Harga', 'terjual': 'terjul_baru'}, inplace=True)
```


- **Kapan gunakan?**
    
    - Membuat kolom agar mudah di baca
        
    - Saat mengeksport ke format yang butuh kolom tertentu.
        

---

### d.2 Alternatif: ganti semua nama dengan `df.columns = [...]`

- Jika ingin mengganti semua header sekaligus:
    

```python
mie.columns = ['Nama','Tipe_mie','terjual','Harga']
```


- **Catatan:** Pastikan jumlah nama cocok dengan jumlah kolom.

    


---
