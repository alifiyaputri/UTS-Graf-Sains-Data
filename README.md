# UTS-Graf-Sains-Data

## Identitas

| | |
|---|---|
| Nama | Alifiyanti Putri Nur Azizah |
| NIM | 24031554032 |
| Kelas | 2024B |
| Mata kuliah | Graf Sains Data (UTS, Gasal 2026/2027) |

**Pembagian periode data interaksi:**
- **P1 (training):** 1-15 Agustus 2015
- **P2 (testing):** 1-18 September 2015
- 
Repository tugas UTS Graf Sains Data: analisis graf RetailRocket menggunakan Neo4j, Vector Space Model, cosine similarity, dan rekomendasi item.

## Dataset

Dataset yang digunakan dalam proyek ini adalah **Retailrocket Recommender System Dataset** yang diperoleh dari Kaggle.

**Sumber dataset:** https://www.kaggle.com/retailrocket/ecommerce-dataset

### Cara menggunakan dataset
1. Buka tautan Kaggle di atas.
2. Download dataset dan ekstrak file ZIP.
3. Ambil file `events.csv`.
4. Letakkan `events.csv` sesuai lokasi dataset yang dibaca oleh notebook.
5. Jalankan notebook secara berurutan dari awal.

## Struktur File

| File | Keterangan |
|---|---|
| `032_Alifiyanti Putri_UTS GSD.ipynb` | Notebook jawaban UTS (kode, output, dan penjelasan) |
| `events_train_P1.csv` | Hasil filter timestamp untuk P1 (265.509 baris) |
| `events_test_P2.csv` | Hasil filter timestamp untuk P2 (303.710 baris) |

File `events.csv` asli tidak disertakan karena ukurannya besar. Unduh dari tautan Kaggle di atas.

## Cara Menjalankan Notebook

1. Unduh `events.csv` dari Kaggle dan letakkan satu folder dengan notebook.
2. Pastikan Neo4j aktif di `bolt://localhost:7687` dengan database `neo4j`.
3. Install library: `pandas`, `numpy`, `scipy`, `scikit-learn`, `networkx`, `matplotlib`, `neo4j`, `tqdm`.
4. Jalankan notebook dari atas ke bawah. Password Neo4j akan diminta lewat kotak input (`getpass`).

## Ringkasan Hasil

**2.1 Wrangling dan EDA**
- Subgraf P1 di Neo4j: 153.836 simpul `Visitor` dan 76.078 simpul `Item`, dengan relasi `VIEWED` (256.361), `ADDED_TO_CART` (6.991), dan `BOUGHT` (2.091).
- VSM dibangun dari sampel acak 2.000 baris P1 (`random_state=42`): matriks user-item berukuran 1918 x 1869 (sparsity 99,94%).
- Proyeksi yang dipilih: **Item-Item** (209 edge, dibanding 179 edge pada proyeksi User-User).
- Cosine similarity dihitung pada 500 item terpopuler di P1 dan disimpan di Neo4j sebagai 2.064 relasi `SIMILAR_TO`. Contoh item acuan: **461686**.

**2.2 Analytics**
- Rekomendasi memakai item-based KNN dengan k = 5. User dipilih acak dengan `random.Random(42)` dari user yang dapat dievaluasi (110 user).
- User terpilih: **1073958**. Item yang diiklankan: 248455, 183758, 119736.
- Evaluasi: **Hit@5 = 0** dan **NDCG@5 = 0** (item relevan 409804 tidak muncul di top-5).
