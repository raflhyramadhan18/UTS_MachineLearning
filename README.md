# UTS Machine Learning - Klasifikasi Buah Jeruk & Anggur

Proyek ini bertujuan untuk membangun model machine learning yang dapat mengklasifikasikan buah ke dalam kategori **Jeruk (Orange)** atau **Anggur (Grapefruit)** berdasarkan fitur fisik dan warna.

## Identitas
* **Nama:** Raflhy Nur Ramadhan
* **NIM:** 1237050004
* **Kelas:** Informatika - Semester 6
* **Kampus:** UIN Sunan Gunung Djati Bandung

---

## 1. Data Collecting (Pengumpulan Data)
Dataset yang digunakan adalah dataset **Oranges vs. Grapefruit** yang diperoleh dari Kaggle. Dataset ini terdiri dari **10.000 baris data** dengan fitur-fitur sebagai berikut:
* **Target (Label):** `name` (Orange atau Grapefruit).
* **Fitur Fisik:** `diameter` dan `weight`.
* **Fitur Warna:** `red`, `green`, dan `blue` (RGB).

Data ini memiliki distribusi yang seimbang antara buah jeruk dan anggur (5.000 data per kelas).

---

## 2. Exploratory Data Analysis (EDA)
Sebelum pemodelan, dilakukan analisis sebaran data menggunakan Histogram dan KDE untuk melihat bagaimana fitur-fitur tersebut membedakan kedua jenis buah.

![Sebaran Data](images/sebaran_data.png)

**Analisis Visual:**
* Fitur **diameter** dan **weight** menunjukkan pemisahan yang signifikan; anggur cenderung lebih besar dan lebih berat daripada jeruk.
* Fitur **warna (RGB)** memiliki tumpang tindih (*overlap*) yang lebih banyak, namun tetap memberikan informasi tambahan bagi model.

---

## 3. Data Preprocessing
Langkah-langkah yang dilakukan untuk menyiapkan data:
1. **Label Encoding:** Mengubah kategori tekstual `name` menjadi nilai biner (0 untuk Grapefruit, 1 untuk Orange).
2. **Feature Scaling:** Menggunakan `StandardScaler` untuk menstandarisasi rentang nilai fitur (terutama weight dan diameter) agar tidak ada fitur yang mendominasi fitur lainnya secara numerik.
3. **Data Splitting:** Membagi data menjadi **80% untuk pelatihan** (8.000 data) dan **20% untuk pengujian** (2.000 data).

---

## 4. Modelling & Evaluasi Mendalam

![Confusion Matrix DT](images/CM_DT.png)  ![Classification Report DT](images/CR_DT.png)


# Evaluasi Model: Decision Tree
Berdasarkan hasil pengujian model menggunakan *Confusion Matrix* dan *Classification Report*
## Precision (Ketepatan)
* **Grapefruit:** Dari seluruh buah yang diprediksi sebagai Grapefruit oleh model, sebanyak **94%** merupakan prediksi yang benar, sedangkan sekitar **6%** sebenarnya adalah Orange namun salah diprediksi sebagai Grapefruit.
* **Orange:** Dari seluruh buah yang diprediksi sebagai Orange oleh model, sebanyak **95%** merupakan prediksi yang benar, sedangkan sekitar **5%** sebenarnya adalah Grapefruit namun salah diprediksi sebagai Orange.

## Recall (Keberhasilan Menangkap)
* **Grapefruit:** Dari total **988** data Grapefruit yang sebenarnya, model berhasil mengidentifikasi **95%** (936 data) dengan benar. Sekitar **5%** sisanya gagal dikenali dan salah diklasifikasikan sebagai Orange.
* **Orange:** Dari total **1012** data Orange yang sebenarnya, model berhasil mengidentifikasi **94%** (947 data) dengan benar. Sekitar **6%** sisanya gagal dikenali dan salah diklasifikasikan sebagai Grapefruit.

## F1-Score
Nilai F1-Score untuk kedua kelas (Grapefruit dan Orange) berada di angka **0.94**, yang menunjukkan bahwa model memiliki keseimbangan yang sangat baik dan stabil antara *Precision* dan *Recall*.

## Support (Jumlah Data Uji)
* **Grapefruit:** 988 data.
* **Orange:** 1012 data.
* **Total Keseluruhan:** 2000 data.

## Kesimpulan Akurasi
Model Decision Tree ini menghasilkan **Accuracy Score sebesar 0.9415 (94.15%)**. Hal ini menunjukkan bahwa model sangat handal dan memiliki tingkat kesalahan yang rendah dalam membedakan antara buah Grapefruit dan Orange.

Komponen Matriks
Berdasarkan hasil visualisasi, kita dapat mengidentifikasi empat komponen utama:

| Komponen | Nama Teknis | Jumlah | Penjelasan |
| :--- | :--- | :--- | :--- |
| **True Negative (TN)** | Benar Grapefruit | **936** | Model dengan benar menebak buah Grapefruit sebagai Grapefruit. |
| **False Positive (FP)** | Salah Orange | **52** | Model menebak Orange, padahal sebenarnya adalah Grapefruit (Kesalahan Tipe I). |
| **False Negative (FN)** | Salah Grapefruit | **65** | Model menebak Grapefruit, padahal sebenarnya adalah Orange (Kesalahan Tipe II). |
| **True Positive (TP)** | Benar Orange | **947** | Model dengan benar menebak buah Orange sebagai Orange. |

---

### Pembedahan Per Kelas

#### **Kelas 0 (Grapefruit)**
* **Total Data Aktual:** 936 (TN) + 52 (FP) = **988 data**.
* **Keberhasilan:** Model berhasil menangkap **936** data original Grapefruit.
* **Kesalahan:** Terdapat **52** data Grapefruit yang "lolos" dan malah dianggap sebagai Orange oleh model.

#### **Kelas 1 (Orange)**
* **Total Data Aktual:** 65 (FN) + 947 (TP) = **1,012 data**.
* **Keberhasilan:** Model sangat baik dalam mengenali Orange dengan total **947** prediksi benar.
* **Kesalahan:** Terdapat **65** data Orange yang dideteksi secara keliru sebagai Grapefruit.

---

### Insight Evaluasi
* **Keseimbangan Model:** Selisih antara kesalahan di kedua sisi (52 vs 65) cukup tipis. Ini menandakan model tidak memiliki bias yang berat ke salah satu kelas (tidak *skewed*).
* **Akurasi Keseluruhan:** Jika kita menjumlahkan semua prediksi benar (936 + 947 = 1883) lalu dibagi total data (2000), maka didapatkan nilai **0.9415** atau **94.15%**, yang sesuai dengan *Accuracy Score* di Classification Report.
* **Identifikasi Eror:** Model sedikit lebih sering salah mengira Orange sebagai Grapefruit (65 kejadian) dibandingkan sebaliknya (52 kejadian).



---

### B. Naive Bayes
Model berbasis probabilitas Teorema Bayes.

* **Akurasi:** Mencapai **92.00%**.
* **Analisis:** Meskipun bekerja secara sederhana dengan asumsi independensi antar fitur, model ini sangat efisien dalam membedakan kelas berdasarkan nilai warna.
* **Kelemahan:** Memiliki jumlah salah prediksi yang sedikit lebih banyak pada data yang saling tumpang tindih.

![Confusion Matrix NB](images/CM_NB.png)
![Classification Report NB](images/CR_NB.png)

---

### C. Support Vector Machine (SVM)
Model yang mencari *hyperplane* terbaik untuk memisahkan kelas.

* **Akurasi:** Tertinggi di angka **95.15%**.
* **Analisis:** SVM paling unggul dalam proyek ini karena mampu menangani fitur diameter dan berat yang memiliki batas pemisahan linear yang cukup jelas.
* **Kelebihan:** Memiliki nilai F1-score paling stabil dan jumlah kesalahan prediksi paling minim.

![Confusion Matrix SVM](images/CM_SVM.png)
![Classification Report SVM](images/CR_SVM.png)

---

## 5. Ringkasan Perbandingan Akurasi

Berikut adalah hasil perbandingan akurasi akhir dari ketiga model:

| Algoritma | Accuracy Score |
| :--- | :--- |
| **Decision Tree** | 0.9415 |
| **Naive Bayes** | 0.9200 |
| **Support Vector Machine** | **0.9515** |

![Perbandingan Akurasi](images/perbandingan_akurasi.png)

---

## 6. Kesimpulan
Berdasarkan seluruh tahapan eksperimen, mulai dari pengolahan data hingga evaluasi, dapat disimpulkan bahwa:
1. Karakteristik fisik (diameter dan berat) adalah indikator terkuat dalam klasifikasi jeruk vs anggur.
2. Ketiga model (Decision Tree, Naive Bayes, SVM) mampu mencapai akurasi di atas 90%.
3. **Support Vector Machine (SVM)** terpilih sebagai model terbaik dengan akurasi **95.15%**, menjadikannya model yang paling handal untuk diimplementasikan dalam sistem klasifikasi ini.

