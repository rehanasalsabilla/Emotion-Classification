# 😊 Emotion Classification Using Machine Learning

## 🧩 Pengertian Proyek
Proyek ini bertujuan untuk membangun sistem **klasifikasi emosi pada ulasan pelanggan (customer review)** menggunakan algoritma *Machine Learning* berbasis *Natural Language Processing (NLP)*.  
Sistem ini mampu mengenali emosi utama seperti **Happy, Sadness, Fear, Love, dan Anger** dari teks ulasan pelanggan, sehingga dapat membantu bisnis memahami sentimen dan perasaan pengguna terhadap produk atau layanan mereka.

---

## 🧾 Deskripsi Proyek
Proyek ini merupakan implementasi klasifikasi teks menggunakan teknik *TF-IDF (Term Frequency – Inverse Document Frequency)* untuk ekstraksi fitur dan tiga model *Machine Learning* berbeda:  
- **Naive Bayes (MultinomialNB)**  
- **Random Forest Classifier**  
- **Support Vector Machine (SVM)**  

Melalui evaluasi performa model menggunakan *GridSearchCV* dan metrik akurasi, model terbaik dipilih berdasarkan performa validasi tertinggi.  
Sistem kemudian digunakan untuk memprediksi emosi pada data uji dan menghasilkan file *submission* untuk evaluasi akhir.

---

## 📂 Dataset

### 📁 Sumber Dataset
Dataset diambil dari **Emotion Classification AI Class Dataset (Kaggle)** dengan tiga file utama:
/kaggle/input/emotion-classification-ai-class/
│
├── data_train.csv
├── data_test.csv
└── sample_solution.csv


### 📊 Deskripsi Dataset
- **data_train.csv**: berisi 4320 data ulasan pelanggan dengan label emosi.  
- **data_test.csv**: berisi 1080 data ulasan tanpa label (digunakan untuk prediksi).  
- **sample_solution.csv**: contoh format pengumpulan hasil prediksi.

Kolom pada dataset:
| Kolom | Deskripsi |
|--------|------------|
| `Customer Review` | Teks ulasan pelanggan |
| `Emotion` | Label emosi yang dikategorikan ke dalam 5 kelas |

Distribusi label pada data pelatihan:
| Emotion | Jumlah Data |
|----------|--------------|
| Happy | 1426 |
| Sadness | 943 |
| Fear | 753 |
| Love | 641 |
| Anger | 557 |

---

## ⚙️ Tools dan Teknologi

| Tools / Library | Kegunaan |
|------------------|-----------|
| **Python** | Bahasa pemrograman utama |
| **Pandas, NumPy** | Manipulasi dan analisis data |
| **NLTK & Sastrawi** | Tokenisasi, stopword removal, dan stemming Bahasa Indonesia |
| **Scikit-learn** | Model Machine Learning, TF-IDF, GridSearchCV |
| **Matplotlib & Seaborn** | Visualisasi data dan distribusi emosi |
| **Spacy** | Pemrosesan bahasa alami tambahan |
| **Kaggle / Colab Environment** | Lingkungan eksekusi proyek |

---

## 🔍 Tahapan Analisis

### 1️⃣ Exploratory Data Analysis (EDA)
- Menampilkan jumlah data, tipe data, dan nilai kosong.
- Visualisasi distribusi emosi dalam bentuk *pie chart* dan *bar plot*.
- Contoh ulasan dengan label emosi ditampilkan untuk eksplorasi awal.

### 2️⃣ Data Preprocessing
Langkah-langkah pra-pemrosesan teks dilakukan untuk meningkatkan kualitas fitur:
- **Case folding** → mengubah semua huruf menjadi huruf kecil.  
- **Pembersihan teks** → menghapus karakter non-alfabet seperti angka dan tanda baca.  
- **Tokenisasi** → memecah teks menjadi kata.  
- **Stopword removal** → menghapus kata tidak bermakna (dengan *stopwords Bahasa Indonesia*).  
- **Stemming** → mengubah kata ke bentuk dasar menggunakan **Sastrawi**.

Contoh hasil setelah preprocessing:
| Sebelum | Sesudah |
|----------|----------|
| “Baguuuus, sesuai dengan pesanan. Semoga sukses selalu..” | “baguuuus sesuai pesan moga sukses” |

### 3️⃣ Label Encoding
Label emosi dikonversi menjadi bentuk numerik agar dapat diproses oleh model:
| Emotion | Encoded |
|----------|----------|
| Anger | 0 |
| Fear | 1 |
| Happy | 2 |
| Love | 3 |
| Sadness | 4 |

### 4️⃣ Feature Extraction (TF-IDF)
Ekstraksi fitur teks menggunakan **TF-IDF Vectorizer** dengan *n-gram range* `(1,1)` dan `(1,2)` untuk mempertahankan konteks kata tunggal dan pasangan kata.

### 5️⃣ Model Training dan Hyperparameter Tuning
Tiga algoritma diuji dengan **GridSearchCV** untuk mencari parameter terbaik:
- **Multinomial Naive Bayes**
  - Best Params: `alpha=0.1`, `max_features=5000`, `ngram_range=(1,2)`
  - Accuracy: **0.5671**
- **Random Forest**
  - Best Params: `n_estimators=300`, `max_depth=None`, `max_features=3000`
  - Accuracy: **0.5648**
- **Support Vector Machine (SVM)**
  - Best Params: `C=1`, `kernel=linear`, `max_features=6000`, `ngram_range=(1,2)`
  - Accuracy: **0.6030**

### 6️⃣ Model Evaluation
Evaluasi dilakukan menggunakan **accuracy**, **precision**, **recall**, dan **f1-score**.  
Model terbaik adalah **SVM** dengan hasil:
| Metric | Score |
|---------|--------|
| Accuracy | 0.603 |
| Precision | 0.60 |
| Recall | 0.60 |
| F1-score | 0.59 |

---

## 📊 Hasil Akhir Analisis
Model terbaik yang diperoleh adalah **Support Vector Machine (SVM)** dengan akurasi validasi sebesar **60.3%**.  
Model ini digunakan untuk memprediksi data uji dan menghasilkan file submission (`submission-baru.csv`) dengan dua kolom:
| id | Emotion |
|----|----------|
| 5039 | Fear |
| 1147 | Love |
| 3623 | Happy |
| 4879 | Happy |
| 4162 | Happy |

---

## 💡 Insight dan Manfaat

### 🔎 Insight
- Dataset cenderung tidak seimbang (kelas “Happy” mendominasi), sehingga model kesulitan mencapai akurasi tinggi di semua kelas.  
- Proses *preprocessing* dengan Bahasa Indonesia (stopword + stemming) secara signifikan meningkatkan akurasi model.  
- *TF-IDF* efektif dalam menangkap fitur penting untuk emosi berbasis teks pendek seperti ulasan pelanggan.

### 🚀 Manfaat
- Dapat digunakan oleh bisnis untuk **analisis sentimen pelanggan secara otomatis**.  
- Membantu perusahaan dalam **pemantauan reputasi produk** dan **deteksi keluhan pelanggan**.  
- Menjadi dasar untuk pengembangan sistem **chatbot cerdas** yang dapat mengenali emosi pengguna.  
- Dapat diadaptasi untuk dataset lain dengan bahasa dan konteks berbeda.

---

## 🧭 Kesimpulan Akhir
Proyek **Emotion Classification** berhasil membangun pipeline lengkap *Natural Language Processing* mulai dari *data cleaning* hingga *model evaluation*.  
Model **SVM dengan TF-IDF** menghasilkan performa terbaik (akurasi 60.3%), membuktikan efektivitasnya dalam memahami ekspresi emosi berbasis teks Bahasa Indonesia.  
Implementasi proyek ini membuka peluang besar untuk pengembangan sistem analisis sentimen dan deteksi emosi otomatis dalam konteks bisnis dan layanan pelanggan.

---

## 👩‍💻 Tim Pengembang
| Nama | NRP |
|------|------|
| **Rehana Putri Salsabilla** | 5027221015 |

---
