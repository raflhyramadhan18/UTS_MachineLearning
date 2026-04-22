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

Kami membandingkan tiga algoritma klasifikasi dengan hasil evaluasi sebagai berikut:

### A. Decision Tree
Model ini membagi data berdasarkan serangkaian aturan keputusan.

* **Precision (Ketepatan):**
    - Dari seluruh buah yang diprediksi sebagai **grapefruit**, sebanyak **95%** merupakan prediksi yang benar.
    - Dari seluruh buah yang diprediksi sebagai **orange**, sebanyak **94%** merupakan prediksi yang benar.
* **Recall (Keberhasilan Menangkap):**
    - Dari total **1011 data grapefruit**, model berhasil mengidentifikasi **94% (±952 data)** dengan benar. Sekitar 6% (59 data) salah diklasifikasikan sebagai orange.
    - Dari total **989 data orange**, model berhasil mengidentifikasi **95% (±938 data)** dengan benar. Sekitar 5% (51 data) salah diklasifikasikan sebagai grapefruit.
* **F1-Score:** Berada di kisaran **0.94**, menunjukkan keseimbangan yang sangat baik antara presisi dan recall.
* **Confusion Matrix:** Berhasil mengklasifikasikan 952 (TN) dan 938 (TP) dengan benar.

![Confusion Matrix DT](images/CM_DT.png)
![Classification Report DT](images/CR_DT.png)

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

