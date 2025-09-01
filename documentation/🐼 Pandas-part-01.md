##### EPISODE 1 : Pengenalan DataFrame dan Series
*by : raka kayla*
## a. Import pandas 📥

```python
import pandas as pd
```

- **Mengapa?**  
    Pandas adalah library utama untuk manipulasi data tabular di Python.
    
- **Alias `pd`:**  
    Memperpendek penulisan, misal `pd.DataFrame` daripada `pandas.DataFrame`.
    
- **Tip:**  
    Selalu import di baris paling atas script/notebook agar konsisten.
    

---
## b. Membuat Series 🚧

- **Suhu Harian**, Suhu setiap pagi selama seminggu
```python
df = pd.Series([28, 29, 27, 30, 31, 29, 28],
    index=['Sen','Sel','Rab','Kam','Jum','Sab','Min'])
```
- **Status Kehadiran Siswa**, Hadir (True) atau Absen (False) untuk 4 siswa
```python
df = pd.Series([True, False, True, True],
    index= ['Andi','Budi','Citra','Dewi'])
```

---
## c. Membuat DataFrame 🏗️

```python
df = pd.DataFrame(
    [[1, 2, 3],
     [4, 5, 6],
     [7, 8, 9]],
    columns=["A", "B", "C"],
    index=["x", "y", "z"]
)
```

- **Struktur list bersarang:**
    
    - Setiap list di dalam mewakili satu baris (row).
        
    - Elemen dalam list → nilai kolom.
        
- **`columns=`**  
    Menetapkan nama kolom. Jika diabaikan, Pandas beri nama otomatis `0,1,2…`.
    
- **`index=`**  
    Menetapkan label baris. Berguna untuk akses data berbasis label (misal `.loc["y"]`).


**Membuat dataframe dengan Series :**
```python
df_siswa = pd.DataFrame({ 
	'Nama': ['Andi','Budi','Citra'], 
	'Kelas': ['12A','12B','12A'], 
	'Matematika': [85,78,92], 
	'Bahasa': [90,88,95] })
```
- **Struktur**:
	- satu series adalah satu kolom
	- satu baris nya sesuai dengan index yang sama pada tiap tiap series

---

## d. Membaca File 📂

1. **Membaca file Excel**
    
    ```python
    mie = pd.read_excel("penjualan_mie.xlsx", sheet_name="Sheet1")
    ```
    
    - Mengambil data dari sheet 'Sheet1' dalam file Excel.
        
2. **Membaca file JSON**
    
    ```python
    mie = pd.read_json("penjualan_mie.json")
    ```
    
    - Konversi file JSON menjadi DataFrame.
        
3. **Membaca dari database SQL (SQLite)**
    
    ```python
    import sqlite3
    conn = sqlite3.connect("penjualan_miebase.db")
    mie = pd.read_sql_query("SELECT * FROM penjualan", conn)
    ```
    
    - Menghubungkan ke database dan menjalankan query.
        
4. **Membaca file TSV**
    
    ```python
    mie = pd.read_csv("penjualan_mie.tsv", delimiter="\t")
    ```
    
    - Membaca file teks dengan pemisah tab.
5. **Membaca file CSV**
    
    ```python
    mie = pd.read_csv("penjualan_mie.csv")
    ```
    
    - Membaca file csv
        


---

## e. Melihat Informasi Dasar DataFrame ℹ️

1. **`mie.info()`**
    
    - 📊 Menampilkan ringkasan: jumlah entries, kolom, non-null count, tipe data, memori.
        
2. **`mie.describe()`**
    
    - 📈 Statistik ringkas kolom numerik: count, mean, std, min, 25/50/75%, max.
        
3. **`mie['A'].nunique()`**
    
    - 🔢 Hitung nilai unik di kolom A.
        
    - ✅ Untuk mengerti cardinality fitur.
        
4. **`mie.shape`**
    
    - 🎛️ Tuple `(baris, kolom)`.
        
    - 🧮 Cepat cek dimensi data.
        
5. **`mie.size`**
    
    - 🔢 Total elemen (`baris × kolom`).
        
    - 🧹 Cek skala data sebelum operasi besar.
        

---

## f. Menampilkan sebagian data 👀

- **`mie.head(n)`** → n baris pertama (default `n=5`).
    
- **`mie.tail(n)`** → n baris terakhir (default `n=5`).
    
- **`mie.sample(n)`** → n baris acak.
    

**Kegunaan:**

- ▶️ `head`/`tail`: cek struktur & format kolom.
    
- 🎲 `sample`: validasi acak untuk cek inkonsistensi.
    
